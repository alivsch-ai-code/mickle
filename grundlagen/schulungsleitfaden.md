# Schulungsleitfaden

Für Personen, die diese Schulung im Betrieb durchführen (typischerweise
HR, eine Führungskraft oder die IT-Verantwortung). Kein zusätzlicher
Modulinhalt, sondern die Anleitung, wie die Module 1–6 vermittelt werden.

## 1. Format wählen

| Situation | Empfohlenes Format |
| --- | --- |
| Einzelne neue Mitarbeitende | Selbststudium: Module 1–6 in eigenem Tempo, Wissenscheck allein |
| Mehrere Personen gleichzeitig, neues Werkzeug wird eingeführt | Halbtags-Workshop (Präsenz oder Video) mit gemeinsamer Übung |
| Auffrischung nach Vorfall oder Rechtsänderung | Nur die betroffenen Module erneut, siehe [`README.md`](README.md#wie-diese-schulung-im-betrieb-eingesetzt-wird) |

## 2. Agenda für einen Halbtags-Workshop (ca. 4 Stunden inkl. Pausen)

| Zeit | Inhalt | Material |
| --- | --- | --- |
| 0:00–0:30 | Modul 1: Grundbegriffe, gemeinsam besprechen | [`01-grundbegriffe.md`](01-grundbegriffe.md) |
| 0:30–1:15 | Modul 2: Prompting, danach Einzel- oder Partnerübung | [`02-prompting.md`](02-prompting.md), [`vorlagen/schulung-prompting-uebungen.md`](../vorlagen/schulung-prompting-uebungen.md) |
| 1:15–1:30 | Pause | — |
| 1:30–2:00 | Modul 3: Grenzen und Risiken, mit Diskussion eigener Beispiele aus dem Betrieb | [`03-grenzen-und-risiken.md`](03-grenzen-und-risiken.md) |
| 2:00–2:20 | Modul 4: Datenschutz und Recht in Kürze | [`04-datenschutz-und-recht-in-kuerze.md`](04-datenschutz-und-recht-in-kuerze.md) |
| 2:20–2:40 | Modul 5: Werkzeuge im Unternehmen — eigene Freigabeliste zeigen oder gemeinsam entwerfen | [`05-werkzeuge-im-unternehmen.md`](05-werkzeuge-im-unternehmen.md) |
| 2:40–2:55 | Pause | — |
| 2:55–3:15 | Modul 6: Rollenspezifische Gruppen (Anwender/Führungskraft/IT) getrennt besprechen | [`06-rollen-vertiefung.md`](06-rollen-vertiefung.md) |
| 3:15–3:45 | Wissenscheck, einzeln bearbeiten, danach gemeinsam auflösen | [`wissenscheck.md`](wissenscheck.md) |
| 3:45–4:00 | Fragen, Teilnahmebestätigung ausgeben | Abschnitt 4 unten |

Zeiten sind Richtwerte — bei einer erfahrenen Gruppe ist die Kurzfassung
(nur Module 1–4 + Wissenscheck, ca. 2,5 Stunden) ausreichend.

## 3. Übung in Modul 2 anleiten

Teilen Sie die Gruppe in Paare auf. Jedes Paar bearbeitet zwei der fünf
Übungen aus [`vorlagen/schulung-prompting-uebungen.md`](../vorlagen/schulung-prompting-uebungen.md)
mit dem im Betrieb freigegebenen Werkzeug (siehe
[Modul 5](05-werkzeuge-im-unternehmen.md)). Wichtig: keine echten Kunden-
oder Personaldaten verwenden, auch nicht anonymisiert zum Testen — dafür
sind die Übungen bewusst mit erfundenen Daten der Muster Metallbau GmbH
formuliert. Anschließend im Plenum zwei bis drei Ergebnisse vergleichen:
Was hat den Unterschied zwischen einem schwachen und einem guten Prompt
ausgemacht?

## 4. Teilnahme dokumentieren

Für den Nachweis, dass eine Schulung stattgefunden hat (relevant für die
Freigabepflicht aus [Modul 6](06-rollen-vertiefung.md#für-führungskräfte)
und für [`sicherheit/README.md#4-pilotfreigabe`](../sicherheit/README.md#4-pilotfreigabe)),
reicht eine einfache Liste:

```
Schulung "KI-Grundlagen" — Teilnahmebestätigung
Datum:
Format: [Selbststudium / Workshop]
Teilnehmende (Name, Rolle):
Bearbeitete Module:
Wissenscheck bestanden (ja/nein, Datum):
Bestätigt durch:
```

Diese Vorlage ist bewusst einfach gehalten — kein Zertifikat mit
Rechtswirkung, sondern ein interner Nachweis für die eigene
Dokumentationspflicht.

## 5. Wiederholung

Empfehlung: Module 3 und 4 jährlich auffrischen, sowie sofort bei
Einführung eines neuen Werkzeugs, einer wesentlichen Rechtsänderung (siehe
Datumsangaben in [`recht/README.md`](../recht/README.md)) oder nach einem
Sicherheitsvorfall. Eine vollständige Wiederholung aller sechs Module ist
dafür nicht nötig.
