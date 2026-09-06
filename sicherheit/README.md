# Sicherheit für LLM-Automatisierung

Diese Checkliste ist technische Orientierung für die Muster Metallbau GmbH,
keine Sicherheitszertifizierung und keine Rechtsberatung. Sie ergänzt die
Hinweise in [`recht/`](../recht/) und muss je Anwendung konkret ausgefüllt
werden.

## 1. Bedrohungsmodell

Prüfen Sie mindestens diese Angriffs- und Fehlerklassen:

- **Prompt Injection:** Externe E-Mails, Dokumente oder Webseiten enthalten
  Anweisungen, die nicht als Daten behandelt werden.
- **Sensitive Information Disclosure:** Das System gibt interne Dokumente,
  Prompts, Zugangsdaten oder personenbezogene Daten an falsche Nutzer aus.
- **Insecure Output Handling:** Modelloutput wird ungeprüft als SQL, HTML,
  Shell-Befehl, E-Mail oder ERP-Eingabe ausgeführt.
- **Excessive Agency:** Ein Agent besitzt mehr Werkzeuge oder Rechte als für
  seine Aufgabe erforderlich.
- **RAG-/Embedding-Schwächen:** Falsche, veraltete oder unberechtigte
  Dokumente werden abgerufen; Metadatenfilter werden umgangen.
- **Unbounded Consumption:** Schleifen, große Dateien oder lange Kontexte
  erzeugen unkontrollierte Kosten oder blockieren den Dienst.

Diese Kategorien sind mit dem [OWASP GenAI LLM Top 10
2025](https://github.com/GenAI-Security-Project/GenAI-LLM-Top10/tree/main/2025)
abzugleichen. Die frühere OWASP-2023-Fassung ist [archiviert](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/tab_archive.md).

## 2. Mindestkontrollen

| Kontrolle         | Mindestanforderung                                                                           |
| ----------------- | -------------------------------------------------------------------------------------------- |
| Rechte            | Servicekonto mit kleinstmöglichen Rechten; Dokumente und Tools nach Rolle trennen.           |
| Tools             | Allowlist statt freier Toolwahl; Schreib-, Versand- und Zahlungsaktionen gesondert schützen. |
| Freigabe          | Menschliche Freigabe vor irreversiblen Aktionen oder Außenkommunikation.                     |
| Eingaben          | Dateien, URLs und E-Mails als untrusted data behandeln; Inhalt und Anweisung trennen.        |
| Ausgaben          | Schema validieren, HTML/SQL/Shell escapen und nie ungeprüft ausführen.                       |
| Secrets           | Keine Schlüssel in Prompts, Logs, Workflows oder Git; Secret Manager verwenden.              |
| Netzwerk          | Egress begrenzen; interne Dienste nicht über frei wählbare URLs erreichbar machen.           |
| Protokollierung   | Entscheidung, Tool, Nutzer, Quelle, Freigabe und Fehler protokollieren; Inhalte minimieren.  |
| Limits            | Maximalgröße, Laufzeit, Toolschritte, Tokens und Kosten je Vorgang begrenzen.                |
| Updates           | Abhängigkeiten, Container und Modelle versionieren; Sicherheitsmeldungen prüfen.             |
| Wiederherstellung | Backups verschlüsseln, Löschung testen und Wiederanlauf dokumentieren.                       |

## 3. RAG-spezifisch

- Berechtigungen bereits beim Retrieval filtern, nicht erst im Prompt.
- Dokumentquelle, Version, Gültigkeitszeitraum und Zugriffsgruppe als Metadaten
  speichern.
- Bei fehlender oder widersprüchlicher Quelle mit „nicht gefunden“ abbrechen.
- Gelöschte Dokumente auch aus Index, Cache, Embeddings und Backups entfernen.
- Quellenabschnitt und verwendete Dokument-IDs in der Antwort oder im Auditlog
  erhalten.

## 4. Pilotfreigabe

Ein Pilot ist erst freigabefähig, wenn ein Testset, eine benannte fachliche
Verantwortung, ein Abschaltweg, ein Datenflussdiagramm und ein dokumentierter
Rollback vorhanden sind. Externe Eingaben dürfen im Pilot keine Zahlung,
Bestellung, Vertragsänderung oder automatische Entscheidung über eine Person
auslösen.
