# KI-Automatisierung für den Mittelstand

Lizenz: Code MIT, Texte CC BY 4.0 · Stand: 2026-09-06

Dieses Repository sammelt sofort einsetzbare Lösungen für KI-Automatisierung in
kleinen und mittleren Unternehmen im deutschsprachigen Raum. Kein Lehrbuch,
keine Grundlagenerklärungen — für jedes Problem: Ausgangslage, Umsetzung,
Kosten, Nutzen, Grenzen und Datenschutz, jeweils mit nachvollziehbarer
Rechnung statt behaupteter Prozentzahlen.

## Zielgruppe

Geschäftsführer, Abteilungsleiter und IT-Verantwortliche in Maschinenbau,
Zulieferbetrieben, Ingenieurbüros, Logistik und Handwerk. Betriebe mit
10 bis 500 Mitarbeitern, ohne Data-Science-Team und ohne sechsstelliges
Budget.

## Ausgangslage

Nach der ifo-Unternehmensbefragung nutzten im Mai 2026 rund 54,5 % der
deutschen Unternehmen KI in irgendeiner Form, gegenüber 40,9 % ein Jahr
zuvor — bei kleinen und mittleren Unternehmen deutlich langsamer als bei
Großunternehmen. Der Bitkom-Studienbericht 2026 kommt mit 41 % aktiver
Nutzung auf eine andere Zahl; beide Erhebungen sind wegen unterschiedlicher
Stichproben und Definitionen nicht direkt vergleichbar, zeigen aber
übereinstimmend: Größere Unternehmen setzen KI häufiger ein als
kleinere, und Rechtsunsicherheit sowie fehlendes Know-how sind die am
häufigsten genannten Hemmnisse im Mittelstand. Quellen und Einordnung:
[`quellen/README.md`](quellen/README.md#wissenschaftliche-studien).

## Nutzungshinweis

- Alle Beispiele beziehen sich auf eine erfundene Firma: **Muster Metallbau
  GmbH, 85 Mitarbeiter**. Jede Ähnlichkeit mit realen Unternehmen, Dokumenten
  oder Prozessen ist Zufall.
- Rechtliche Aussagen (Ordner [`recht/`](recht/)) sind Orientierung, keine
  Rechtsberatung. Sie sind mit Datum versehen, weil sich die Rechtslage
  ändert — insbesondere die Transparenzpflichten nach Art. 50 EU AI Act, die
  seit dem 2. August 2026 gelten.
- Preise und Modellnamen sind, wo nicht sicher verifizierbar, mit
  `[PRÜFEN]` markiert statt geraten. Prüfen Sie Preise vor einer
  Entscheidung immer beim Anbieter selbst.
- Jeder Anwendungsfall folgt dem Schema in
  [`anwendungsfaelle/VORLAGE.md`](anwendungsfaelle/VORLAGE.md) und nennt
  mindestens drei konkrete Fehlerquellen.

## Struktur

| Ordner                                                 | Inhalt                                                                                 |
| ------------------------------------------------------ | -------------------------------------------------------------------------------------- |
| [`grundlagen/`](grundlagen/)                           | Schulungsmodul für Mitarbeitende: LLM, RAG, Prompting, Fehlerquellen                   |
| [`anwendungsfaelle/`](anwendungsfaelle/)               | Ein Ordner pro Anwendungsfall, benannt nach dem Problem                                |
| [`vorlagen/`](vorlagen/)                               | Prompts zum Kopieren, thematisch sortiert                                              |
| [`workflows/`](workflows/)                             | Exportierte n8n-/Make-Szenarien als JSON                                               |
| [`werkzeuge/`](werkzeuge/)                             | Werkzeug- und Anbieterübersicht: Automatisierungsplattformen, LLM-APIs, lokale Modelle |
| [`recht/`](recht/)                                     | DSGVO, Auftragsverarbeitung, EU AI Act Art. 50                                         |
| [`sicherheit/`](sicherheit/)                           | Technische Sicherheitskontrollen für LLM, RAG und Agenten                              |
| [`wirtschaftlichkeit/`](wirtschaftlichkeit/)           | Kostenmodelle, ROI-Rechnung, Anbietervergleich                                         |
| [`grundlagen/evaluation.md`](grundlagen/evaluation.md) | Testsets, Messgrößen und Regressionstests für LLM-Anwendungen                          |
| [`quellen/`](quellen/)                                 | Verwandte externe Projekte (Workflow-Sammlungen, Compliance-Vorlagen, Kostenrechner)   |

Für die Nutzung dieses Repos als Wissensbasis durch einen KI-Assistenten
(nicht nur als Nachschlagewerk für Menschen) siehe [`AGENTS.md`](AGENTS.md).

## Geplante Anwendungsfälle

Sortiert danach, wie schnell sie einem Kleinbetrieb Geld sparen: niedriger
Einrichtungsaufwand und hohe Wiederholungsfrequenz zuerst. Diese Reihenfolge
entstand aus einer Recherche vergleichbarer Praxisberichte und
Open-Source-Sammlungen (u. a. n8n-Workflow-Bibliotheken und
Branchenleitfäden für Handwerk und Maschinenbau) sowie eigener Einschätzung
der Zielbranchen — nicht aus Anbieterversprechen.

| #   | Anwendungsfall                                                                        | Branche(n)               | Einrichtungsaufwand | Status    |
| --- | ------------------------------------------------------------------------------------- | ------------------------ | ------------------- | --------- |
| 1   | Angebotserstellung aus Kundenanfragen                                                 | Handwerk, Zulieferer     | niedrig (Stunden)   | Vorschlag |
| 2   | Tägliche E-Mail-Postfach-Zusammenfassung und Priorisierung                            | alle                     | niedrig             | Vorschlag |
| 3   | Automatische Beantwortung von Standard-Kundenanfragen (Auftragsstatus, Liefertermine) | alle, bes. Logistik      | mittel              | Vorschlag |
| 4   | Belegerfassung und Buchhaltungsvorbereitung (Rechnungen, Lieferscheine)               | alle                     | mittel              | Vorschlag |
| 5   | Vorbereitung von Zahlungserinnerungen (Mahnwesen)                                     | alle                     | niedrig             | Vorschlag |
| 6   | Meeting- und Baustellenprotokolle aus Audioaufnahmen                                  | Handwerk, Ingenieurbüro  | mittel              | Vorschlag |
| 7   | Wartungsberichte und technische Kurzdokumentation                                     | Maschinenbau, Zulieferer | mittel              | Vorschlag |
| 8   | Übersetzung technischer Dokumente und Kundenkorrespondenz                             | Zulieferer, Maschinenbau | niedrig             | Vorschlag |
| 9   | Lieferanten- und Preisanfragen bündeln und vergleichen                                | Einkauf, Logistik        | mittel              | Vorschlag |
| 10  | Vertriebs- und Angebotstexte für Marketing                                            | alle                     | niedrig             | Vorschlag |

Warten auf Auswahl, bevor Inhalte für einzelne Fälle entstehen.

### Weitere Kandidaten (Backlog, ungeprüft)

Aus der Recherche zusätzlich gesammelt, noch nicht priorisiert:

- Wareneingangskontrolle per Bilderkennung (Qualitätsprüfung)
- Reklamations- und Rückrufmanagement: automatische Kategorisierung
- Interne Wissenssuche über Firmendokumente (RAG-Chatbot) — Achtung:
  Kennzeichnungspflicht nach Art. 50 EU AI Act bei Kundenkontakt
  ([`recht/`](recht/) beachten)
- Ersatzteil-Identifikation aus Fotos oder Beschreibungen
- Tourenplanung und Sendungsverfolgung (Logistik)
- Aufbereitung von Wartungsdaten für vorausschauende Instandhaltung
- Erstellung von Schulungsunterlagen aus bestehender Dokumentation
- Recherche-Unterstützung bei Normen und Richtlinien (mit Prüfpflicht durch
  Fachpersonal)
- Formulierung von Stellenanzeigen (ausdrücklich **kein** automatisiertes
  Bewerber-Scoring — das gilt nach EU AI Act als Hochrisiko-Anwendung)

## Mitmachen

Siehe [`CONTRIBUTING.md`](CONTRIBUTING.md).

## Lizenz

Code: [MIT](LICENSE) · Texte und Dokumentation: [CC BY 4.0](LICENSE-DOCS)
