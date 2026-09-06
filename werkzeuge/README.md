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

## Kurze Auswahlhilfe für Automatisierung

| Situation                                                  | Erster Prüfpunkt                                      | Passende GitHub-Referenz                                                                                                                                          |
| ---------------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Feste Abläufe zwischen E-Mail, ERP und Dateiablage         | Workflow-Orchestrierung mit Freigabeschritt           | [n8n](https://github.com/n8n-io/n8n) oder Make; n8n ist selbst hostbar, Make nicht.                                                                               |
| Visuelle LLM-App mit RAG und Agenten                       | Plattformumfang und Datenablage                       | [Dify](https://github.com/langgenius/dify) oder [Langflow](https://github.com/langflow-ai/langflow); beide sind nicht automatisch produktionssicher konfiguriert. |
| Interne Chatoberfläche für lokale Modelle                  | Authentifizierung, Dokumentrechte und Offline-Betrieb | [Open WebUI](https://github.com/open-webui/open-webui) mit [Ollama](https://github.com/ollama/ollama).                                                            |
| Viele Cloud- und lokale Modelle hinter einer Schnittstelle | Routing, Fallback, Kosten- und Schlüsselverwaltung    | [LiteLLM](https://github.com/BerriAI/litellm); ein Gateway wird zur zusätzlichen sicherheitskritischen Komponente.                                                |
| Hoher Durchsatz auf eigener GPU-Infrastruktur              | Serving, Batching und Hardwarekompatibilität          | [vLLM](https://github.com/vllm-project/vllm); für einzelne Büro-PCs meist überdimensioniert.                                                                      |
| Dokumentenlastige Wissenssuche                             | Parser, Chunking, Quellenbezug, Retrieval-Evaluation  | [RAGFlow](https://github.com/infiniflow/ragflow), [Haystack](https://github.com/deepset-ai/haystack) oder [LlamaIndex](https://github.com/run-llama/llama_index). |
| Messbare Qualität statt Demo-Eindruck                      | Testdatensatz, Traces, Regressionen, Kosten           | [Opik](https://github.com/comet-ml/opik), Haystack-Evaluation oder [DSPy](https://github.com/stanfordnlp/dspy).                                                   |

Die Tabelle ist eine Startauswahl. Vor einer Entscheidung müssen Lizenz,
Version, Sicherheitsmeldungen, Authentifizierung, Datenflüsse, Backup,
Löschung, Betriebskosten und ein Test mit anonymisierten Beispieldaten geprüft
werden.

## LLM-Anbieter (Cloud-APIs)

| Anbieter                       | Beispielmodelle                       | Serverstandort                            | Hinweis                                                                  |
| ------------------------------ | ------------------------------------- | ----------------------------------------- | ------------------------------------------------------------------------ |
| OpenAI                         | GPT-4o, GPT-5-Reihe                   | USA (EU-Datenverarbeitung teils optional) | AVV verfügbar, Details prüfen                                            |
| Anthropic                      | Claude-Modelle (Sonnet, Opus, Haiku)  | USA                                       | AVV verfügbar, Details prüfen                                            |
| Mistral AI                     | Mistral-Modelle (u. a. Mistral Large) | Vertrags- und Regionendetails `[PRÜFEN]`  | vor Einsatz AVV, Speicherort, Subprozessoren und Trainingsnutzung prüfen |
| Microsoft Azure OpenAI Service | GPT-Modelle über Azure                | EU-Region wählbar (z. B. Frankfurt)       | relevant, wenn ohnehin Microsoft-Vertrag besteht                         |

Preise pro Token/Anfrage: `[PRÜFEN]` — abhängig von Modell und
Vertragsform, ändert sich regelmäßig.

## Lokale, EU-gehostete und Cloud-Modelle getrennt bewerten

| Werkzeug                                                                     | Zweck                                                                         |
| ---------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| Ollama                                                                       | Betrieb offener Sprachmodelle auf eigener Hardware oder eigener Infrastruktur |
| Offene Modelle (z. B. Llama-, Mistral-, Qwen-Reihe, jeweils offene Gewichte) | Basis für Ollama oder eigene Infrastruktur                                    |

Eine lokale Ausführung auf eigener Hardware, EU-Hosting und Cloud-Betrieb sind
unterschiedliche Datenschutz- und Betriebsmodelle. EU-Hosting bedeutet nicht,
dass Daten das Unternehmen nicht verlassen. Auch bei lokaler Ausführung müssen
Backups, Telemetrie, Administrationszugänge, Plugins und externe APIs geprüft
werden.

Voraussetzung für eigene Hardware ist ausreichend Rechenleistung, meist GPU,
oder ein passend dimensionierter Server. Eine pauschale Qualitätsaussage ist nicht
belastbar: Ergebnisqualität hängt von Modell, Quantisierung, Hardware,
Kontextlänge und Aufgabe ab. Vor einer Entscheidung mit anonymisierten,
repräsentativen Beispielen testen und dieselben Testfälle gegen die geplante
Cloud-Alternative laufen lassen. Für RAG-Anwendungen zusätzlich Retrieval und
Quellenbezug messen, siehe [LlamaIndex](https://github.com/run-llama/llama_index/blob/main/docs/src/content/docs/framework/optimizing/building_rag_from_scratch.md)
und [Haystack](https://github.com/deepset-ai/haystack/blob/main/docs-website/docs/optimization/evaluation/statistical-evaluation.mdx).

Für kleine lokale Installationen ist Ollama ein einfacher Einstieg. Für
leistungsfähiges Serving mit vielen parallelen Anfragen sind [vLLM](https://github.com/vllm-project/vllm)
oder [llama.cpp](https://github.com/ggml-org/llama.cpp) technische Alternativen.
Sie lösen keine Modelllizenz-, Zugriffs- oder Datenschutzprüfung.

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

## Mindestkriterien vor dem Pilotbetrieb

- **Datenfluss:** Eingaben, Ausgaben, Logs, Embeddings, Backups und Telemetrie
  aufzeichnen.
- **Zugriff:** Rollen, Mandanten, Tool-Allowlist, Secrets und Netzwerkzugriffe
  testen.
- **Qualität:** 20 bis 50 repräsentative, anonymisierte Testfälle mit
  erwarteter Antwort oder erwarteten Feldern definieren.
- **Fehlerverhalten:** Unsicherheit, fehlende Quellen, Timeout, Anbieterfehler
  und widersprüchliche Dokumente testen.
- **Freigabe:** Aktionen mit Außenwirkung zunächst als Entwurf behandeln;
  Versand, Zahlung, Auftrag und Personalentscheidung benötigen eine benannte
  menschliche Freigabe.
- **Betrieb:** Update-, Backup-, Wiederherstellungs-, Lösch- und
  Abschaltprozess dokumentieren.
