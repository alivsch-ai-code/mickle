# Mitmachen

Beiträge sind willkommen, wenn sie zum Zweck dieses Repos passen: sofort
benutzbare Lösungen für konkrete Abteilungsprobleme in kleinen und
mittleren Unternehmen, nicht allgemeine KI-Grundlagen.

## Regeln für neue Anwendungsfälle

- Verwenden Sie die Struktur aus
  [`anwendungsfaelle/VORLAGE.md`](anwendungsfaelle/VORLAGE.md), alle
  sieben Abschnitte vollständig.
- Alle Beispiele beziehen sich auf die fiktive Muster Metallbau GmbH,
  85 Mitarbeiter. Keine realen Firmen, Dokumente oder Prozesse — auch
  nicht anonymisiert.
- Nennen Sie mindestens drei konkrete Fehlerquellen im Abschnitt
  "Grenzen". Ein Anwendungsfall ohne ehrlichen Grenzen-Abschnitt wird
  nicht angenommen.
- Zeigen Sie jede Zeitersparnis als nachvollziehbare Rechnung, nie als
  behauptete Prozentzahl.
- Nennen Sie immer auch eine lokale/offene Alternative (z. B. Ollama),
  wenn der Hauptansatz einen Cloud-Anbieter nutzt.
- Keine erfundenen Preise oder Modellnamen. Wenn ein Preis nicht sicher
  bekannt ist, schreiben Sie `[PRÜFEN]` statt zu schätzen.
- Kurze Sätze, Sie-Form, keine Marketingsprache, keine Superlative, keine
  Emojis.

## Rechtliche Inhalte

Beiträge im Ordner `recht/` sind Orientierung, keine Rechtsberatung.
Nennen Sie bei jeder rechtlichen Aussage das Datum, auf das sie sich
bezieht.

## Prompts und Workflows

- Prompts gehören nach `vorlagen/`, thematisch sortiert, mit kurzer
  Beschreibung, wofür sie gedacht sind und mit welchem Modell sie
  getestet wurden.
- n8n-/Make-Exporte gehören nach `workflows/` als JSON, mit einem
  Verweis aus dem zugehörigen Anwendungsfall.

## Pull Requests

- Ein Anwendungsfall pro Pull Request.
- Beschreiben Sie kurz, welche Abteilung/welches Problem der Fall
  adressiert.
