# Quellen und verwandte Projekte

Anwendungsfälle und Automatisierungs-Vorlagen gibt es auf GitHub bereits
massenhaft — aber fast ausschließlich als reine Workflow- oder Code-Sammlung,
ohne Kosten-, Nutzen-, Grenzen- und Datenschutz-Betrachtung und ohne Bezug
zu KMU im deutschsprachigen Raum. Diese Liste ordnet die relevantesten
gefundenen Projekte ein und zeigt, wo sie sich mit diesem Repository
überschneiden — und wo nicht.

**Wichtig:** Dies sind Drittprojekte. Sie wurden nicht im Detail geprüft,
nicht getestet und werden hier nicht empfohlen, sondern nur eingeordnet.
Lizenz, Aktualität und Codequalität vor Übernahme in einen eigenen Betrieb
immer selbst prüfen. Stand der Recherche: 2026-09-06.

## Neu verifizierte Recherchepunkte

Die folgenden Projekte wurden für einzelne Aussagen in diesem Repository
gezielt in ihren öffentlich verfügbaren Dokumentationsdateien geprüft. Die
Prüfung belegt nur den jeweils genannten Inhalt, keine Eignung für einen
konkreten Betrieb.

| Punkt                                    | Beleg und Einordnung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Self-Hosting und Datenschutz bei n8n     | Die [offizielle n8n-Dokumentation zu Datenschutz](https://github.com/n8n-io/n8n-docs/blob/main/docs/privacy-and-security/README.md) unterscheidet Cloud und Self-Hosting, beschreibt Telemetrie und weist darauf hin, dass Self-Hosted-Betreiber eigene Lösch- und Aufbewahrungsprozesse verantworten. Das stützt die Empfehlung zur eigenen Betriebs- und Löschkonzeption, nicht die Aussage, dass Self-Hosting automatisch DSGVO-konform ist. Stand der Prüfung: 2026-09-06.                                                                                                                                                         |
| Agentenrisiken                           | Das [OWASP-Repository](https://github.com/GenAI-Security-Project/GenAI-LLM-Top10/tree/main/2025) führt für 2025 unter anderem Prompt Injection, Sensitive Information Disclosure, Improper Output Handling, Excessive Agency und Misinformation. Die ältere [OWASP-2023-Fassung](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/tab_archive.md) ist archiviert und sollte nicht als aktuelle Version bezeichnet werden. Stand der Prüfung: 2026-09-06.                                                                                                                                    |
| RAG nicht nur als Demo                   | [LlamaIndex beschreibt](https://github.com/run-llama/llama_index/blob/main/docs/src/content/docs/framework/optimizing/building_rag_from_scratch.md) getrennte Schritte für Ingestion, Retrieval, Response-Synthese mit Quellenangaben und Evaluation. [Haystack dokumentiert](https://github.com/deepset-ai/haystack/blob/main/docs-website/docs/optimization/evaluation/statistical-evaluation.mdx) Recall, MRR und getrennte Evaluationspipelines. Daraus folgt für dieses Repo: Ein RAG-Anwendungsfall braucht Testfragen, Quellenbezug und Messung der Retrieval-Qualität, nicht nur einen Chatbot. Stand der Prüfung: 2026-09-06. |
| Governance ist kein Konformitätsnachweis | Das [Microsoft Agent Governance Toolkit](https://github.com/microsoft/agent-governance-toolkit/blob/main/docs/compliance/eu-ai-act-checklist.md) kennzeichnet seine Abdeckung selbst als teilweise und grenzt Runtime-Governance von vollständiger Konformitätsbewertung ab. Das ist ein gutes Muster für dieses Repo: Checklisten und technische Kontrollen als Arbeitsmittel darstellen, nie als Rechtsnachweis. Stand der Prüfung: 2026-09-06.                                                                                                                                                                                      |
| Lokale Modelle und Schnittstellen        | Das offizielle [Ollama-Repository](https://github.com/ollama/ollama) beschreibt lokale Ausführung, REST API und Integrationen. Das belegt die technische Möglichkeit eines lokalen Ansatzes, aber weder eine bestimmte Modellqualität noch vollständige Vertraulichkeit bei falsch konfigurierten Netzwerk-, Telemetrie- oder Backup-Einstellungen. Stand der Prüfung: 2026-09-06.                                                                                                                                                                                                                                                     |

## Bewertungsmaßstab für GitHub-Quellen

GitHub-Quellen werden nach fünf Fragen eingeordnet: Ist es das offizielle
Repository? Ist die Lizenz für den geplanten Einsatz geeignet? Wann wurde der
konkrete Pfad zuletzt geändert? Gibt es Tests oder nur Beispielcode? Welche
Annahmen gelten für Datenschutz, Betrieb und Sicherheit? Eine Antwort
übernimmt aus einem Repository nur die Aussage, die der konkrete Pfad trägt.

## Kuratierte technische Auswahl, Stand 2026-09-06

Die Sternzahlen sind ein Popularitätssignal aus GitHub, kein Qualitätsurteil.
Sie wurden am 2026-09-06 abgelesen und veralten. Lizenz, Aktivität und
Einsatzgrenzen sind wichtiger als die Reihenfolge.

| Projekt                                                            |                                   GitHub-Snapshot | Wofür es technisch passt                                                                                                  | Für einen KMU-Pilot prüfen                                                                                                    |
| ------------------------------------------------------------------ | ------------------------------------------------: | ------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| [Dify](https://github.com/langgenius/dify)                         |                 ca. 154,6k Sterne; Release 1.17.0 | Selbst hostbare Plattform für Workflows, RAG, Agenten, Modellverwaltung und LLMOps; Docker-Compose-Einstieg dokumentiert. | Dify Open Source License mit Zusatzbedingungen, Ressourcenbedarf, Secrets, Rollen und Datenablage prüfen.                     |
| [Langflow](https://github.com/langflow-ai/langflow)                |                        ca. 154,3k; Release 1.12.0 | Visueller Builder für Agenten und Workflows, Python-Komponenten, API- und MCP-Bereitstellung.                             | Authentifizierung, Tool-Schutz, Mehrmandantenbetrieb und Exportierbarkeit der Flows prüfen.                                   |
| [Open WebUI](https://github.com/open-webui/open-webui)             |                        ca. 151,1k; Release 0.11.3 | Self-hosted Oberfläche für Ollama und OpenAI-kompatible APIs, RBAC, lokale RAG- und Evaluationsfunktionen.                | Open-WebUI-Lizenz und Branding-Bedingungen, Dokumentenrechte, Datenbank, Backups und Tool-Zugriffe prüfen.                    |
| [LangChain / LangGraph](https://github.com/langchain-ai/langchain) | ca. 145,8k; aktuelle LangChain-Core-Version 1.6.2 | Breites Entwickler-Ökosystem; LangGraph für kontrollierbare, zustandsbehaftete Agenten-Workflows.                         | Abstraktions- und Abhängigkeitsumfang, Tracing-Anbieter und Betriebsmodell prüfen.                                            |
| [llama.cpp](https://github.com/ggml-org/llama.cpp)                 |                         ca. 127,2k; Release 0.4.0 | Lokale C/C++-Inference, Quantisierung, CPU/GPU-Hybridbetrieb und OpenAI-kompatibler Server.                               | Modelllizenz, Hardware, Quantisierungsqualität, Updates und Netzwerkzugriff absichern.                                        |
| [vLLM](https://github.com/vllm-project/vllm)                       |                         ca. 91,1k; Release 0.28.0 | Hochdurchsatz-Serving für GPU-Infrastruktur, kontinuierliches Batching, strukturierte Ausgaben und OpenAI-kompatible API. | GPU-Kosten, CUDA-/Treiberbindung, Skalierungsbedarf und Betriebs-Know-how prüfen.                                             |
| [RAGFlow](https://github.com/infiniflow/ragflow)                   |                         ca. 90,1k; Release 0.27.1 | Dokumentenlastige RAG-Anwendungen mit DeepDoc, Chunking, Quellenbezug, Agenten und MCP.                                   | Ressourcenbedarf, x86-Einschränkung der Images, externe LLM-/Embedding-Dienste und Sandbox-Konfiguration prüfen.              |
| [OpenHands](https://github.com/OpenHands/OpenHands)                |                         ca. 86,3k; Release 1.16.0 | Coding-Agenten und Automatisierungen mit lokalen, Docker-, VM- oder Remote-Backends.                                      | Nicht als allgemeine Büroautomatisierung einsetzen; Sandbox, Dateirechte, Netzwerk und Kostenlimits zwingend prüfen.          |
| [LiteLLM](https://github.com/BerriAI/litellm)                      |                        ca. 58,2k; Release 1.100.0 | LLM-Gateway für viele Anbieter, einheitliche API, Routing, Fallbacks, Kosten- und Zugriffskontrolle.                      | Proxy-Sicherheit, Schlüsselverwaltung, Logging personenbezogener Prompts und Lizenzumfang prüfen.                             |
| [LlamaIndex](https://github.com/run-llama/llama_index)             |                        ca. 52,0k; Release 0.14.24 | Daten- und Agentenframework für Konnektoren, Indexierung, Retrieval, Dokumentverarbeitung und lokale Modelle.             | Integrationsanzahl, Paketpflege, Quellenzitate, Berechtigungstrennung und Cloud-Erweiterungen prüfen.                         |
| [DSPy](https://github.com/stanfordnlp/dspy)                        |                          ca. 37,8k; Release 3.3.1 | Programmierbarer Ansatz für modulare LLM-Systeme und messbare Prompt-/Programmoptimierung.                                | Geeignet für Entwicklung und Evaluation, aber nicht allein eine Betriebsplattform; Testdatensatz und Kostenlimits definieren. |
| [Haystack](https://github.com/deepset-ai/haystack)                 |                          ca. 26,4k; Release 3.1.1 | Modulare, explizite RAG- und Agentenpipelines mit Retrieval-, Routing-, Memory- und Evaluationskomponenten.               | Telemetrie deaktivieren oder bewerten, Self-Hosting-/Enterprise-Grenzen und Pipeline-Betrieb prüfen.                          |
| [Opik](https://github.com/comet-ml/opik)                           |                         ca. 21,8k; Release 2.2.52 | Self-hostbare Observability- und Evaluationsplattform für Traces, Datensätze, LLM-as-a-judge und CI/CD-Tests.             | Prompt- und Trace-Aufbewahrung, personenbezogene Daten, Zugriffsschutz und Löschfristen prüfen.                               |
| [Pydantic AI](https://github.com/pydantic/pydantic-ai)             |                         ca. 19,7k; Release 2.40.0 | Typisierte Agenten, strukturierte Ausgaben, Tool-Schemas, Evals und durable Workflows in Python.                          | Für Python-Entwicklung geeignet, aber eigene UI, Authentifizierung, Deployment- und Audit-Schicht erforderlich.               |

### Nicht mehr als aktive Top-Auswahl führen

- [Flowise](https://github.com/FlowiseAI/Flowise) ist seit dem 13. August 2026
  archiviert. Das Repository verweist auf die weitere Entwicklung außerhalb
  dieses Repos. Es kann als historische Referenz dienen, ist aber keine neue
  Standardempfehlung.
- [Continue](https://github.com/continuedev/continue) weist selbst darauf hin,
  dass das Repository nicht mehr aktiv gepflegt wird. Für neue VS-Code- oder
  JetBrains-Auswahl daher nur als archivierte Referenz führen.
- [Semantic Kernel](https://github.com/microsoft/semantic-kernel) verweist im
  README auf Microsoft Agent Framework als Nachfolger. Für neue Projekte
  zuerst die [Migrationsdokumentation](https://learn.microsoft.com/en-us/agent-framework/migration-guide/from-semantic-kernel)
  prüfen.

## Workflow-Vorlagen (n8n / Make)

Große, technische Sammlungen fertiger Workflows. Sinnvoll als
Ausgangspunkt für die Umsetzung in [`workflows/`](../workflows/), ersetzen
aber nicht die Einordnung nach Kosten/Nutzen/Grenzen, die dieses Repo
liefert.

| Projekt                                                                                                 | Umfang          | Hinweis                                                      |
| ------------------------------------------------------------------------------------------------------- | --------------- | ------------------------------------------------------------ |
| [enescingoz/awesome-n8n-templates](https://github.com/enescingoz/awesome-n8n-templates)                 | 280+ Templates  | Gmail, Telegram, Slack, RAG-Chatbots, Dokumentenverarbeitung |
| [ritik-prog/n8n-automation-templates-5000](https://github.com/ritik-prog/n8n-automation-templates-5000) | 5000+ Templates | CRM, Finance, E-Commerce, RAG                                |
| [Zie619/n8n-workflows](https://github.com/Zie619/n8n-workflows)                                         | 2000+ Templates | aggregiert aus n8n-Forum und Community                       |
| [wassupjay/n8n-free-templates](https://github.com/wassupjay/n8n-free-templates)                         | 200+ Templates  | Fokus auf Vector-DBs, Embeddings, LLM-Anbindung              |

Diese Mengen sind ein Grund, warum dieses Repo bewusst _keine_ weitere
Workflow-Sammlung sein will: Auswahl und Einordnung fehlen dort, nicht
Masse.

## KI-Agenten-Anwendungsfälle (branchenübergreifend)

Sammlungen von Anwendungsbeispielen für KI-Agenten, meist englischsprachig
und ohne KMU- oder DACH-Bezug. Nützlich zur Ideenfindung für das Backlog
in der Haupt-[README](../README.md).

| Projekt                                                                                         | Fokus                                                                            |
| ----------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| [ashishpatel26/500-AI-Agents-Projects](https://github.com/ashishpatel26/500-AI-Agents-Projects) | Kuratierte Fallsammlung über viele Branchen (Gesundheit, Finanzen, Handel u. a.) |
| [Arindam200/awesome-ai-apps](https://github.com/Arindam200/awesome-ai-apps)                     | RAG-, Agenten- und Workflow-Beispielprojekte                                     |
| [parkerluxu/Awesome-agent-cases](https://github.com/parkerluxu/Awesome-agent-cases)             | Büroautomatisierung, u. a. mit n8n                                               |
| [jim-schwoebel/awesome_ai_agents](https://github.com/jim-schwoebel/awesome_ai_agents)           | Über 1.500 Ressourcen und Tools rund um KI-Agenten                               |

## EU AI Act und Compliance

Vorlagen und Checklisten zur Rechtslage. Ergänzen den Orientierungstext in
[`recht/`](../recht/) dieses Repos, ersetzen aber keine Rechtsberatung —
dort gilt derselbe Vorbehalt wie hier.

| Projekt                                                                                         | Fokus                                                                  |
| ----------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| [GenAI-Gurus/awesome-eu-ai-act](https://github.com/GenAI-Gurus/awesome-eu-ai-act)               | Kuratierte Tools, offizielle Quellen, Vorlagen zur AI-Act-Vorbereitung |
| [kanad13/EU-AI-Act](https://github.com/kanad13/EU-AI-Act)                                       | DSGVO- und AI-Act-Compliance erklärt                                   |
| [microsoft/agent-governance-toolkit](https://github.com/microsoft/agent-governance-toolkit)     | Governance-Rahmen für autonome KI-Agenten, inkl. EU-AI-Act-Checkliste  |
| [mirkoschubert/datenschutz-checkliste](https://github.com/mirkoschubert/datenschutz-checkliste) | Deutschsprachige DSGVO-Checkliste                                      |

## Wissenschaftliche Studien

Kontrollierte Studien zu Produktivitätseffekten generativer KI. Keine
davon wurde im deutschen Mittelstand durchgeführt — sie liefern eine
Plausibilitätsprüfung für Nutzenrechnungen, keinen Ersatz für eigene
Messung. Eingeordnet in [`wirtschaftlichkeit/README.md`](../wirtschaftlichkeit/README.md#5-was-die-forschung-zu-zeitersparnis-zeigt).

| Studie                                                                                                                                                                                                                                                          | Kernbefund                                                                                                                                                                                                                                                                 |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Noy & Zhang, _Science_ (2023), [DOI 10.1126/science.adh2586](https://www.science.org/doi/10.1126/science.adh2586)                                                                                                                                               | Schreibaufgaben mit ChatGPT: ca. 40 % weniger Zeit, 18 % höhere Qualität                                                                                                                                                                                                   |
| Brynjolfsson, Li & Raymond, NBER Working Paper 31161 (2023), [nber.org/papers/w31161](https://www.nber.org/papers/w31161)                                                                                                                                       | Kundenservice mit KI-Assistent: 14 % mehr gelöste Vorgänge/Stunde im Schnitt, 34 % bei unerfahrenen Beschäftigten                                                                                                                                                          |
| _"How Much Do LLMs Hallucinate in Document Q&A Scenarios?"_, [arXiv:2603.08274](https://arxiv.org/html/2603.08274v1)                                                                                                                                            | Untersucht Halluzinationsraten bei dokumentenbasierten Abfragen (RAG) über Modelle, Kontextlängen und Temperaturen hinweg — relevant für den Backlog-Fall "interne Wissenssuche"                                                                                           |
| Evaluation von LLM-Informationsextraktion aus klinischen Texten, [PMC11713360](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11713360/)                                                                                                                          | Modellabhängige Halluzinationsrate bei strukturierter Extraktion (in dieser Studie: Llama2 27 vollständige Halluzinationen vs. ChatGPT 3 bei gleicher Aufgabe) — kein Beleg für Rechnungsverarbeitung, aber Beleg dafür, dass Modellwahl die Fehlerquote stark beeinflusst |
| _"Invoice Information Extraction: Methods and Performance Evaluation"_, [arXiv:2510.15727](https://arxiv.org/pdf/2510.15727)                                                                                                                                    | Vergleich von Verfahren zur Rechnungsdatenextraktion, Genauigkeitswerte im Bereich 94–98 % je nach Verfahren und Dokumentqualität — relevant für Anwendungsfall 4 (Belegerfassung), sobald dieser ausgearbeitet wird                                                       |
| Bitkom, _Künstliche Intelligenz in Deutschland_, Studienbericht 2026, [bitkom.org](https://www.bitkom.org/Bitkom/Publikationen/Kuenstliche-Intelligenz-in-Deutschland)                                                                                          | 41 % der Unternehmen nutzen KI aktiv, im Mittelstand deutlich seltener; Haupthemmnisse: Rechtsunsicherheit, fehlendes Know-how, Personalmangel                                                                                                                             |
| ifo Institut, Umfrage Mai 2026 (Pressemeldung Juni 2026, u. a. berichtet von [changement-magazin.de](https://changement-magazin.de/inspiration/impuls/zahlen-zur-ki-nutzung-ifo-institut-kuenstliche-intelligenz-ist-endgueltig-in-der-breite-angekommen-8262)) | 54,5 % der Unternehmen nutzen KI (breitere Stichprobe/andere Methodik als Bitkom — Zahlen sind nicht direkt vergleichbar)                                                                                                                                                  |

## Sicherheit bei LLM-Anwendungen

| Projekt                                                                                                 | Fokus                                                                                                                                                                                                                                                                                                   |
| ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [OWASP GenAI LLM Top 10 2025](https://github.com/GenAI-Security-Project/GenAI-LLM-Top10/tree/main/2025) | Aktuellere Referenz für Risiken wie Prompt Injection, Sensitive Information Disclosure, Improper Output Handling und Excessive Agency; die frühere OWASP-Projektseite ist archiviert. Grundlage für [`recht/README.md`](../recht/README.md#4-technisches-risiko-manipulierte-eingaben-prompt-injection) |

## Etablierte Open-Source-Frameworks (für eigene technische Umsetzung)

Für Betriebe mit eigener Entwicklungskapazität, die über No-Code-Workflows
(n8n/Make) hinaus eine eigene Anwendung bauen wollen — z. B. für den
Backlog-Fall "interne Wissenssuche über Firmendokumente":

| Projekt                                                             | Zweck                                                                                                                                                                                                    |
| ------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | Verbreitetes Framework zum Verketten von LLM-Aufrufen, Werkzeugen und Datenquellen                                                                                                                       |
| [run-llama/llama_index](https://github.com/run-llama/llama_index)   | Framework mit Schwerpunkt auf Retrieval-Augmented Generation (RAG) über eigene Dokumente                                                                                                                 |
| [deepset-ai/haystack](https://github.com/deepset-ai/haystack)       | RAG- und Such-Framework, ursprünglich aus einem deutschen Unternehmen (deepset, Berlin)                                                                                                                  |
| [BerriAI/litellm](https://github.com/BerriAI/litellm)               | Einheitliche Schnittstelle zu über 100 LLM-APIs — vereinfacht den Anbieterwechsel aus Punkt 4 der [Wirtschaftlichkeits-Übersicht](../wirtschaftlichkeit/README.md#4-anbietervergleich-worauf-es-ankommt) |

## Kostenrechner für LLM-APIs

Werkzeuge, die aktuelle Preise ziehen und vergleichen — nützlich als
Ergänzung zu Abschnitt 4 ("Kosten") in jedem Anwendungsfall, statt Preise
hier im Repo manuell nachzupflegen.

| Projekt                                                           | Fokus                                                   |
| ----------------------------------------------------------------- | ------------------------------------------------------- |
| [AgentOps-AI/tokencost](https://github.com/AgentOps-AI/tokencost) | Preisschätzung für 400+ LLMs                            |
| [LLMWise-AI/llm-cost](https://github.com/LLMWise-AI/llm-cost)     | Kommandozeilen-Vergleich, Live-Preise über 200+ Modelle |

## Wie dieses Repo sich abgrenzt

- Diese Repos liefern **Masse** (Workflows, Agentenbeispiele) oder
  **Rechtsvorlagen**. Dieses Repo liefert die **Einordnung für einen
  konkreten Kleinbetrieb**: Was kostet es wirklich, was spart es wirklich,
  wann geht es schief.
- Keine der gefundenen Sammlungen ist auf Deutsch, auf DACH-Recht oder auf
  Branchen wie Maschinenbau/Handwerk/Zulieferer zugeschnitten.
- Wo ein externes Projekt eine Aufgabe bereits gut löst (z. B.
  Kostenvergleich, fertiger n8n-Workflow), wird in den Anwendungsfällen
  darauf verwiesen, statt es hier zu duplizieren.
