# [Name des Anwendungsfalls]

> Kopieren Sie diese Datei in einen neuen Ordner unter `anwendungsfaelle/`,
> benannt nach dem Problem (z. B. `anwendungsfaelle/angebotserstellung/`).
> Alle Beispiele beziehen sich auf die fiktive Muster Metallbau GmbH,
> 85 Mitarbeiter. Löschen Sie diesen Hinweisblock vor der Veröffentlichung.

## 1. Ausgangslage

- Wer im Betrieb hat dieses Problem (Rolle/Abteilung)?
- Wie oft tritt es auf (pro Tag/Woche/Monat)?
- Wie viel Zeit kostet es heute, konkret vorgerechnet
  (z. B. "X Vorgänge/Woche × Y Minuten = Z Stunden/Woche")?
- Womit wird es heute gelöst (Excel, Zuruf, Papier, keine Lösung)?

## 2. Lösungsansatz

- Was genau wird automatisiert (Schritt X bis Y im Ablauf)?
- Was bleibt bewusst manuell — und warum?
- Welche Rolle prüft das Ergebnis, bevor es wirksam wird?

## 3. Umsetzung

- Schritt-für-Schritt-Anleitung.
- Prompt(s): Verweis auf Datei in `vorlagen/` oder Inline-Codeblock.
- Workflow-Datei: Verweis auf Datei in `workflows/`, falls zutreffend.
- Benötigte Zugänge/Konten (z. B. E-Mail-Postfach, API-Schlüssel).
- Geschätzte Einrichtungszeit.

## 4. Kosten

- Token-/API-Kosten pro Vorgang (Rechnung offenlegen, Modell nennen; wenn
  Preis nicht sicher bekannt: `[PRÜFEN]` statt schätzen).
- Einmaliger Einrichtungsaufwand (Stunden × internem oder externem
  Stundensatz, Stundensatz als Annahme kennzeichnen).
- Laufende Kosten (Abo, Wartung, Anpassung bei Änderungen).

## 5. Nutzen

- Geschätzte Zeitersparnis pro Vorgang und pro Monat, als Rechnung:
  "vorher Z Minuten, nachher Z' Minuten, × Häufigkeit = Ersparnis/Monat".
- Ab wann amortisiert sich der Einrichtungsaufwand (Monat X)?
- Keine behaupteten Prozentzahlen ohne zugrundeliegende Rechnung.

## 6. Grenzen

- Mindestens drei konkrete Fehlerquellen, mit Beispiel.
- Wann funktioniert der Ansatz NICHT (z. B. Sonderfälle, Ausnahmen,
  unklare Eingabedaten)?
- Wo muss ein Mensch das Ergebnis zwingend prüfen, bevor es nach außen
  geht oder eine Wirkung entfaltet?

## 7. Datenschutz

- Welche Daten verlassen das Haus (Art der Daten, z. B. Kundennamen,
  Preise, Konstruktionsdaten)?
- Welcher Anbieter verarbeitet sie, mit Sitz/Serverstandort?
- Ist ein Auftragsverarbeitungsvertrag (AVV) nötig und vorhanden?
- Gilt eine Kennzeichnungspflicht nach Art. 50 EU AI Act (z. B. bei
  Kundenkontakt per Chatbot)?
- Welche lokale/offene Alternative bleibt im Haus (z. B. Ollama mit einem
  offenen Modell), falls Daten das Haus nicht verlassen dürfen?
