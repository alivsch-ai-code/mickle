# Übungsprompts: Prompting-Schulung (Modul 2)

Fünf Übungen für [`grundlagen/02-prompting.md`](../grundlagen/02-prompting.md)
und den [Schulungsleitfaden](../grundlagen/schulungsleitfaden.md). Alle
Daten sind erfunden (Muster Metallbau GmbH) — verwenden Sie beim Üben keine
echten Kunden- oder Personaldaten, auch nicht anonymisiert.

Getestet mit: nicht modellspezifisch verifiziert. Diese Prompts sind
Übungsvorlagen zum Erlernen der vier Grundprinzipien aus
[Modul 2](../grundlagen/02-prompting.md#die-vier-grundprinzipien), keine
produktiv freigegebenen Prompts. Vor Verwendung im Betrieb mit dem dort
freigegebenen Werkzeug prüfen (siehe
[`grundlagen/05-werkzeuge-im-unternehmen.md`](../grundlagen/05-werkzeuge-im-unternehmen.md)).

## Übung 1: Kundenanfrage zusammenfassen

Ausgangslage: eine unstrukturierte Kundenanfrage per E-Mail.

**Aufgabe:** Schreiben Sie einen Prompt, der aus der Anfrage eine
Zusammenfassung mit den Feldern Kunde, gewünschte Leistung, Menge,
Wunschtermin und offenen Rückfragen erstellt. Fehlende Angaben sollen als
"fehlt" markiert werden, nicht erfunden.

**Musterlösungsansatz:** siehe Vorher/Nachher-Beispiel in
[Modul 2](../grundlagen/02-prompting.md#vorhernachher-an-einem-beispiel).

## Übung 2: Rollenprompt für eine technische Rückfrage

Ausgangslage: Ein Kunde fragt, ob ein bestimmtes Stahlprofil für eine
Außenanwendung geeignet ist.

**Aufgabe:** Formulieren Sie einen Rollenprompt, der eine technisch
präzise, nicht werbliche Antwort verlangt, und der ausdrücklich anweist,
bei fehlender technischer Sicherheit auf eine Rückfrage bei der
Fachabteilung zu verweisen statt zu raten.

**Worauf zu achten ist:** Der Prompt muss die Grenze zwischen "Entwurf für
eine fachliche Prüfung" und "fertige technische Auskunft" klar machen —
siehe [Modul 3, Halluzination](../grundlagen/03-grenzen-und-risiken.md#1-halluzination).

## Übung 3: Angebotstext aus Stichpunkten

Ausgangslage: Ein Vertriebsmitarbeiter hat Stichpunkte zu Leistung, Menge
und Preis, aber noch keinen zusammenhängenden Angebotstext.

**Aufgabe:** Schreiben Sie einen Prompt mit Formatvorgabe (Anrede,
maximal 150 Wörter, ein Absatz mit Leistungsbeschreibung, eine Tabelle mit
Positionen) und einem Beispiel für den gewünschten Ton.

**Worauf zu achten ist:** Ein Beispiel für die gewünschte Ausgabe
(Prinzip 4) macht hier den größten Unterschied — ohne Beispiel variiert
der Ton stark zwischen Durchläufen (siehe
[Nicht-Determinismus](../grundlagen/03-grenzen-und-risiken.md#4-nicht-determinismus)).

## Übung 4: E-Mail-Postfach priorisieren

Ausgangslage: zehn kurze, erfundene E-Mail-Betreffzeilen mit
unterschiedlicher Dringlichkeit.

**Aufgabe:** Formulieren Sie einen Prompt, der die E-Mails nach
Dringlichkeit ordnet und für jede eine Ein-Satz-Begründung liefert.
Ergänzen Sie eine Anweisung, wie das Modell mit einer E-Mail umgehen soll,
die eine ungewöhnliche oder verdächtige Aufforderung enthält (z. B. eine
dringende Zahlungsaufforderung von einer unbekannten Adresse).

**Worauf zu achten ist:** Diese Übung verbindet Prompting mit
[Prompt Injection](../grundlagen/03-grenzen-und-risiken.md#2-prompt-injection)
— der Prompt sollte verlangen, solche E-Mails zu kennzeichnen, nicht
automatisch zu beantworten.

## Übung 5: Iteratives Nachbessern

Ausgangslage: Übung 3 wurde bereits bearbeitet.

**Aufgabe:** Ohne den ursprünglichen Prompt neu zu schreiben, bessern Sie
das Ergebnis in zwei Schritten gezielt nach: (1) "Kürzer, maximal 80
Wörter", (2) "Ohne Anrede, direkt mit der Leistungsbeschreibung
beginnen." Vergleichen Sie den Aufwand mit einem kompletten Neuschreiben
des Prompts.

**Worauf zu achten ist:** Zeigt das iterative Vorgehen aus
[Modul 2](../grundlagen/02-prompting.md#iteratives-vorgehen) in der
Praxis.

## Nach der Übung

Bewährte, im Betrieb tatsächlich genutzte Prompts gehören als eigene
Datei in diesen Ordner (`vorlagen/`) — thematisch benannt, mit kurzer
Beschreibung und dem Werkzeug/Modell, mit dem sie getestet wurden. Siehe
[`CONTRIBUTING.md`](../CONTRIBUTING.md#prompts-und-workflows).
