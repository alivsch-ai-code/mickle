# Grundlagen: KI-Schulung für Mitarbeitende

Der Rest dieses Repositoriums verzichtet bewusst auf Grundlagenerklärungen
— wer einen [Anwendungsfall](../anwendungsfaelle/) liest, will eine Lösung,
keine Einführung. Dieser Ordner ist die ausdrückliche Ausnahme: eine
vollständige, in sich geschlossene KI-Schulung für Mitarbeitende, die
KI-gestützte Automatisierung im Betrieb bedienen, prüfen oder verantworten.

Stand: 2026-09-06. Kurze Sätze, Sie-Form, keine Marketingsprache — wie im
gesamten Repo.

## Für wen diese Schulung gedacht ist

- **Anwenderinnen und Anwender**, die täglich mit einem KI-Werkzeug
  arbeiten (Module 1–5 + Wissenscheck).
- **Führungskräfte**, die Ergebnisse freigeben oder ein Budget
  verantworten (Module 1–5 + Abschnitt "Führungskraft" in Modul 6).
- **IT- und Datenschutzverantwortliche**, die ein Werkzeug einführen oder
  betreiben (alle Module + Abschnitt "IT/Datenschutz" in Modul 6 +
  [`evaluation.md`](evaluation.md)).

Diese Schulung ersetzt keine Kosten-Nutzen-Betrachtung (dafür:
[`wirtschaftlichkeit/`](../wirtschaftlichkeit/)) und keine Rechtsberatung
(dafür: [`recht/`](../recht/)). Sie vermittelt das Wissen, das eine Person
braucht, um mit einem KI-Werkzeug sicher zu arbeiten und zu erkennen, wann
sie eine andere Stelle im Betrieb einschalten muss.

## Module

| # | Modul | Dauer | Datei |
| - | --- | --- | --- |
| 1 | Grundbegriffe: LLM, Token, RAG, Agent | ca. 30 Min. | [`01-grundbegriffe.md`](01-grundbegriffe.md) |
| 2 | Prompting in der Praxis | ca. 45 Min. | [`02-prompting.md`](02-prompting.md) |
| 3 | Grenzen und Risiken | ca. 30 Min. | [`03-grenzen-und-risiken.md`](03-grenzen-und-risiken.md) |
| 4 | Datenschutz und Recht in Kürze | ca. 20 Min. | [`04-datenschutz-und-recht-in-kuerze.md`](04-datenschutz-und-recht-in-kuerze.md) |
| 5 | Werkzeuge im Unternehmen | ca. 20 Min. | [`05-werkzeuge-im-unternehmen.md`](05-werkzeuge-im-unternehmen.md) |
| 6 | Vertiefung nach Rolle | ca. 15–30 Min. | [`06-rollen-vertiefung.md`](06-rollen-vertiefung.md) |
| — | Wissenscheck (Selbsttest, 15 Fragen) | ca. 15 Min. | [`wissenscheck.md`](wissenscheck.md) |

Gesamtdauer für Module 1–6 plus Wissenscheck: ca. 3 bis 3,5 Stunden — passt
als Selbststudium in zwei Sitzungen oder als Rahmen für einen
Halbtags-Workshop (siehe [`schulungsleitfaden.md`](schulungsleitfaden.md)).

Wer die Schulung nur als Selbststudium bearbeitet, sollte Module der Reihe
nach lesen: Modul 2 baut auf Modul 1 auf, Modul 3 setzt Modul 2 voraus.
Modul 6 ist rollenspezifisch und muss nicht vollständig gelesen werden —
nur der jeweils passende Abschnitt.

## Wie diese Schulung im Betrieb eingesetzt wird

- **Selbststudium:** Module 1–6 der Reihe nach lesen, Wissenscheck am Ende
  allein bearbeiten. Geeignet für einzelne neue Mitarbeitende.
- **Präsenz- oder Video-Workshop:** Ablauf, Agenda mit Zeiten, benötigte
  Übungen und eine Teilnahmebestätigung-Vorlage stehen in
  [`schulungsleitfaden.md`](schulungsleitfaden.md). Geeignet, wenn mehrere
  Personen gleichzeitig geschult werden oder ein Werkzeug neu eingeführt
  wird.
- **Auffrischung:** Wiederholen Sie mindestens Modul 3 und Modul 4, wenn
  ein neues Werkzeug eingeführt wird, sich die Rechtslage ändert (siehe
  Datumsangaben in [`recht/`](../recht/)) oder nach einem
  Sicherheitsvorfall. Empfehlung für eine turnusmäßige Auffrischung:
  jährlich.

## Übungsmaterial

Prompt-Vorlagen für die Übungen in Modul 2 liegen in
[`vorlagen/schulung-prompting-uebungen.md`](../vorlagen/schulung-prompting-uebungen.md).

## Nach der Schulung: technische Vertiefung

[`evaluation.md`](evaluation.md) vertieft, wie ein KI-System vor dem
Pilotbetrieb gemessen und danach überwacht wird — das ist Aufgabe der
IT-/Datenschutzverantwortlichen (Modul 6), nicht Teil der
Basis-Anwenderschulung.

## Weiterführend

Wissenschaftliche Studien und technische Frameworks zu den hier
angerissenen Themen: [`quellen/README.md`](../quellen/README.md).
Kosten- und Rechtsfragen vertiefend: [`wirtschaftlichkeit/`](../wirtschaftlichkeit/)
und [`recht/`](../recht/). Technische Sicherheitskontrollen:
[`sicherheit/`](../sicherheit/).
