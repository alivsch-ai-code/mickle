# Agentische Systeme: Muster, Governance, Grenzen

Technische Vertiefung für IT-/Entwicklungsverantwortliche, die über den
Einsatz eines KI-Agenten (siehe Definition in
[Modul 1, Abschnitt 5](01-grundbegriffe.md#5-begriffe-die-im-alltag-oft-vermischt-werden)
und "Agentic RAG" in [`rag-techniken.md`](rag-techniken.md#7-agentic-rag))
entscheiden oder einen bereits geplant haben. Kein Bestandteil der sechs
Basis-Module. Stand: 2026-09-06.

## 1. Von Retrieval zu Agenten

Drei Stufen, wie ein System an Informationen kommt, bevor es antwortet:

- **Classical RAG:** feste Suche vor jeder Antwort (siehe
  [Modul 1, Abschnitt 4](01-grundbegriffe.md#4-rag-retrieval-augmented-generation)).
- **Graph RAG:** Dokumente werden zusätzlich als Wissensgraph mit
  Entitäten und Beziehungen aufbereitet, damit auch Fragen beantwortet
  werden können, die eine reine Ähnlichkeitssuche nicht löst (z. B. "Wer
  hat mit wem an Projekt X gearbeitet?").
- **Agentic RAG:** ein Agent entscheidet selbst, ob, wann und wie oft er
  nachschlägt (siehe [`rag-techniken.md`, Abschnitt 7](rag-techniken.md#7-agentic-rag)).

Dazu kommen bei Agenten drei Arten von Gedächtnis: **Kurzzeitgedächtnis**
(der aktuelle Gesprächsverlauf, verschwindet nach der Sitzung),
**Langzeitgedächtnis** (dauerhaft gespeicherte Fakten über mehrere
Sitzungen hinweg) und **episodisches Gedächtnis** (Erinnerung an
konkrete, vergangene Abläufe, um daraus zu lernen). Je mehr Gedächtnis ein
System hat, desto mehr wird es zu einer eigenen, pflegebedürftigen
Datenbank — mit denselben Datenschutzfragen wie in
[Modul 4](04-datenschutz-und-recht-in-kuerze.md), wenn dort
personenbezogene Daten gespeichert werden.

Quelle Graph RAG: Edge et al. (2024), *"From Local to Global: A Graph RAG
Approach to Query-Focused Summarization"*, [arXiv:2404.16130](https://arxiv.org/abs/2404.16130).

## 2. Agenten-Muster

- **ReAct-Loop:** Das Modell wechselt sich ab zwischen Denken ("was ist
  der nächste Schritt?") und Handeln (ein Werkzeug aufrufen), beobachtet
  das Ergebnis und denkt erneut nach — die technische Grundform der
  meisten heutigen Agenten. Quelle: Yao et al. (2022), *"ReAct:
  Synergizing Reasoning and Acting in Language Models"*,
  [arXiv:2210.03629](https://arxiv.org/abs/2210.03629).
- **Planner → Executor:** Ein Modell erstellt zuerst einen vollständigen
  Plan, ein zweiter Schritt (Modell oder Code) führt ihn ab.
- **Tool-Auswahl und -Routing:** Bei mehreren verfügbaren Werkzeugen
  entscheidet das Modell, welches für die aktuelle Teilaufgabe passt.
- **Reflection/Selbstkritik:** Das Modell bewertet sein eigenes
  Zwischenergebnis und bessert nach, bevor es antwortet oder weitermacht.
  Quelle: Shinn et al. (2023), *"Reflexion: Language Agents with Verbal
  Reinforcement Learning"*, [arXiv:2303.11366](https://arxiv.org/abs/2303.11366).

Keines dieser Muster macht ein Ergebnis automatisch verlässlicher — sie
beschreiben, *wie* ein Agent vorgeht, nicht, *ob* das Ergebnis stimmt. Die
Prüfpflicht aus [Modul 3, Abschnitt 6](03-grenzen-und-risiken.md#6-die-faustregel-für-jedes-ergebnis)
gilt unverändert.

## 3. Multi-Agenten-Orchestrierung

Statt eines einzelnen Agenten koordiniert ein **Orchestrator** mehrere
spezialisierte Subagenten, die parallel an Teilaufgaben arbeiten: Der
Orchestrator nimmt das Ziel entgegen, zerlegt es in Teilaufgaben, verteilt
sie an passende Subagenten (z. B. Recherche, Analyse, Planung,
Ausführung, Prüfung), sammelt deren Ergebnisse ein und fasst sie zum
Endergebnis zusammen. Anthropic beschreibt dieses Muster in der eigenen
Praxis als "Orchestrator-Workers": Ein Leitagent entwickelt die Strategie
und delegiert an Subagenten, die unabhängig voneinander Informationen
sammeln und ihre Funde zur Synthese zurückgeben.

**Der entscheidende Kostenpunkt:** Laut Anthropics eigener Fallstudie
verbrauchen einzelne Agenten etwa das 4-Fache der Tokens einer normalen
Chat-Anfrage, Multi-Agenten-Systeme etwa das 15-Fache — weil jeder
Subagent ein eigener, bezahlter Modellaufruf ist. Das lohnt sich laut
Anthropic nur, wenn der Wert der Aufgabe die höheren Kosten rechtfertigt.
Für die Kostenrechnung nach
[`wirtschaftlichkeit/README.md`](../wirtschaftlichkeit/README.md)
bedeutet das: die Tokenmenge eines Multi-Agenten-Systems nicht wie eine
einzelne Anfrage schätzen, sondern separat und großzügiger ansetzen.

**Ausdrückliche Warnung aus derselben Quelle:** Bevor ein Multi-Agenten-System
aufgebaut wird, zuerst die einfachste Lösung versuchen — "meist reicht
die Optimierung einzelner Modellaufrufe mit Retrieval und Beispielen im
Kontext bereits aus". Zusätzliche Komplexität nur dann, wenn eine
einfachere Lösung nachweislich nicht ausreicht, und nur mit messbarem
Ergebnis, das den Mehraufwand rechtfertigt — dieselbe Grundhaltung wie
beim Fine-Tuning in [`llm-fine-tuning.md`](llm-fine-tuning.md).

**Beispielhafte Rollenaufteilung** (z. B. für eine komplexe Rechercheaufgabe):
Research-Agent (sammelt Informationen), Analysis-Agent (wertet aus),
Planning-Agent (erstellt Ablauf), Execution-Agent (führt über Werkzeuge
aus), Review-Agent (prüft das Ergebnis) — der Orchestrator verbindet
diese Rollen über eine gemeinsame Gedächtnisschicht und reicht das
Endergebnis weiter.

Quellen: [Anthropic, Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents);
[Anthropic, How We Built Our Multi-Agent Research System](https://www.anthropic.com/engineering/built-multi-agent-research-system).

## 4. Produktion und Governance

Begriffe, die in Anbieterbeschreibungen für "produktionsreife" Agenten
auftauchen — größtenteils bereits an anderer Stelle in diesem Kurs mit
konkreten Kontrollen hinterlegt, hier nur benannt und verortet:

| Begriff | Bedeutung | Bereits behandelt |
| --- | --- | --- |
| Confidence Scoring | Das Modell gibt zu einer Aussage eine Sicherheitseinschätzung mit aus | Ersetzt keine eigene Prüfung (siehe Halluzination, Modul 3) |
| Policy Gates | Feste Regeln, die eine Aktion vor Ausführung blockieren oder freigeben | [`sicherheit/README.md`, Mindestkontrollen](../sicherheit/README.md#2-mindestkontrollen) |
| Audit Trail Design | Nachvollziehbares Protokoll aller Entscheidungen und Werkzeugaufrufe | [`sicherheit/README.md`, Protokollierung](../sicherheit/README.md#2-mindestkontrollen) |
| Decision Reasoning Logs | Aufzeichnung, warum ein Agent eine bestimmte Entscheidung getroffen hat | siehe Audit Trail, dieselbe Kontrolle |
| Eval & Observability | Messung der Ergebnisqualität und Beobachtung des Systemverhaltens im Betrieb | [`evaluation.md`](evaluation.md) |
| Cost/Token Economics | Laufende Kosten pro Vorgang | [`wirtschaftlichkeit/README.md`](../wirtschaftlichkeit/README.md) |

Ohne diese Kontrollen ist ein Agent kein produktionsreifes System,
sondern ein Prototyp — unabhängig davon, wie ausgefeilt seine
Agenten-Muster (Abschnitt 2) sind.

## 5. Ausblick: mit Vorsicht zu lesende Begriffe

In Übersichten zu agentischen Systemen tauchen zunehmend Begriffe wie
"Memory & Learning Loops" (Agenten, die aus vergangenen Abläufen
dauerhaft lernen), "Self-Improving Agents", "Multi-Modal Reasoning über
mehrere Datentypen hinweg" oder "Agentic Workflows at Scale" auf. Das
sind Forschungs- und Frühphasen-Themen, keine für einen Mittelstandsbetrieb
etablierten, produktionsreifen Bausteine — Stand 2026-09-06 fehlen dafür
belastbare, unabhängige Praxisberichte in der für dieses Repo relevanten
Größenordnung. Bei einem Anbieter, der mit diesen Begriffen wirbt: nach
einer konkreten, überprüfbaren Fallstudie fragen statt die Begriffe als
Qualitätsnachweis zu werten.

## 6. Wenn Sie selbst entwickeln oder einen Dienstleister beurteilen

Für die Einstellung einer Entwicklerrolle oder die Bewertung eines
Dienstleisters für agentische Systeme werden in der Praxis häufig sechs
Kompetenzbereiche genannt: klassische Softwareentwicklung, Umgang mit
KI-Werkzeugen und Prompting, Produktverständnis (welches Problem löst
das System für wen), agentische/Multi-Agenten-Architektur (Abschnitte
2–3), Deployment und Monitoring (Abschnitt 4), sowie Kommunikation mit
fachlichen Stakeholdern. Als grobe Checkliste für ein Vorstellungsgespräch
oder eine Anbieterauswahl brauchbar — kein geprüftes Kompetenzmodell mit
Quellenbeleg, sondern eine in der Branche verbreitete Einordnung. Für
einen Betrieb ohne eigenes Data-Science-Team ist meist entscheidender,
ob eine Fachperson die Abschnitte 3 und 4 dieses Dokuments in der eigenen
Sprache erklären kann, als ob alle sechs Bereiche gleich stark ausgeprägt
sind.
