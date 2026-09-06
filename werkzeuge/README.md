# Werkzeuge und Anbieter

Übersicht der Werkzeuge, auf die sich die Anwendungsfälle in diesem Repo
stützen, sowie ein Katalog klassischer Automatisierungswerkzeuge über
weitere Branchen (Abschnitt
["Klassische Automatisierung nach Branche"](#klassische-automatisierung-nach-branche-kein-ki-bezug)
unten). Keine vollständige Marktübersicht, sondern eine Auswahl, die für
Betriebe ohne eigenes IT-Team praktikabel ist. Preise ändern sich häufig —
wo nicht sicher, steht `[PRÜFEN]` statt einer geschätzten Zahl. Prüfen Sie
Preise vor einer Entscheidung immer direkt beim Anbieter.

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
Sie lösen keine Modelllizenz-, Zugriffs- oder Datenschutzprüfung. Was
Techniken wie Quantisierung oder Continuous Batching, die in solchen
Werkzeugen stecken, tatsächlich bewirken: siehe
[`grundlagen/llm-optimierung.md`](../grundlagen/llm-optimierung.md).

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

## Klassische Automatisierung nach Branche (kein KI-Bezug)

Diese Werkzeuge haben keine KI-Komponente — die EU-AI-Act-Hinweise in
[`recht/`](../recht/) gelten hier nicht (siehe
[`recht/README.md`](../recht/README.md), Abschnitt „Geltungsbereich“).
Es sind reine Werkzeug-Steckbriefe (Lizenz, Hosting, ein Hinweis), keine
ausgearbeiteten Anwendungsfälle — Kosten-, Nutzen- und Datenschutzprüfung
für den jeweiligen Betrieb stehen noch aus (siehe
[`AGENTS.md`](../AGENTS.md#nicht-ziele)). Stand der Recherche: 2026-09-06.

### IT/DevOps

| Werkzeug | Lizenz | Selbst hostbar | Hinweis |
| --- | --- | --- | --- |
| [Ansible](https://github.com/ansible/ansible) | GPL-3.0 | Ja, agentenlos per SSH | Konfigurationsmanagement und Provisionierung. Red Hats kostenpflichtige „Ansible Automation Platform“ ergänzt Clustering/Analytics, der Kern bleibt frei. |
| [Terraform](https://github.com/hashicorp/terraform) | Business Source License 1.1 seit August 2023 — **kein OSI-Open-Source mehr** | Eingeschränkt (BSL verbietet konkurrierende kommerzielle Nutzung) | Infrastructure as Code für Cloud-Ressourcen. Lokale/offene Alternative: [OpenTofu](https://github.com/opentofu/opentofu) — Apache-2.0-Fork unter der Linux Foundation, entstanden genau wegen dieser Lizenzänderung. |
| [Jenkins](https://github.com/jenkinsci/jenkins) | MIT | Ja | CI/CD-Automatisierungsserver, community-geführt. CloudBees bietet eine kommerzielle Managed-Variante separat an. |

### Fertigung/Industrie

| Werkzeug | Lizenz | Selbst hostbar | Hinweis |
| --- | --- | --- | --- |
| [OpenPLC](https://github.com/Autonomy-Logic/openplc-runtime) | MIT (aktuelle v4-Linie; ältere v3 war GPL-3.0) | Ja — Linux, Raspberry Pi, Windows, Docker | Offene Soft-SPS (IEC 61131-3). Das Projekt wechselte von der alten v3-Codebasis zu einer neuen Organisation (Autonomy-Logic) und MIT-Lizenz — genaues Umstellungsdatum `[PRÜFEN]`, vor Einsatz aktuellen Repo-Stand prüfen. |
| [Node-RED](https://github.com/node-red/node-red) | Apache 2.0 | Ja — läuft auf Node.js, z. B. Raspberry Pi | Low-Code-Automatisierung für IoT und ereignisgetriebene Abläufe, unter der OpenJS Foundation. |

### Finanzen/Handel

| Werkzeug | Lizenz | Selbst hostbar | Hinweis |
| --- | --- | --- | --- |
| [ccxt](https://github.com/ccxt/ccxt) | MIT | Ja — Bibliothek, läuft in eigener Infrastruktur | Einheitliche API-Anbindung an über 100 Kryptobörsen für eigenen Handelscode. |
| [QuantConnect Lean](https://github.com/QuantConnect/Lean) (Engine) | Apache 2.0 | Ja — lokale Installation, Backtesting und Live-Handel ohne Cloud-Pflicht laut Projekt-Dokumentation | Algorithmische Handels-Engine. Von der kommerziellen QuantConnect-Cloud-Plattform (baut auf derselben Engine auf) zu unterscheiden. |

### Gesundheitswesen

| Werkzeug | Lizenz | Selbst hostbar | Hinweis |
| --- | --- | --- | --- |
| [HAPI FHIR](https://github.com/hapifhir/hapi-fhir) | Apache 2.0 | Ja | Java-Implementierung des HL7-FHIR-Standards für Client-/Server-Interoperabilität im Gesundheitswesen. Kommerziellen Support bietet Smile Digital Health, ohne den Kern umzulizenzieren. |
| [OpenMRS](https://github.com/openmrs/openmrs-core) | MPL 2.0 mit Healthcare-Disclaimer | Ja — Jetty, Cargo, Docker | Patientenbasiertes elektronisches Patientenaktensystem für ressourcenarme Gesundheitseinrichtungen. Verarbeitet Patientendaten — DSGVO-/AVV-Prüfung ist hier nicht optional (siehe [`recht/README.md`](../recht/README.md)). |

### Handel/E-Commerce

| Werkzeug | Lizenz | Selbst hostbar | Hinweis |
| --- | --- | --- | --- |
| [Saleor](https://github.com/saleor/saleor) | BSD-3-Clause | Ja | Headless, GraphQL-basierte E-Commerce-Plattform. Saleor Cloud ist ein separates kostenpflichtiges Hosting-Angebot, der Code selbst bleibt offen. |
| [Magento 2 / Magento Open Source](https://github.com/magento/magento2) | Open Software License 3.0 | Ja | Offene E-Commerce-Plattform. Adobe Commerce ist die kostenpflichtige Erweiterung (B2B-Funktionen, KI-Merchandising, optional gemanagtes Cloud-Hosting) auf demselben Kern — Preise `[PRÜFEN]` direkt bei Adobe. |

### Smart Home / Gebäudeautomation

| Werkzeug | Lizenz | Selbst hostbar | Hinweis |
| --- | --- | --- | --- |
| [Home Assistant](https://github.com/home-assistant/core) | Apache 2.0 | Ja — Kernprinzip lokaler Betrieb, z. B. Raspberry Pi | Herstellerübergreifende Smart-Home-Zentrale. Nabu Casa bietet einen optionalen kostenpflichtigen Cloud-Zusatz (Fernzugriff, Sprachassistenten); Kernfunktion bleibt lokal und kostenlos. |
| [openHAB](https://github.com/openhab/openhab-core) | Eclipse Public License 2.0 `[PRÜFEN — Angabe aus Sekundärquellen, vor Verwendung direkt am Repository gegenprüfen]` | Ja — Kernprinzip lokaler Betrieb | Herstellerneutrale Automatisierungsplattform für Gebäude/Smart Home, unter der openHAB Foundation. |

### Robotik

| Werkzeug | Lizenz | Selbst hostbar | Hinweis |
| --- | --- | --- | --- |
| [ROS 2](https://github.com/ros2/ros2) | Kein einheitliches Lizenzmodell — Kernbibliotheken überwiegend Apache 2.0, einzelne Pakete abweichend (u. a. BSD, LGPL); je Paket prüfen | Ja — läuft auf eigener Roboter-/Recheneinheit, keine Cloud-Pflicht | Middleware und Werkzeuge für Roboterentwicklung. ROS 1 (letzte Distribution „Noetic“) erreichte am 31. Mai 2025 das End of Life — für neue Vorhaben ROS 2 verwenden. |
| [ArduPilot](https://github.com/ArduPilot/ardupilot) | GPL-3.0 | Ja — läuft auf eigener Flugsteuerungshardware | Autopilot-Software für Drohnen, Fahrzeuge, Boote und Unterwasserfahrzeuge (ArduPlane, ArduCopter, ArduRover, ArduSub). |

### Marketing/Social Media

| Werkzeug | Lizenz | Selbst hostbar | Hinweis |
| --- | --- | --- | --- |
| [Rasa](https://github.com/RasaHQ/rasa) | Apache 2.0 | Ja | Framework für Conversational AI (NLU, Dialogmanagement). Laut offiziellem Repository befindet sich „Rasa Open Source“ **im Wartungsmodus** — die Weiterentwicklung konzentriert sich auf die kostenpflichtige „Rasa Platform“ und „Hello Rasa“. Vor einer Entscheidung aktuellen Stand direkt im Repository prüfen. |
| [InstaPy](https://github.com/InstaPy/InstaPy) | GPL-3.0 | Technisch ja, **nicht empfohlen** | Automatisiert Instagram-Interaktionen per Browser-Steuerung. Letzter inhaltlicher Commit Dezember 2022, über 500 offene Issues; das Projekt warnt selbst vor Konto-Sperrungen durch Instagram. Hohes Risiko für Konto- und Reputationsschäden — für einen Betrieb nicht geeignet. |

## Wie diese Liste zu lesen ist

Ein Werkzeug in dieser Tabelle ist keine Empfehlung ohne Prüfung. Für die
KI-Werkzeuge oben ist es der Ausgangspunkt für den jeweiligen
Anwendungsfall — Details zu Kosten und Datenschutz stehen dort unter
Punkt 4 und 7, nicht hier. Für die klassischen Automatisierungswerkzeuge
nach Branche gibt es noch keinen Anwendungsfall dazu; Kosten- und
Datenschutzprüfung sind dort vollständig Aufgabe des jeweiligen Betriebs.

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
