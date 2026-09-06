# RAG in der Produktion: sieben Fehlerquellen

Technische Vertiefung für IT- und Entwicklungsverantwortliche, die ein
Retrieval-Augmented-Generation-System selbst bauen, einführen oder
betreiben. Ergänzt [`evaluation.md`](evaluation.md) und die
RAG-Mindestkontrollen in
[`sicherheit/README.md`](../sicherheit/README.md#3-rag-spezifisch). Kein
Bestandteil der sechs Basis-Module — vorausgesetzt wird
[Modul 1, Abschnitt 4](01-grundbegriffe.md#4-rag-retrieval-augmented-generation).

Die sieben Probleme treten typischerweise erst auf, wenn ein
RAG-Prototyp auf echte Nutzerfragen und einen echten, wachsenden
Dokumentbestand trifft — nicht in der Demo mit einer Handvoll
Testdokumenten. Stand: 2026-09-06.

## 1. Schlechte Chunking-Strategie (Bad Chunking)

**Was passiert:** Dokumente werden vor der Indexierung in Abschnitte
("Chunks") zerlegt. Eine zu starre Zerlegung — etwa nach fester
Zeichenzahl, ohne Rücksicht auf Absätze oder Tabellen — trennt
zusammengehörige Informationen, vermischt Themen in einem Chunk oder
trifft nicht die richtige Detailebene. Ein zu kleiner Chunk verliert
Kontext, ein zu großer verwässert die Relevanz beim Retrieval.

**Anzeichen:** Eine Antwort zitiert einen Chunk, der nur die Hälfte eines
Arguments enthält; eine Tabelle wird mitten in einer Zeile zerschnitten;
das Retrieval liefert Treffer, die nur am Rand zum Thema passen.

**Gegenmaßnahme:** Struktur des Dokuments beim Chunking berücksichtigen
(Überschriften, Absätze, Tabellen als Einheit behalten), Chunk-Größe an
den Dokumenttyp anpassen und mit überlappenden Chunks experimentieren.
Kein Chunking-Parameter ist ohne Test an echten Dokumenten des eigenen
Bestands verlässlich.

Quelle: [Pinecone, Chunking Strategies](https://www.pinecone.io/learn/chunking-strategies/).

## 2. Schwaches Retrieval (Poor Retrieval)

**Was passiert:** Die relevante Information existiert im Dokumentbestand,
wird aber von der Suche nicht gefunden — falsches Embedding-Modell für
Sprache oder Fachdomäne, zu enges Ähnlichkeitsmaß, fehlende
Keyword-Ergänzung bei Fachbegriffen, Artikel- oder Auftragsnummern. Die
Generierung kann ein Problem, das schon beim Retrieval entsteht, nicht
mehr reparieren.

**Anzeichen:** Das Modell antwortet mit "keine Information gefunden",
obwohl der Bestand die Antwort enthält; unterschiedliche Formulierungen
derselben Frage liefern völlig unterschiedliche Trefferqualität.

**Gegenmaßnahme:** Retrieval-Qualität getrennt von der Endantwort messen
(Recall, MRR — siehe [`evaluation.md`, Abschnitt 2](evaluation.md#2-messgrößen)),
Hybrid-Suche (Vektor- plus Keyword-Suche) bei Fachbegriffen und Nummern
einsetzen, einen Reranking-Schritt nach der ersten Suche ergänzen.

Quelle: [Databricks, Retrieval Quality](https://docs.databricks.com/aws/en/ai-search/retrieval-quality).

## 3. Lost in the Middle

**Was passiert:** Sprachmodelle nutzen Informationen am Anfang und Ende
eines langen Kontexts nachweislich zuverlässiger als Informationen in der
Mitte. Bei vielen abgerufenen Chunks kann eine tatsächlich relevante, aber
mittig platzierte Information im Kontext untergehen, obwohl sie technisch
vorhanden war.

**Anzeichen:** Eine Antwort ignoriert einen abgerufenen, thematisch
passenden Chunk, sobald viele andere Chunks gleichzeitig übergeben
werden; eine geringere Trefferzahl verbessert überraschend die
Antwortqualität.

**Gegenmaßnahme:** Nicht mehr Chunks übergeben als nötig, die
relevantesten Treffer per Reranking an den Anfang oder das Ende der
Kontextreihenfolge stellen, Ausgabe stichprobenartig gegen die
tatsächlich abgerufenen Chunks prüfen statt sich auf den gefühlten
Eindruck zu verlassen.

Quelle: Liu et al. (2023), *"Lost in the Middle: How Language Models Use
Long Contexts"*, [arXiv:2307.03172](https://arxiv.org/abs/2307.03172).

## 4. Veraltetes Wissen (Stale Knowledge)

**Was passiert:** Der Suchindex wird nicht automatisch aktualisiert, wenn
sich Quelldokumente ändern, gelöscht oder ersetzt werden. Das System
antwortet dann mit korrekt zitierten, aber inhaltlich überholten
Informationen — etwa einer alten Preisliste oder einer bereits ersetzten
Arbeitsanweisung.

**Anzeichen:** Eine Antwort verweist korrekt auf ein Dokument, dessen
Inhalt sich seit der letzten Indexierung geändert hat; gelöschte
Dokumente tauchen weiterhin in Antworten auf.

**Gegenmaßnahme:** Reindexierung an Dokumentänderungen koppeln, nicht nur
an einen festen Zeitplan; gelöschte Dokumente aktiv aus Index, Cache und
Embeddings entfernen (siehe
[`sicherheit/README.md#3-rag-spezifisch`](../sicherheit/README.md#3-rag-spezifisch));
ein Gültigkeitsdatum als Metadatenfeld je Dokument führen und in der
Antwort mit ausgeben.

Quelle: [LlamaIndex, Document Management](https://developers.llamaindex.ai/python/framework/module_guides/indexing/document_management/).

## 5. Kontext-Überlauf (Context Overflow)

**Was passiert:** Abgerufene Chunks, Systemanweisung und Gesprächsverlauf
überschreiten zusammen das Kontextfenster des Modells (siehe
[Modul 1, Abschnitt 2](01-grundbegriffe.md#2-token-kontextfenster-systemprompt)).
Je nach Implementierung wird dann stillschweigend gekürzt — im
ungünstigsten Fall verdrängt ein zuletzt hinzugefügter Chunk die
eigentliche Anweisung.

**Anzeichen:** Das Modell ignoriert Formatvorgaben aus der
Systemanweisung, sobald viele Chunks abgerufen wurden; Antworten werden
in langen Gesprächen zunehmend unpräziser.

**Gegenmaßnahme:** Feste Obergrenze für Anzahl und Gesamtlänge der
abgerufenen Chunks definieren, Systemanweisung immer zuerst und getrennt
von Suchergebnissen platzieren, tatsächliche Kontextnutzung (Token je
Anfrage) protokollieren statt anzunehmen, dass sie unter dem Limit
bleibt.

Quelle: [Anthropic, Context Windows](https://platform.claude.com/docs/en/build-with-claude/context-windows).

## 6. Erfundene Quellenangaben (Hallucinated Citations)

**Was passiert:** Das Modell erzeugt eine Quellenangabe, die es nicht
tatsächlich verwendet hat, oder hängt eine korrekte Aussage an einen
falschen Beleg. Das wirkt besonders vertrauenswürdig, weil die Antwort
belegt aussieht, es aber nicht ist — eine Sonderform der Halluzination
aus [Modul 3, Abschnitt 1](03-grenzen-und-risiken.md#1-halluzination).

**Anzeichen:** Eine zitierte Quelle existiert nicht im Index; eine
Aussage ist inhaltlich richtig, die angegebene Quelle dazu aber ein
anderes, unpassendes Dokument.

**Gegenmaßnahme:** Zitate technisch aus den tatsächlich abgerufenen
Chunks erzeugen lassen (Zitat-IDs statt frei formulierter
Quellenangaben), nicht aus dem freien Text des Modells; jede Aussage mit
Kunden- oder Außenwirkung stichprobenartig gegen die zitierte Quelle
prüfen, bevor sie verwendet wird (siehe
[Modul 3, Abschnitt 6](03-grenzen-und-risiken.md#6-die-faustregel-für-jedes-ergebnis)).

Quelle: [Anthropic, Citations](https://platform.claude.com/docs/en/build-with-claude/citations).

## 7. Antwortzeit durch die Suche (Retrieval Latency)

**Was passiert:** Embedding-Berechnung, Vektorsuche, Metadatenfilterung
und ein zusätzlicher Reranking-Schritt addieren sich zur eigentlichen
Modell-Antwortzeit. Bei wachsendem Dokumentbestand oder mehreren
gleichzeitigen Nutzenden wird die Suche selbst zum Engpass, nicht das
Sprachmodell.

**Anzeichen:** Die Antwortzeit steigt spürbar mit der Größe des
Dokumentbestands, unabhängig vom verwendeten Modell; ein zusätzlicher
Reranking-Schritt verbessert die Qualität, verdoppelt aber spürbar die
Wartezeit.

**Gegenmaßnahme:** Suche, Filterung, Reranking und Modellantwort einzeln
messen statt nur die Gesamtzeit zu betrachten; Indexgröße und
Filterkriterien vor dem eigentlichen Vektorvergleich reduzieren;
Reranking nur auf eine bereits vorgefilterte, kleine Trefferzahl
anwenden, nicht auf den gesamten Index.

Quelle: [Pinecone, Decrease Latency](https://docs.pinecone.io/guides/optimize/decrease-latency).

## Einordnung für den eigenen Betrieb

Diese sieben Punkte sind Prüfkriterien, keine Checkliste, die ein
fertiges RAG-Produkt automatisch erfüllt. Wer ein RAG-System über ein
Werkzeug aus [`werkzeuge/README.md`](../werkzeuge/README.md) einführt
(z. B. RAGFlow, Haystack, LlamaIndex), sollte für jeden der sieben Punkte
konkret prüfen, wie das jeweilige Werkzeug damit umgeht — keines davon
gleicht sie automatisch aus. Vor dem Pilotbetrieb gelten zusätzlich die
Mindestkriterien aus
[`werkzeuge/README.md#mindestkriterien-vor-dem-pilotbetrieb`](../werkzeuge/README.md#mindestkriterien-vor-dem-pilotbetrieb)
und [`sicherheit/README.md#4-pilotfreigabe`](../sicherheit/README.md#4-pilotfreigabe).
