# Grundlagen: Schulungsmodul für Mitarbeitende

Der Rest dieses Repositoriums verzichtet bewusst auf Grundlagenerklärungen
— wer einen [Anwendungsfall](../anwendungsfaelle/) liest, will eine Lösung,
keine Einführung. Dieser Ordner ist die ausdrückliche Ausnahme: ein
Schulungsmodul für Mitarbeitende, die KI-gestützte Automatisierung im
Betrieb tatsächlich bedienen, prüfen und verantworten sollen. Zielgruppe
ist damit nicht die Geschäftsführung (die will Kosten/Nutzen, siehe
[`wirtschaftlichkeit/`](../wirtschaftlichkeit/)), sondern die Person, die
morgen den Prompt anpasst oder das Ergebnis freigibt.

Stand: 2026-09-06. Kurze Sätze, Sie-Form, keine Marketingsprache — wie im
gesamten Repo.

## Lernpfad (drei Einheiten, je 30–45 Minuten)

| Einheit | Inhalt | Material |
|---|---|---|
| 1 | Grundbegriffe: LLM, Prompt, Token, Halluzination | dieser Ordner, Abschnitte 1–2 |
| 2 | Prompting in der Praxis, mit echten Vorlagen | Abschnitt 3 + [`vorlagen/`](../vorlagen/) |
| 3 | Grenzen, Fehlerquellen, Datenschutz, Freigabepflicht | Abschnitt 4–6 + [`recht/`](../recht/) |

## 1. Was ein Sprachmodell (LLM) tut — und was nicht

Ein Large Language Model (LLM, z. B. GPT-, Claude- oder Mistral-Modelle)
sagt auf Basis von Trainingsdaten das statistisch wahrscheinlichste
nächste Wort voraus, wieder und wieder, bis eine vollständige Antwort
entsteht. Daraus folgt unmittelbar:

- Es **versteht** eine Anfrage nicht im menschlichen Sinn, es setzt Muster
  fort, die in ähnlichem Zusammenhang gelernt wurden.
- Es kennt keine Fakten außerhalb seiner Trainingsdaten und ohne
  zusätzliche Werkzeuge (siehe RAG, Abschnitt 2) auch keine aktuellen
  betriebsinternen Informationen.
- Es kann **selbstbewusst Falsches** produzieren ("Halluzination") — ein
  falsches Datum, eine erfundene Norm, eine nicht existierende Telefonnummer
  wirken sprachlich genauso sicher wie eine korrekte Angabe. Wie stark das
  je nach Aufgabe ins Gewicht fällt, unterscheidet sich deutlich nach
  Modell und Aufgabentyp (siehe Studienübersicht in
  [`quellen/README.md`](../quellen/README.md#wissenschaftliche-studien)).
- Die gleiche Eingabe kann bei zwei Durchläufen unterschiedliche Ausgaben
  liefern (Nicht-Determinismus) — wichtig für alles, was reproduzierbar
  sein muss (z. B. Buchhaltung).

## 2. RAG (Retrieval-Augmented Generation)

RAG bedeutet: Bevor das Modell antwortet, werden passende Ausschnitte aus
einer eigenen Dokumentensammlung (z. B. Firmenwiki, Handbücher,
Auftragshistorie) automatisch gesucht und dem Modell als Kontext
mitgegeben. So kann ein Modell auch zu Inhalten antworten, die es nie
"gelernt" hat.

- **Löst:** das Problem fehlenden betriebsinternen Wissens, ohne ein
  eigenes Modell trainieren zu müssen.
- **Löst nicht:** Halluzination vollständig — das Modell kann den
  gefundenen Kontext trotzdem falsch wiedergeben oder ergänzen. Siehe dazu
  die Studie zu Halluzinationsraten bei dokumentenbasierten Abfragen in
  [`quellen/README.md`](../quellen/README.md#wissenschaftliche-studien).
- Relevant für den Backlog-Anwendungsfall "interne Wissenssuche über
  Firmendokumente" in der Haupt-[README](../README.md).
- Technische Umsetzung typischerweise über Frameworks wie LlamaIndex oder
  Haystack, siehe [`quellen/README.md`](../quellen/README.md#etablierte-open-source-frameworks-für-eigene-technische-umsetzung).

## 3. Prompting: die vier Grundprinzipien

1. **Rolle und Ziel benennen** ("Sie sind ... Ihre Aufgabe ist ...").
2. **Kontext mitgeben**, statt Wissen vorauszusetzen (den Text, die Daten,
   das Beispiel direkt in den Prompt einfügen).
3. **Format vorgeben** (Stichpunkte, Tabelle, feste Länge) — spart Zeit
   beim Nachbearbeiten.
4. **Ein Beispiel für die gewünschte Ausgabe** liefern, wenn das Format
   ungewöhnlich ist.

Fertige, getestete Prompts für konkrete Aufgaben: siehe
[`vorlagen/`](../vorlagen/).

## 4. Begriffe, die im Alltag oft vermischt werden

| Begriff | Bedeutung |
|---|---|
| Chatbot | Konversationelle Oberfläche zu einem LLM, meist ohne eigene Handlungsfähigkeit |
| Workflow (n8n/Make) | Fest programmierte Schrittfolge; KI ist nur ein Baustein darin |
| KI-Agent | System, das selbst entscheidet, welche Werkzeuge/Schritte als Nächstes nötig sind, statt einer festen Schrittfolge zu folgen — dadurch flexibler, aber schwerer vorhersehbar |
| RAG | siehe Abschnitt 2 — Wissensanbindung, kein eigenständiger Systemtyp |

## 5. Typische Fehlerquellen auf einen Blick

- **Halluzination** — siehe Abschnitt 1.
- **Prompt Injection** — manipulierte Eingaben aus externen Quellen
  (E-Mails, Dokumente) können das Modell zu ungewollten Handlungen
  verleiten. Details: [`recht/README.md`](../recht/README.md#4-technisches-risiko-manipulierte-eingaben-prompt-injection).
- **Veraltetes oder falsches Wissen** ohne RAG-Anbindung.
- **Bias**: Trainingsdaten enthalten gesellschaftliche Verzerrungen, die
  das Modell reproduzieren kann — besonders relevant bei allem, was mit
  Personenbewertung zu tun hat (siehe Hochrisiko-Hinweis in
  [`recht/README.md`](../recht/README.md#3-eu-ai-act--hochrisiko-anwendungen-anhang-iii)).

## 6. Bevor ein Ergebnis verwendet wird

Jeder Anwendungsfall in diesem Repo benennt unter Punkt 6 ("Grenzen"),
welche Rolle das Ergebnis vor Wirksamwerden prüfen muss. Als Faustregel
für Mitarbeitende: Ein KI-generiertes Ergebnis ist ein **Entwurf**, keine
Entscheidung — bis eine dafür verantwortliche Person es freigegeben hat.

## Weiterführend

Wissenschaftliche Studien und technische Frameworks zu den hier
angerissenen Themen: [`quellen/README.md`](../quellen/README.md).
Kosten- und Rechtsfragen vertiefend: [`wirtschaftlichkeit/`](../wirtschaftlichkeit/)
und [`recht/`](../recht/).
