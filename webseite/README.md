# Webseite: KI-Schulung Mittelstand

Eine einzelne, eigenständige HTML-Seite: eine interaktive, dreizehnteilige
Trainingswebsite auf Basis von [`grundlagen/`](../grundlagen/), mit einer
eingebetteten KI-Auskunft (Fragebogen + Chat). Kein Build-Prozess, kein
Server, keine Abhängigkeiten außer zwei Google-Fonts-Links.

Veröffentlicht als Claude-Artifact:
<https://claude.ai/code/artifact/b5d02378-b21e-47ee-bdfb-970546d9d4dd>
(privat, bis über das Teilen-Menü der Seite freigegeben).

Stand: 2026-09-06.

## Drei Bereiche

Über die obere Reiterleiste erreichbar:

| Bereich | Inhalt |
| --- | --- |
| **Auskunft** | Fragebogen und Chat (siehe unten) |
| **Kurs** | Der eigentliche Kurs-Player: dreizehn vollständige Lektionen mit Sidebar-Navigation und Fortschrittsanzeige |
| **Referenz** | Kondensierte Zahlen/Tabellen aus `README.md`, `werkzeuge/`, `recht/`, `sicherheit/`, `wirtschaftlichkeit/`, `quellen/` |

### Der Kurs

Anders als die frühere Fassung dieser Seite (die nur eine
Ein-Satz-Zusammenfassung je Modul zeigte und auf die Markdown-Dateien
verwies) enthält der Kurs-Player den **vollständigen Inhalt** aller
dreizehn Lektionen direkt auf der Seite — sinnvoll, weil eine besuchende
Person die zugrunde liegenden `.md`-Dateien im Repository gar nicht
einsehen kann. Dreizehn Lektionen, gruppiert in der linken
Navigationsleiste:

- **Basis-Schulung:** die sechs Module aus `grundlagen/01`–`06` plus
  Wissenscheck (als aufklappbare Fragen/Antworten).
- **Technische Vertiefung:** `evaluation.md`,
  `rag-produktionsprobleme.md`, `rag-techniken.md`, `llm-fine-tuning.md`,
  `llm-optimierung.md`, `agentische-systeme.md`.

Der Lektionsinhalt liegt als HTML-Konstanten (`LESSON_M1` … `LESSON_AS`)
im `<script>`-Block von [`index.html`](index.html) — von Hand aus den
jeweiligen `.md`-Dateien übertragen, keine automatische Konvertierung.
Fortschritt ("gelesen") wird per `localStorage` im Browser der
besuchenden Person gespeichert, nicht geteilt und nicht an Claude oder den
Betreiber übermittelt.

## Fragebogen und Chat

Zwei getrennte Bausteine, umschaltbar über die Reiter im Kopf des
Assistenten-Kastens (Bereich "Auskunft"):

- **Fragebogen:** ein klassischer Klick-Fragebogen ohne KI — vier feste
  Fragen (Rolle, größtes Zeitproblem, Vertraulichkeit der Daten,
  Betriebsgröße) mit Antwortoptionen zum Anklicken, Fortschrittsbalken und
  Zurück-Navigation. Die Auswertung ist eine feste Zuordnungstabelle in
  JavaScript (`ROLLE_TEXT`, `PROBLEM_TEXT`, `VERTRAULICH_TEXT`,
  `GROESSE_TEXT`) und liefert vier Ergebniskacheln: passende Lektion,
  passender Backlog-Anwendungsfall, Werkzeug-Ansatz, nächster Schritt.
  Funktioniert vollständig ohne KI-Aufruf. Optional lässt sich das
  Ergebnis über den Knopf "Mit KI ausformulieren" einmalig zu einem
  persönlichen Absatz erweitern (ein einzelner `sample()`-Aufruf mit den
  vier Antworten, kein Chatverlauf).
- **Chat:** ein Chat im Stil bekannter KI-Chat-Oberflächen — Avatar-Kreise,
  Sprechblase rechts für eigene Nachrichten, freier Fließtext links für
  Antworten, abgerundetes Eingabefeld mit Sende-Button, drei tanzende
  Punkte als Tippanzeige während Claude antwortet. Beispiel-Chips helfen
  beim Einstieg.

Dieser Agent ist bewusst so gebaut, dass er sich bei jeder besuchenden
Person neu einbettet: Er läuft vollständig im Browser der Person über
deren eigenes Claude-Konto, ohne eigenen Server und ohne dass der
Betreiber der Seite mitliest oder etwas konfigurieren muss.

