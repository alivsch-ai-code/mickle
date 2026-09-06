# RAG-Techniken: sieben Bausteine für bessere Trefferqualität

Technische Vertiefung, Gegenstück zu
[`rag-produktionsprobleme.md`](rag-produktionsprobleme.md): Dort stehen
die Fehlerquellen, hier die Techniken, mit denen sie in der Praxis
adressiert werden. Für IT-/Entwicklungsverantwortliche, die ein
RAG-System selbst bauen oder ein Werkzeug aus
[`werkzeuge/README.md`](../werkzeuge/README.md) danach bewerten wollen.
Voraussetzung: [Modul 1, Abschnitt 4](01-grundbegriffe.md#4-rag-retrieval-augmented-generation).
Stand: 2026-09-06.

## 1. Hybrid Search

Kombiniert klassische Stichwortsuche (Keyword-/BM25-Suche) mit
semantischer Vektorsuche. Die Vektorsuche findet bedeutungsähnliche
Treffer auch bei anderer Formulierung, verpasst aber leicht exakte
Fachbegriffe, Artikelnummern oder Normbezeichnungen — genau dort ist die
Stichwortsuche stark. Adressiert direkt
[Problem 2, schwaches Retrieval](rag-produktionsprobleme.md#2-schwaches-retrieval-poor-retrieval).

Quelle: [Elastic, Hybrid Search](https://www.elastic.co/docs/solutions/search/hybrid-search).

## 2. Reranking

Nach der ersten, schnellen Suche (Vektor- oder Hybrid-Suche) bewertet ein
zweites, genaueres Modell die gefundenen Treffer erneut und ordnet sie
nach tatsächlicher Relevanz zur Anfrage neu. Verbessert die Trefferqualität
deutlich, kostet aber zusätzliche Zeit — siehe
[Problem 7, Antwortzeit durch die Suche](rag-produktionsprobleme.md#7-antwortzeit-durch-die-suche-retrieval-latency),
wo dieser Zielkonflikt explizit benannt ist.

Quelle: [Cohere, Rerank Overview](https://docs.cohere.com/docs/rerank-overview).

## 3. Query Rewriting

Die Nutzeranfrage wird vor der eigentlichen Suche durch ein Modell
umformuliert oder in mehrere Teilfragen zerlegt — etwa um Umgangssprache,
Tippfehler oder implizite Bezüge ("und der Rest?") in eine für die Suche
besser geeignete Form zu bringen. Nützlich bei Gesprächsverläufen, in
denen sich eine Anfrage auf vorherige Nachrichten bezieht.

Quelle: [LlamaIndex, Query Transformations](https://developers.llamaindex.ai/python/examples/query_transformations/).

## 4. Metadata Filtering

Die Suche wird vor dem eigentlichen Ähnlichkeitsvergleich auf eine
Teilmenge des Index eingeschränkt — nach Datum, Dokumenttyp, Abteilung
oder Zugriffsgruppe. Reduziert nicht nur falsche Treffer, sondern ist
auch eine Sicherheitskontrolle: Berechtigungen lassen sich so bereits
beim Retrieval durchsetzen, nicht erst nachträglich im Prompt (siehe
[`sicherheit/README.md#3-rag-spezifisch`](../sicherheit/README.md#3-rag-spezifisch)).

Quelle: [Pinecone, Filter by Metadata](https://docs.pinecone.io/guides/search/filter-by-metadata).

## 5. Contextual Retrieval

Jedem Chunk wird vor der Indexierung automatisch ein kurzer, vom Modell
erzeugter Kontext-Satz vorangestellt, der erklärt, wovon der Chunk
handelt und wie er im Gesamtdokument steht. Das verringert, dass ein aus
dem Zusammenhang gerissener Chunk (siehe
[Problem 1, schlechte Chunking-Strategie](rag-produktionsprobleme.md#1-schlechte-chunking-strategie-bad-chunking))
beim Retrieval falsch eingeordnet wird.

Quelle: [Anthropic, Contextual Retrieval](https://www.anthropic.com/engineering/contextual-retrieval).

## 6. Parent-Child Retrieval

Die Suche läuft auf kleinen, präzisen Chunks ("Child"), zurückgegeben
wird aber der größere, umgebende Abschnitt ("Parent"), aus dem der Chunk
stammt. Verbindet die Genauigkeit kleiner Chunks beim Auffinden mit dem
vollständigeren Kontext größerer Abschnitte bei der Beantwortung — eine
gezielte Antwort auf den Zielkonflikt aus
[Problem 1](rag-produktionsprobleme.md#1-schlechte-chunking-strategie-bad-chunking).

Quelle: [LlamaIndex, Retriever-Integrationen](https://developers.llamaindex.ai/python/framework/integrations/retrievers/).

## 7. Agentic RAG

Statt eines festen Ablaufs "suchen → antworten" entscheidet ein Agent
selbst, ob, wann, wie oft und mit welcher Suchanfrage er nachschlägt —
er kann eine erste Antwort selbst bewerten, bei Bedarf gezielt
nachrecherchieren und mehrere Quellen kombinieren, bevor er antwortet.
Technisch ein Anwendungsfall des allgemeinen Musters "Ziel definieren,
Modell plant und handelt, Ergebnis wird geprüft, bei Bedarf wird
nachgebessert", das in agentischen Systemen allgemein verwendet wird —
nicht spezifisch für RAG, siehe die Definition von KI-Agent in
[Modul 1, Abschnitt 5](01-grundbegriffe.md#5-begriffe-die-im-alltag-oft-vermischt-werden).
Leistungsfähiger als starres RAG, aber schwerer vorhersehbar und teurer
im Betrieb (mehrere Modellaufrufe statt einem) — die Freigabepflicht aus
[Modul 3, Abschnitt 6](03-grenzen-und-risiken.md#6-die-faustregel-für-jedes-ergebnis)
gilt hier unverändert, eher verstärkt. Ausführlicher zu Agenten-Mustern
und den tatsächlichen Mehrkosten mehrerer Agenten:
[`agentische-systeme.md`](agentische-systeme.md).

Quelle: [IBM, Agentic RAG](https://www.ibm.com/think/topics/agentic-rag).

## Einordnung für den eigenen Betrieb

Keine dieser sieben Techniken ist automatisch in einem RAG-Werkzeug aus
[`werkzeuge/README.md`](../werkzeuge/README.md) enthalten oder aktiviert.
Vor einer Entscheidung prüfen, welche der Techniken das gewählte Werkzeug
tatsächlich unterstützt, und die Wirkung mit dem eigenen Testset messen
(siehe [`evaluation.md`, Abschnitt 2](evaluation.md#2-messgrößen)) —
nicht am Prinzip allein, sondern an der Trefferqualität mit den eigenen
Dokumenten.
