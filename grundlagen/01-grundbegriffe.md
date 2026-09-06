# Modul 1: Grundbegriffe

Ziel dieses Moduls: Sie können nach dem Lesen erklären, was ein
Sprachmodell tatsächlich tut, welche Begriffe im Betrieb häufig verwechselt
werden, und warum das für den täglichen Umgang mit einem KI-Werkzeug wichtig
ist.

## 1. Was ein Sprachmodell (LLM) tut — und was nicht

Ein Large Language Model (LLM, z. B. GPT-, Claude- oder Mistral-Modelle)
sagt auf Basis von Trainingsdaten das statistisch wahrscheinlichste
nächste Wortstück (Token, siehe Abschnitt 2) voraus, wieder und wieder, bis
eine vollständige Antwort entsteht. Daraus folgt unmittelbar:

- Es **versteht** eine Anfrage nicht im menschlichen Sinn, es setzt Muster
  fort, die in ähnlichem Zusammenhang gelernt wurden.
- Es kennt keine Fakten außerhalb seiner Trainingsdaten und ohne
  zusätzliche Werkzeuge (siehe RAG, Abschnitt 4) auch keine aktuellen
  betriebsinternen Informationen.
- Es kann **selbstbewusst Falsches** produzieren ("Halluzination") — ein
  falsches Datum, eine erfundene Norm, eine nicht existierende
  Telefonnummer wirken sprachlich genauso sicher wie eine korrekte Angabe.
  Wie stark das je nach Aufgabe ins Gewicht fällt, unterscheidet sich
  deutlich nach Modell und Aufgabentyp (siehe Studienübersicht in
  [`quellen/README.md`](../quellen/README.md#wissenschaftliche-studien)).
  Vertiefung: [Modul 3](03-grenzen-und-risiken.md).
- Die gleiche Eingabe kann bei zwei Durchläufen unterschiedliche Ausgaben
  liefern (Nicht-Determinismus) — wichtig für alles, was reproduzierbar
  sein muss (z. B. Buchhaltung).

## 2. Token, Kontextfenster, Systemprompt

Diese drei Begriffe erklären, warum ein KI-Werkzeug manchmal "vergisst",
was Sie zu Beginn geschrieben haben, oder warum Kosten pro Nutzung
schwanken:

- **Token:** kleinste Texteinheit, mit der ein Modell rechnet — grob ein
  Wortteil (Faustregel: 1 Token ≈ 0,75 deutsche Wörter). Cloud-Anbieter
  berechnen Kosten meist nach Token, siehe
  [`wirtschaftlichkeit/README.md`](../wirtschaftlichkeit/README.md#1-kosten-pro-vorgang-berechnen).
- **Kontextfenster:** die maximale Menge an Text (in Token), die ein
  Modell in einer Anfrage gleichzeitig "sehen" kann — Eingabe, bisheriger
  Gesprächsverlauf und Ausgabe zusammen. Ist das Fenster voll, fällt
  älterer Inhalt aus der Betrachtung. Die genaue Größe unterscheidet sich
  je Modell und Anbieter — bei einer konkreten Aufgabe mit großen
  Dokumenten vor Einsatz prüfen, nicht raten.
- **Systemprompt:** eine feste Anweisung, die vor jeder Nutzeranfrage an
  das Modell mitgegeben wird (z. B. "Sie antworten ausschließlich auf
  Deutsch und in Stichpunkten"). Wird bei fertigen Chat-Oberflächen oft vom
  Anbieter oder von der IT-Abteilung vorkonfiguriert, nicht von der
  einzelnen Nutzerin oder dem einzelnen Nutzer.

## 3. Fine-Tuning, Prompting, Embeddings — drei unterschiedliche Wege

Diese Begriffe fallen oft in Anbietergesprächen und werden leicht
verwechselt:

| Begriff | Bedeutung | Wann relevant für einen Kleinbetrieb |
| --- | --- | --- |
| Prompting | Das Modell bekommt Anweisung und Kontext bei jeder Anfrage neu mitgegeben, ohne dass sich das Modell selbst verändert | Regelfall für die meisten Anwendungsfälle in diesem Repo — kein technischer Zusatzaufwand |
| Retrieval-Augmented Generation (RAG) | Passende Dokumente werden vor der Antwort automatisch gesucht und als Kontext mitgegeben (siehe Abschnitt 4) | Wenn betriebsinternes Wissen gebraucht wird, das im Prompt allein zu umfangreich wäre |
| Fine-Tuning | Ein bestehendes Modell wird mit eigenen Beispieldaten zusätzlich trainiert und dadurch dauerhaft verändert | Selten für einen Betrieb dieser Größenordnung sinnvoll — hoher Aufwand, Daten- und Wartungsbedarf; vor einer Entscheidung prüfen, ob Prompting oder RAG das Problem nicht bereits löst |
| Embeddings | Zahlendarstellung von Text, die Bedeutungsähnlichkeit misst; technische Grundlage von RAG und semantischer Suche | Kein eigenständiges Werkzeug, sondern ein Baustein innerhalb von RAG-Systemen |

## 4. RAG (Retrieval-Augmented Generation)

RAG bedeutet: Bevor das Modell antwortet, werden passende Ausschnitte aus
einer eigenen Dokumentensammlung (z. B. Firmenwiki, Handbücher,
Auftragshistorie) automatisch gesucht und dem Modell als Kontext
mitgegeben. So kann ein Modell auch zu Inhalten antworten, die es nie
"gelernt" hat.

- **Löst:** das Problem fehlenden betriebsinternen Wissens, ohne ein
  eigenes Modell trainieren zu müssen.
- **Löst nicht:** Halluzination vollständig — das Modell kann den
  gefundenen Kontext trotzdem falsch wiedergeben oder ergänzen. Siehe dazu
  die Studie zu Halluzinationsraten bei dokumentenbasierten Abfragen in
  [`quellen/README.md`](../quellen/README.md#wissenschaftliche-studien).
- Relevant für den Backlog-Anwendungsfall "interne Wissenssuche über
  Firmendokumente" in der Haupt-[README](../README.md).
- Technische Umsetzung typischerweise über Frameworks wie LlamaIndex oder
  Haystack, siehe [`quellen/README.md`](../quellen/README.md#etablierte-open-source-frameworks-für-eigene-technische-umsetzung).

## 5. Begriffe, die im Alltag oft vermischt werden

| Begriff | Bedeutung |
| --- | --- |
| Chatbot | Konversationelle Oberfläche zu einem LLM, meist ohne eigene Handlungsfähigkeit |
| Workflow (n8n/Make) | Fest programmierte Schrittfolge; KI ist nur ein Baustein darin |
| KI-Agent | System, das selbst entscheidet, welche Werkzeuge/Schritte als Nächstes nötig sind, statt einer festen Schrittfolge zu folgen — dadurch flexibler, aber schwerer vorhersehbar |
| RAG | siehe Abschnitt 4 — Wissensanbindung, kein eigenständiger Systemtyp |
| Foundation Model | großes, allgemein trainiertes Basismodell (z. B. GPT-, Claude-, Llama-Reihe), das per Prompting, RAG oder Fine-Tuning an eine konkrete Aufgabe angepasst wird |

## Weiter mit Modul 2

[Modul 2: Prompting in der Praxis](02-prompting.md) — mit den vier
Grundprinzipien und Übungsvorlagen.
