# Modul 2: Prompting in der Praxis

Ziel dieses Moduls: Sie können einen Prompt so formulieren, dass er beim
ersten oder zweiten Versuch ein brauchbares Ergebnis liefert, statt mehrfach
grundlos nachzubessern.

Voraussetzung: [Modul 1](01-grundbegriffe.md).

## Die vier Grundprinzipien

1. **Rolle und Ziel benennen** ("Sie sind ... Ihre Aufgabe ist ...").
2. **Kontext mitgeben**, statt Wissen vorauszusetzen (den Text, die Daten,
   das Beispiel direkt in den Prompt einfügen — ein Modell kennt Ihre
   Auftragsnummer oder Ihren Kunden nicht von selbst, siehe
   [Modul 1, Abschnitt 1](01-grundbegriffe.md#1-was-ein-sprachmodell-llm-tut--und-was-nicht)).
3. **Format vorgeben** (Stichpunkte, Tabelle, feste Länge) — spart Zeit
   beim Nachbearbeiten.
4. **Ein Beispiel für die gewünschte Ausgabe** liefern, wenn das Format
   ungewöhnlich ist.

## Vorher/Nachher an einem Beispiel

Beispiel bei der fiktiven Muster Metallbau GmbH: Eine Mitarbeiterin im
Vertrieb soll aus einer Kundenanfrage eine kurze interne Zusammenfassung
für die Auftragserfassung erstellen.

**Schwacher Prompt** (verletzt alle vier Prinzipien):

> Fass das mal zusammen: [E-Mail-Text]

Ergebnis: Das Modell rät Länge, Zielgruppe und Format — meist ein zu langer
Fließtext, der noch einmal überarbeitet werden muss.

**Verbesserter Prompt:**

> Sie sind Assistenz in der Auftragserfassung der Muster Metallbau GmbH.
> Fassen Sie die folgende Kundenanfrage für die interne Weiterverarbeitung
> zusammen. Format: maximal 5 Stichpunkte mit den Feldern Kunde,
> gewünschte Leistung, Menge, Wunschtermin, offene Rückfragen. Wenn eine
> Angabe fehlt, schreiben Sie "fehlt" statt zu raten.
>
> Kundenanfrage: [E-Mail-Text]

Der Unterschied: Rolle und Ziel sind benannt (Prinzip 1), die Anfrage ist
als Kontext eingefügt (Prinzip 2), das Format ist vorgegeben (Prinzip 3),
und der letzte Satz verhindert, dass fehlende Angaben stillschweigend
erfunden werden — das nimmt die Halluzinationsgefahr aus
[Modul 3](03-grenzen-und-risiken.md) direkt im Prompt vorweg.

## Drei Techniken für schwierigere Aufgaben

| Technik | Wann einsetzen | Kurzbeispiel |
| --- | --- | --- |
| Rollenprompt | Der Ton oder die fachliche Perspektive der Antwort ist wichtig | "Sie sind Meister in der Schlosserei und antworten technisch präzise, nicht werblich." |
| Few-Shot (Beispiele mitgeben) | Das gewünschte Format ist ungewöhnlich oder firmenspezifisch | Zwei Beispiel-Angebotszeilen im gewünschten Format vor die eigentliche Aufgabe stellen |
| In Schritte zerlegen | Die Aufgabe hat mehrere Teilziele, die einzeln geprüft werden sollen | Erst "Liste alle Positionen der Anfrage auf", danach getrennt "Ordne jeder Position einen Preis zu" |

## Iteratives Vorgehen

Ein Prompt muss selten beim ersten Versuch perfekt sein. Praktikables
Vorgehen:

1. Ersten Entwurf mit den vier Grundprinzipien schreiben.
2. Ergebnis gegen die tatsächliche Aufgabe prüfen — fehlt etwas, ist der
   Ton falsch, ist das Format unbrauchbar?
3. Gezielt nachbessern ("Kürzer.", "Ohne Anrede.", "Nur die Positionen mit
   Preis, keine Erklärung.") statt den ganzen Prompt neu zu schreiben.
4. Bewährte Prompts sichern statt jedes Mal neu zu formulieren — dafür ist
   [`vorlagen/`](../vorlagen/) da.

## Was Prompting nicht löst

- Fehlendes betriebsinternes Wissen — dafür ist RAG nötig
  ([Modul 1, Abschnitt 4](01-grundbegriffe.md#4-rag-retrieval-augmented-generation)).
- Falsche oder erfundene Angaben, wenn der Prompt sie nicht ausdrücklich
  verbietet — siehe Beispiel oben und [Modul 3](03-grenzen-und-risiken.md).
- Manipulierte Inhalte aus externen Quellen (z. B. eine E-Mail, die
  versteckte Anweisungen an das Modell enthält) — siehe Prompt Injection
  in [Modul 3](03-grenzen-und-risiken.md).

## Übung

Fünf vorbereitete Übungsprompts mit Musterlösungsansatz für den
Selbstversuch oder den Workshop:
[`vorlagen/schulung-prompting-uebungen.md`](../vorlagen/schulung-prompting-uebungen.md).

## Weiter mit Modul 3

[Modul 3: Grenzen und Risiken](03-grenzen-und-risiken.md).
