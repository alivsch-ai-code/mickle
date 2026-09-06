# Evaluation von LLM-Anwendungen

Ein LLM-System ist erst dann für einen Betrieb geeignet, wenn seine Qualität
für die konkrete Aufgabe gemessen wurde. Ein allgemeiner Modellvergleich oder
eine gelungene Demo reicht nicht aus. Dieses Schema gilt für Prompts, RAG,
Workflows und Agenten.

## 1. Testset aufbauen

Legen Sie vor dem Pilotbetrieb ein kleines, anonymisiertes Testset an:

- 20 bis 50 typische Eingaben aus dem vorgesehenen Prozess.
- 5 bis 10 schwierige Fälle, etwa fehlende Angaben, schlechte OCR,
  widersprüchliche Dokumente oder Prompt-Injection-Versuche.
- Eine erwartete Ausgabe oder prüfbare Kriterien je Fall.
- Keine produktiven Kundendaten, Personalakten, Zugangsdaten oder
  vertraulichen Konstruktionsdaten.
- Version, Datum, Modell, Prompt, Workflow und Datenstand protokollieren.

Bei RAG-Systemen gehört zusätzlich die erwartete Quelle zum Testfall. Bei
strukturierter Extraktion gehören Pflichtfelder, zulässige Werte und das
Verhalten bei fehlenden Werten dazu.

## 2. Messgrößen

| Messgröße            | Frage                                            | Beispiel für ein Akzeptanzkriterium                                    |
| -------------------- | ------------------------------------------------ | ---------------------------------------------------------------------- |
| Aufgabenrichtigkeit  | Ist die Antwort inhaltlich korrekt?              | Alle kritischen Pflichtfelder stimmen.                                 |
| Quellenbezug         | Stützt die Antwort sich auf die richtige Quelle? | Jede Sachbehauptung verweist auf einen abgerufenen Abschnitt.          |
| Vollständigkeit      | Wurden relevante Angaben übernommen?             | Kein Pflichtfeld aus dem Auftrag fehlt.                                |
| Abstention           | Erkennt das System fehlende Grundlage?           | Bei fehlender Quelle wird nicht geraten.                               |
| Formatvalidität      | Ist die Ausgabe maschinenlesbar?                 | JSON entspricht dem Schema; ungültige Werte werden abgewiesen.         |
| Nacharbeit           | Wie viel menschliche Korrektur bleibt?           | Korrekturzeit je Vorgang wird vor und nach Pilot gemessen.             |
| Latenz               | Wie lange dauert ein Vorgang?                    | P95 bleibt innerhalb der Prozessanforderung.                           |
| Kosten               | Was kostet ein korrekt abgeschlossener Vorgang?  | Modell-, Plattform-, Speicher- und Prüfkosten getrennt rechnen.        |
| Sicherheitsverhalten | Werden riskante Eingaben erkannt oder blockiert? | Keine externe Eingabe löst ohne Freigabe eine irreversible Aktion aus. |

Recall, MRR und mAP sind für Retrieval nützlich. Haystack beschreibt diese
Metriken und getrennte Evaluationspipelines in der
[statistischen Evaluation](https://github.com/deepset-ai/haystack/blob/main/docs-website/docs/optimization/evaluation/statistical-evaluation.mdx).
LlamaIndex zeigt für RAG außerdem Quellenangaben und Evaluation als getrennte
Bausteine in seinem
[RAG-from-scratch-Leitfaden](https://github.com/run-llama/llama_index/blob/main/docs/src/content/docs/framework/optimizing/building_rag_from_scratch.md).

## 3. Regressionen verhindern

Führen Sie das Testset erneut aus, wenn sich eines dieser Elemente ändert:

- Modell oder Modellversion.
- Systemprompt, Promptvorlage oder Toolbeschreibung.
- Chunking, Embeddings, Reranking oder Dokumentbestand.
- Workflow, Berechtigungen, Parser oder Ausgabeformat.

Eine Änderung gilt erst als besser, wenn sie die kritischen Fälle nicht
verschlechtert. LLM-as-a-judge kann bei offenen Texten helfen, ersetzt aber
bei kritischen Feldern keine deterministische Prüfung durch Regeln oder eine
fachkundige Person. [Opik](https://github.com/comet-ml/opik) dokumentiert
Datensätze, Experimente, Traces, LLM-as-a-judge-Metriken und CI/CD-Tests als
eine mögliche technische Umsetzung.

## 4. Freigabeentscheidung

Dokumentieren Sie nach jedem Pilot:

1. Zweck und erlaubte Eingaben.
2. Testset-Version und Messwerte.
3. Bekannte Fehler und nicht abgedeckte Fälle.
4. Verantwortliche Person für die fachliche Prüfung.
5. Aktionen, die immer eine menschliche Freigabe brauchen.
6. Abschaltkriterium, etwa eine kritische Fehlerrate oder ein Datenabfluss.

Die Messwerte gelten nur für den getesteten Zweck. Sie sind kein allgemeines
Qualitätsurteil über ein Modell oder einen Anbieter.