Beide Bausteine, die die KI nutzen, teilen sich dieselbe Grundlage
(`script`-Block in [`index.html`](index.html)): eine feste
Kontext-Zeichenkette (`KB`) mit der kondensierten Wissensbasis aller
dreizehn Lektionen plus Referenzdaten wird bei jedem Aufruf mitgeschickt —
die `sample`-Fähigkeit hat kein Gedächtnis zwischen Aufrufen, der Chat
hängt seinen bisherigen Verlauf selbst wieder an. Die Regeln in `KB`
erzwingen dieselben Grundsätze wie [`AGENTS.md`](../AGENTS.md): Sie-Form,
keine erfundenen Preise, Zeitersparnis nur als Rechnung, kein
Bewerber-Scoring, lokale Alternative bei Vertraulichkeit nennen,
Rechtsaussagen nur als datierte Orientierung.

Kosten und Einwilligung: Jeder KI-Aufruf verbraucht das Claude-Guthaben der
besuchenden Person, nicht das des Betreibers. Der erste Aufruf fragt um
Erlaubnis; bei Ablehnung blendet die Seite Chat und "Mit KI ausformulieren"
dauerhaft aus (siehe `permanentlyHide()` in [`index.html`](index.html)).
Der Fragebogen und der gesamte Kurs-Player brauchen dafür keine Erlaubnis
und bleiben in jedem Fall nutzbar.

## Design

Gestaltet als technisches Datenblatt statt als Werbe-Landingpage — passend
zur Regel aus [`AGENTS.md`](../AGENTS.md), dass jede aus diesem Repo
gespeiste Antwort ohne Marketingsprache und Superlative auskommt. Der
Kopfbereich ist einem DIN-Schriftfeld nachempfunden (Benennung, Zielgruppe,
Stand, Lizenz, Blatt-Nummer), wie es auf technischen Zeichnungen steht —
naheliegend, weil die fiktive Referenzfirma des gesamten Repos ein
Metallbaubetrieb ist. Der Kurs-Player übernimmt dieselbe Sprache
(Fließtext, Tabellen, Zitat-Boxen für Prompt-Beispiele) statt eines
eigenen E-Learning-Looks. Schriften: Titillium Web (Überschriften, Label),
IBM Plex Sans (Fließtext), IBM Plex Mono (Zahlen, Daten, Chat-Transkript).
Hell-/Dunkelmodus vollständig unterstützt.

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
(`permanentlyHide()`); **Fragebogen und Kurs** funktionieren dort
unverändert vollständig, weil sie ohne KI-Aufruf auskommen. Für die volle
Seite mit KI-Auskunft bleibt der Claude-Artifact-Link oben maßgeblich.

## Aktualisieren

1. [`index.html`](index.html) direkt bearbeiten (kein Build-Schritt).
2. Bei inhaltlichen Änderungen an einer Lektion in `grundlagen/`: die
   passende `LESSON_*`-Konstante im `<script>`-Block von Hand nachziehen.
   Bei einer neuen Lektion: neue `LESSON_*`-Konstante ergänzen und einen
   Eintrag im `LESSONS`-Array hinzufügen.
3. Bei anderen inhaltlichen Änderungen im Repo (Zahlen, Rechtsfristen,
   Werkzeuge): sowohl die `KB`-Konstante (für die KI-Auskunft) als auch
   den Bereich "Referenz" (für die sichtbare Anzeige) von Hand nachziehen
   — beides muss zum tatsächlichen Repo-Stand passen.
4. Vor dem Veröffentlichen einmalig `node --check` auf den extrahierten
   `<script>`-Inhalt laufen lassen (reine Syntaxprüfung, kein Test-Loop) —
   bei handgeschriebenen Template-Strings mit vielen Sonderzeichen ist das
   die schnellste Art, einen kaputten String vor der Veröffentlichung zu
   finden.
5. Erneut als Artifact veröffentlichen (`Artifact`-Tool mit derselben
   Datei und, um dieselbe URL zu behalten, mit `url` auf die bestehende
   Adresse oben) und die Kopie unter `webseite/index.html` im Repository
   aktuell halten.

## Grenzen

- Kein Ersatz für das Repo selbst — Detailtiefe, die über die dreizehn
  Lektionen hinausgeht (z. B. vollständige Anwendungsfall-Vorlage, alle
  Sicherheits-Mindestkontrollen), bleibt in den jeweiligen
  Markdown-Dateien.
- Die KI-Auskunft beantwortet nur, was in der `KB`-Zeichenkette steht. Für
  Anwendungsfälle, die im Repo nur als Backlog-Zeile existieren, sagt sie
  das offen, statt Inhalte zu erfinden.
- Rechtliche und wirtschaftliche Aussagen der Auskunft sind, wie im übrigen
  Repo, Orientierung mit Datumsstand — keine Rechts- oder Steuerberatung.
- Der Fortschrittsbalken im Kurs ist eine reine Lesebestätigung
  ("angeklickt"), keine Lernerfolgskontrolle — die prüft der Wissenscheck.
