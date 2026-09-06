# Modul 4: Datenschutz und Recht in Kürze

Dieses Modul ist eine Kurzfassung für den Arbeitsalltag, keine
Rechtsberatung. Die ausführliche Fassung mit Datum und Quellen steht in
[`recht/README.md`](../recht/README.md) — bei einer konkreten Entscheidung
gilt diese, nicht die Kurzfassung hier. Stand: 2026-09-06.

Voraussetzung: [Modul 3](03-grenzen-und-risiken.md).

## 1. Was Sie nie in ein nicht freigegebenes Werkzeug eingeben

Bevor Sie einen Text, eine Tabelle oder ein Dokument in ein KI-Werkzeug
einfügen, prüfen Sie, ob es ein vom Betrieb freigegebenes Werkzeug ist
(siehe [Modul 5](05-werkzeuge-im-unternehmen.md)). In ein **nicht**
freigegebenes Werkzeug (z. B. ein privater Zugang zu einem
Cloud-Chatbot) gehören insbesondere nicht:

- Kunden- oder Mitarbeiternamen zusammen mit weiteren personenbezogenen
  Angaben (Adresse, Gehalt, Gesundheitsdaten, Bewerbungsunterlagen).
- Konstruktionsdaten, Stücklisten oder Preise mit Wettbewerbsrelevanz.
- Zugangsdaten, Schlüssel oder interne Vertragsinhalte.

Grund: Ohne geprüften Auftragsverarbeitungsvertrag (siehe Abschnitt 2) und
ohne bekannten Serverstandort ist unklar, wie und wo diese Daten
verarbeitet und gespeichert werden.

## 2. Auftragsverarbeitungsvertrag (AVV) — warum das wichtig ist

Sobald ein externer Dienst personenbezogene Daten in Ihrem Auftrag
verarbeitet, ist nach Art. 28 DSGVO ein Auftragsverarbeitungsvertrag
nötig. Das ist eine Vereinbarung zwischen dem Betrieb und dem Anbieter —
keine Einzelperson kann das für sich selbst abschließen. Deshalb gilt:
Ein KI-Werkzeug ist erst dann für personenbezogene Daten geeignet, wenn
die IT- oder Datenschutzverantwortung das freigegeben hat. Details:
[`recht/README.md#1-dsgvo--die-praktisch-relevanten-fragen`](../recht/README.md#1-dsgvo--die-praktisch-relevanten-fragen).

## 3. Kennzeichnungspflicht bei Kundenkontakt (EU AI Act, Art. 50)

Seit dem 2. August 2026 gilt: Ein Chatbot oder KI-Assistent, der mit
Kundinnen und Kunden kommuniziert, muss für sie erkennbar als KI
gekennzeichnet sein — spätestens bei der ersten Interaktion, in einfacher
Sprache. Wenn Sie an einem Anwendungsfall mit direktem Kundenkontakt
arbeiten (z. B. automatische Antwort auf eine Kundenanfrage), prüfen Sie,
ob diese Kennzeichnung eingebaut ist — das ist keine optionale
Höflichkeit, sondern seit diesem Datum verpflichtend. Details und
Bußgeldrahmen: [`recht/README.md#2-eu-ai-act--transparenzpflichten-nach-art-50`](../recht/README.md#2-eu-ai-act--transparenzpflichten-nach-art-50).

## 4. Automatisierte Bewertung von Personen ist tabu

Ein KI-Ergebnis darf nicht ohne wirksame menschliche Prüfung direkt in
eine Entscheidung über eine Person einfließen — etwa bei
Bewerbungsauswahl, Leistungsbeurteilung oder Kreditwürdigkeit. Solche
Einsatzzwecke gelten nach EU AI Act als Hochrisiko und unterliegen
deutlich strengeren Pflichten. Details:
[`recht/README.md#3-eu-ai-act--hochrisiko-anwendungen-anhang-iii`](../recht/README.md#3-eu-ai-act--hochrisiko-anwendungen-anhang-iii).

## 5. Im Zweifel

Fragen Sie vor der ersten Nutzung eines neuen Werkzeugs oder bei einer
neuen Art von Daten die IT- oder Datenschutzverantwortung im Betrieb, statt
selbst zu entscheiden. Das ist keine Verzögerung, sondern Teil der
Freigabepflicht aus [Modul 3, Abschnitt 6](03-grenzen-und-risiken.md#6-die-faustregel-für-jedes-ergebnis).

## Weiter mit Modul 5

[Modul 5: Werkzeuge im Unternehmen](05-werkzeuge-im-unternehmen.md).
