# Webseite: KI-Handbuch Mittelstand

Eine einzelne, eigenständige HTML-Seite, die dieses Repository als
Nachschlagewerk zusammenfasst und eine interaktive KI-Auskunft enthält, die
nur auf Basis der Repo-Inhalte antwortet. Kein Build-Prozess, kein Server,
keine Abhängigkeiten außer zwei Google-Fonts-Links.

Veröffentlicht als Claude-Artifact:
<https://claude.ai/code/artifact/b5d02378-b21e-47ee-bdfb-970546d9d4dd>
(privat, bis über das Teilen-Menü der Seite freigegeben).

Stand: 2026-09-06.

## Was die Seite zeigt

Eine Zusammenfassung jedes Ordners in diesem Repo, als eine scrollbare
Seite mit Sprungmarken-Navigation ("Aktenreiter"):

| Abschnitt | Fasst zusammen |
| --- | --- |
| Ausgangslage | Nutzungszahlen (ifo, Bitkom) aus [`README.md`](../README.md) |
| Schulung | Die sechs Module aus [`grundlagen/`](../grundlagen/) |
| Anwendungsfälle | Die Backlog-Tabelle aus [`README.md`](../README.md#geplante-anwendungsfälle) |
| Werkzeuge | Auswahlhilfe aus [`werkzeuge/README.md`](../werkzeuge/README.md) |
| Recht & Sicherheit | Kernpunkte aus [`recht/README.md`](../recht/README.md) und [`sicherheit/README.md`](../sicherheit/README.md) |
| Wirtschaftlichkeit | Formeln und Studien aus [`wirtschaftlichkeit/README.md`](../wirtschaftlichkeit/README.md) |
| Quellen | Auswahl kuratierter Projekte aus [`quellen/README.md`](../quellen/README.md) |

Die Seite ist eine Momentaufnahme, kein Live-Spiegel: Inhalte sind von
Hand aus dem Repo-Stand vom 2026-09-06 kondensiert, nicht automatisch
generiert. Ändert sich ein Modul, eine Rechtsfrist oder eine Zahl im Repo,
muss die Seite manuell nachgezogen werden (Abschnitt "Aktualisieren"
unten).

## Fragebogen und Chat

Zwei getrennte Bausteine, umschaltbar über die Reiter im Kopf des
Assistenten-Kastens:

- **Fragebogen:** ein klassischer Klick-Fragebogen ohne KI — vier feste
  Fragen (Rolle, größtes Zeitproblem, Vertraulichkeit der Daten,
  Betriebsgröße) mit Antwortoptionen zum Anklicken, Fortschrittsbalken und
  Zurück-Navigation. Die Auswertung ist eine feste Zuordnungstabelle in
  JavaScript (`ROLLE_TEXT`, `PROBLEM_TEXT`, `VERTRAULICH_TEXT`,
  `GROESSE_TEXT`) und liefert vier Ergebniskacheln: passendes
  Schulungsmodul, passender Backlog-Anwendungsfall, Werkzeug-Ansatz,
  nächster Schritt. Funktioniert vollständig ohne KI-Aufruf. Optional lässt
  sich das Ergebnis über den Knopf "Mit KI ausformulieren" einmalig zu
  einem persönlichen Absatz erweitern (ein einzelner `sample()`-Aufruf mit
  den vier Antworten, kein Chatverlauf).
- **Chat:** ein Chat im Stil bekannter KI-Chat-Oberflächen — Avatar-Kreise,
  Sprechblase rechts für eigene Nachrichten, freier Fließtext links für
  Antworten, abgerundetes Eingabefeld mit Sende-Button, drei tanzende
  Punkte als Tippanzeige während Claude antwortet. Beispiel-Chips für
  häufige Fragen (Kennzeichnungspflicht, Kostenrechnung, Bewerber-Scoring,
  lokale Werkzeuge, Prompting vs. Fine-Tuning) helfen beim Einstieg.

Beide Bausteine, die die KI nutzen, teilen sich dieselbe Grundlage
(`script`-Block am Ende von [`index.html`](index.html)): eine feste
Kontext-Zeichenkette (`KB`) mit der kondensierten Wissensbasis wird bei
jedem Aufruf mitgeschickt — die `sample`-Fähigkeit hat kein Gedächtnis
zwischen Aufrufen, der Chat hängt seinen bisherigen Verlauf selbst wieder
an. Die Regeln in `KB` erzwingen dieselben Grundsätze wie
[`AGENTS.md`](../AGENTS.md): Sie-Form, keine erfundenen Preise, Zeitersparnis
nur als Rechnung, kein Bewerber-Scoring, lokale Alternative bei
Vertraulichkeit nennen, Rechtsaussagen nur als datierte Orientierung.

Kosten und Einwilligung: Jeder KI-Aufruf verbraucht das Claude-Guthaben der
besuchenden Person, nicht das des Betreibers. Der erste Aufruf fragt um
Erlaubnis; bei Ablehnung blendet die Seite Chat und "Mit KI ausformulieren"
dauerhaft aus (siehe `permanentlyHide()` in [`index.html`](index.html)).
Der Fragebogen selbst braucht dafür keine Erlaubnis und bleibt in jedem
Fall nutzbar, weil seine Auswertung ohne KI-Aufruf auskommt.

## Design

Gestaltet als technisches Datenblatt statt als Werbe-Landingpage — passend
zur Regel aus [`AGENTS.md`](../AGENTS.md), dass jede aus diesem Repo
gespeiste Antwort ohne Marketingsprache und Superlative auskommt. Der
Kopfbereich ist einem DIN-Schriftfeld nachempfunden (Benennung, Zielgruppe,
Stand, Lizenz, Blatt-Nummer), wie es auf technischen Zeichnungen steht —
naheliegend, weil die fiktive Referenzfirma des gesamten Repos ein
Metallbaubetrieb ist. Schriften: Titillium Web (Überschriften, Label —
Herkunft aus Straßenschrift-/DIN-Schriftfamilien), IBM Plex Sans
(Fließtext), IBM Plex Mono (Zahlen, Daten, Chat-Transkript). Hell-/Dunkelmodus
vollständig unterstützt.

## GitHub Pages

Zusätzlich zum Claude-Artifact wird die Seite über
[`.github/workflows/pages.yml`](../.github/workflows/pages.yml) automatisch
nach GitHub Pages veröffentlicht, sobald sich etwas in `webseite/` ändert
und der Commit nach `main` gepusht wird (offizielle Actions
`configure-pages` → `upload-pages-artifact` → `deploy-pages`, Quellordner
`webseite/`).

**Einmaliger manueller Schritt** (kann nicht per Git erledigt werden):
Im GitHub-Repository unter *Settings → Pages → Source* **"GitHub Actions"**
auswählen. Danach läuft jeder weitere Push automatisch. Die Seite ist dann
erreichbar unter `https://<benutzername>.github.io/<repo-name>/`.

**Wichtige Einschränkung auf GitHub Pages:** Die `sample`-Fähigkeit
(`window.claude`) existiert nur, wenn die Seite als Claude-Artifact
geöffnet wird — bei jeder anderen Adresse, also auch auf GitHub Pages, ist
`window.claude` gar nicht vorhanden. Das Skript erkennt das und blendet
**Chat** sowie den Knopf "Mit KI ausformulieren" automatisch dauerhaft aus
(`permanentlyHide()`); der **Fragebogen** funktioniert dort unverändert
vollständig, weil seine Auswertung ohne KI-Aufruf auskommt. Für die volle
Seite mit KI-Auskunft bleibt der Claude-Artifact-Link oben maßgeblich.

## Aktualisieren

1. [`index.html`](index.html) direkt bearbeiten (kein Build-Schritt).
2. Bei inhaltlichen Änderungen im Repo: den `KB`-Konstante im
   `<script>`-Block sowie die sichtbaren Abschnitte (Module, Backlog-Tabelle,
   Formeln, Studien) von Hand nachziehen — beides muss zum tatsächlichen
   Repo-Stand passen, sonst beantwortet die KI-Auskunft auf Basis veralteter
   Angaben.
3. Erneut als Artifact veröffentlichen (`Artifact`-Tool mit derselben Datei
   und, um dieselbe URL zu behalten, mit `url` auf die bestehende Adresse
   oben).

## Grenzen

- Kein Ersatz für das Repo selbst — Detailtiefe (z. B. vollständige
  Anwendungsfall-Vorlage, alle Sicherheits-Mindestkontrollen) bleibt in den
  jeweiligen Markdown-Dateien.
- Die KI-Auskunft beantwortet nur, was in der `KB`-Zeichenkette steht. Für
  Anwendungsfälle, die im Repo nur als Backlog-Zeile existieren, sagt sie
  das offen, statt Inhalte zu erfinden.
- Rechtliche und wirtschaftliche Aussagen der Auskunft sind, wie im übrigen
  Repo, Orientierung mit Datumsstand — keine Rechts- oder Steuerberatung.
