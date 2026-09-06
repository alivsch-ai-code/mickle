# Werkzeuge und Anbieter

Übersicht der Werkzeuge, auf die sich die Anwendungsfälle in diesem Repo
stützen. Keine vollständige Marktübersicht, sondern die Auswahl, die für
Betriebe mit 10 bis 500 Mitarbeitern ohne eigenes IT-Team praktikabel ist.
Preise ändern sich häufig — wo nicht sicher, steht `[PRÜFEN]` statt einer
geschätzten Zahl. Prüfen Sie Preise vor einer Entscheidung immer direkt
beim Anbieter.

Zu jedem Werkzeug: Serverstandort/Anbietersitz (relevant für DSGVO, siehe
[`recht/`](../recht/)) und ob eine lokale Alternative existiert.

## Automatisierungsplattformen (Orchestrierung von Abläufen)

| Werkzeug                | Modell                                                | Serverstandort                                     | Lokale Alternative                        |
| ----------------------- | ----------------------------------------------------- | -------------------------------------------------- | ----------------------------------------- |
| n8n                     | Source-available/fair-code, selbst hostbar oder Cloud | wählbar bei Self-Hosting; Cloud-Details `[PRÜFEN]` | ist selbst die lokale Alternative         |
| Make (ehem. Integromat) | Cloud, kein Self-Hosting                              | EU-Rechenzentrum wählbar                           | keine — bei Bedarf n8n self-hosted nutzen |
| Zapier                  | Cloud, kein Self-Hosting                              | USA                                                | keine — bei Bedarf n8n self-hosted nutzen |

Für Betriebe mit Datenschutzbedenken kann n8n selbst gehostet auf eigener
oder deutscher Infrastruktur ein geeigneter Ansatz sein. Das bedeutet nicht
automatisch, dass alle Daten im Haus bleiben: verbundene Cloud-Dienste,
Telemetrie, Backups und externe Webhooks müssen separat geprüft werden. Die
[n8n-Dokumentation zu Datenschutz und Self-Hosting](https://github.com/n8n-io/n8n-docs/blob/main/docs/privacy-and-security/README.md)
nennt eigene Lösch- und Aufbewahrungsprozesse für Self-Hosted-Betreiber.

## LLM-Anbieter (Cloud-APIs)

| Anbieter                       | Beispielmodelle                       | Serverstandort                            | Hinweis                                                                  |
| ------------------------------ | ------------------------------------- | ----------------------------------------- | ------------------------------------------------------------------------ |
| OpenAI                         | GPT-4o, GPT-5-Reihe                   | USA (EU-Datenverarbeitung teils optional) | AVV verfügbar, Details prüfen                                            |
| Anthropic                      | Claude-Modelle (Sonnet, Opus, Haiku)  | USA                                       | AVV verfügbar, Details prüfen                                            |
| Mistral AI                     | Mistral-Modelle (u. a. Mistral Large) | Vertrags- und Regionendetails `[PRÜFEN]`  | vor Einsatz AVV, Speicherort, Subprozessoren und Trainingsnutzung prüfen |
| Microsoft Azure OpenAI Service | GPT-Modelle über Azure                | EU-Region wählbar (z. B. Frankfurt)       | relevant, wenn ohnehin Microsoft-Vertrag besteht                         |

Preise pro Token/Anfrage: `[PRÜFEN]` — abhängig von Modell und
Vertragsform, ändert sich regelmäßig.

## Lokale/offene Modelle (Daten verlassen das Haus nicht)

| Werkzeug                                                                     | Zweck                                              |
| ---------------------------------------------------------------------------- | -------------------------------------------------- |
| Ollama                                                                       | Betrieb offener Sprachmodelle auf eigener Hardware |
| Offene Modelle (z. B. Llama-, Mistral-, Qwen-Reihe, jeweils offene Gewichte) | Basis für Ollama oder eigene Infrastruktur         |

Voraussetzung: ausreichend Rechenleistung (GPU) im Haus oder bei einem
Hosting-Anbieter mit Sitz in der EU. Eine pauschale Qualitätsaussage ist nicht
belastbar: Ergebnisqualität hängt von Modell, Quantisierung, Hardware,
Kontextlänge und Aufgabe ab. Vor einer Entscheidung mit anonymisierten,
repräsentativen Beispielen testen und dieselben Testfälle gegen die geplante
Cloud-Alternative laufen lassen. Für RAG-Anwendungen zusätzlich Retrieval und
Quellenbezug messen, siehe [LlamaIndex](https://github.com/run-llama/llama_index/blob/main/docs/src/content/docs/framework/optimizing/building_rag_from_scratch.md)
und [Haystack](https://github.com/deepset-ai/haystack/blob/main/docs-website/docs/optimization/evaluation/statistical-evaluation.mdx).

## Texterkennung und Dokumentenverarbeitung (OCR)

| Werkzeug                                            | Modell                          | Hinweis                                          |
| --------------------------------------------------- | ------------------------------- | ------------------------------------------------ |
| Tesseract OCR                                       | Open Source, lokal              | Basis-OCR, keine Layoutanalyse                   |
| Azure AI Document Intelligence                      | Cloud                           | strukturierte Belege (Rechnungen, Lieferscheine) |
| Mistral OCR / Modell-native OCR großer LLM-Anbieter | Cloud oder lokal je nach Modell | für unstrukturierte, gemischte Dokumente         |

## Transkription (Audio zu Text)

| Werkzeug                                    | Modell           | Hinweis                                                   |
| ------------------------------------------- | ---------------- | --------------------------------------------------------- |
| Whisper (OpenAI, offene Gewichte)           | lokal betreibbar | für Meeting-/Baustellenprotokolle, siehe Anwendungsfall 6 |
| Cloud-Transkriptionsdienste großer Anbieter | Cloud            | schneller, aber Audiodaten verlassen das Haus             |

## Buchhaltungs- und Vertriebssoftware (Integrationsziele)

| Werkzeug           | Einsatzbereich                                                       |
| ------------------ | -------------------------------------------------------------------- |
| DATEV              | Buchhaltung, verbreitet bei Steuerberatern im deutschsprachigen Raum |
| Lexoffice, sevDesk | Cloud-Buchhaltung für kleinere Betriebe                              |

Diese Systeme werden in den Anwendungsfällen als Ziel für automatisiert
erfasste Belege genannt, nicht als von diesem Repo bereitgestelltes
Werkzeug.

## Wie diese Liste zu lesen ist

Ein Werkzeug in dieser Tabelle ist keine Empfehlung ohne Prüfung. Es ist
der Ausgangspunkt für den jeweiligen Anwendungsfall. Details zu Kosten und
Datenschutz stehen im jeweiligen Anwendungsfall unter Punkt 4 und 7, nicht
hier.
