# Wirtschaftlichkeit: Rechenrahmen statt Behauptungen

Dieser Ordner legt fest, wie Kosten und Nutzen in jedem Anwendungsfall
berechnet werden — damit alle Zahlen in diesem Repo vergleichbar sind und
niemand behauptete Prozentzahlen ohne Rechnung akzeptieren muss.

## 1. Kosten pro Vorgang berechnen

Formel für die laufenden API-/Token-Kosten eines einzelnen Vorgangs:

```
Kosten je Vorgang = (Eingabe-Tokens × Preis je Eingabe-Token)
                   + (Ausgabe-Tokens × Preis je Ausgabe-Token)
```

- Tokenmenge lässt sich am bestehenden Prompt/Beispieltext grob abschätzen
  (Faustregel: 1 Token ≈ 0,75 deutsche Wörter) oder mit einem Tokenizer
  exakt zählen.
- Aktuelle Preise je Modell ändern sich häufig. Statt Preise hier zu
  pflegen, verweist jeder Anwendungsfall auf den Zeitpunkt der Prüfung und
  markiert unsichere Werte mit `[PRÜFEN]`. Werkzeuge zum Live-Abgleich:
  siehe [`quellen/README.md`](../quellen/README.md#kostenrechner-für-llm-apis).
- Bei Automatisierungsplattformen (n8n Cloud, Make) kommen ggf.
  Ausführungs- oder Vorgangskosten der Plattform selbst hinzu — getrennt
  von den Modellkosten ausweisen.
- **Ohne KI-Komponente entfällt diese Formel.** Bei klassischer
  Automatisierung (z. B. Ansible, Terraform, Jenkins, ROS) gibt es keine
  Token-Kosten — hier zählen nur Lizenz-/Hosting-Kosten (siehe
  Steckbrief in [`werkzeuge/README.md`](../werkzeuge/README.md)) und
  Einrichtung (Abschnitt 2 unten).

## 2. Einrichtungsaufwand

```
Einmalige Kosten = Einrichtungsstunden × Stundensatz
```

- Stundensatz als Annahme kennzeichnen (intern: ca. Bruttopersonalkosten
  je Stunde; extern: Dienstleistersatz `[PRÜFEN]`).
- Realistisch einordnen: Ein Anwendungsfall mit "niedrigem" Aufwand
  bedeutet in der Regel 2 bis 4 Stunden für den ersten funktionierenden
  Durchlauf, nicht Minuten — Testen und Nachjustieren eingerechnet.

## 3. Nutzen berechnen

```
Zeitersparnis je Vorgang = Zeit vorher − Zeit nachher
Ersparnis je Monat = Zeitersparnis je Vorgang × Häufigkeit je Monat
Amortisation (Monate) = Einmalige Kosten ÷ (Ersparnis je Monat in Euro
                         − laufende Kosten je Monat)
```

- "Ersparnis in Euro" setzt einen internen Stundensatz voraus — diesen
  explizit nennen, nicht implizit annehmen.
- Zeitersparnis wird immer als Vorher/Nachher-Rechnung gezeigt (siehe
  [`anwendungsfaelle/VORLAGE.md`](../anwendungsfaelle/VORLAGE.md), Punkt 5),
  nie als freistehende Prozentzahl.
- Qualitative Nutzen (z. B. schnellere Reaktionszeit gegenüber Kunden,
  weniger Fehler durch Vier-Augen-Wegfall) werden benannt, aber nicht in
  eine Euro-Zahl gezwungen, wenn dafür keine belastbare Grundlage besteht.

## 4. Anbietervergleich: worauf es ankommt

Nicht der günstigste Preis pro Token entscheidet, sondern die Kosten pro
gelöstem Vorgang bei ausreichender Qualität. Vergleichskriterien, die in
jedem Anwendungsfall relevant sind:

| Kriterium | Warum relevant |
|---|---|
| Preis je Vorgang (nicht je Token) | Ein teureres Modell kann bei weniger Fehlern und Nacharbeit günstiger sein |
| Serverstandort | siehe [`recht/README.md`](../recht/README.md) — Drittlandübermittlung, AVV |
| Verfügbarkeit eines AVV | ohne AVV bei personenbezogenen Daten nicht einsetzbar |
| Möglichkeit lokaler/offener Alternative | relevant, wenn Daten das Haus nicht verlassen dürfen |
| Abhängigkeit vom Anbieter (Lock-in) | Wechselkosten bei Preiserhöhung oder Abkündigung |

## 5. Was die Forschung zu Zeitersparnis zeigt

Diese Studien ersetzen keine eigene Messung im Betrieb (siehe Punkt 3),
liefern aber eine Einordnung, ob eine im Anwendungsfall behauptete
Zeitersparnis plausibel ist. Beide sind kontrollierte Studien in
Großunternehmen bzw. mit Freiberuflern, nicht im deutschen Mittelstand —
Übertragbarkeit im Einzelfall prüfen.

- **Noy & Zhang (2023),** *"Experimental evidence on the productivity
  effects of generative artificial intelligence"*, Science, DOI:
  [10.1126/science.adh2586](https://www.science.org/doi/10.1126/science.adh2586).
  453 Berufstätige mit Hochschulabschluss bearbeiteten berufstypische
  Schreibaufgaben; die Hälfte durfte ChatGPT nutzen. Ergebnis: rund 40 %
  weniger Zeitaufwand, 18 % höher bewertete Qualität. Übertragbarkeit auf
  Anwendungsfälle wie Angebots- oder Vertriebstexte (siehe
  [`anwendungsfaelle/`](../anwendungsfaelle/)) naheliegend, aber nicht
  gemessen.
- **Brynjolfsson, Li & Raymond,** *"Generative AI at Work"*, NBER Working
  Paper Nr. 31161 (2023), veröffentlicht in der Quarterly Journal of
  Economics (2025): [nber.org/papers/w31161](https://www.nber.org/papers/w31161).
  5.179 Kundenservice-Mitarbeitende eines Softwareunternehmens erhielten
  gestaffelt einen KI-Assistenten. Ergebnis: durchschnittlich 14 % mehr
  gelöste Vorgänge pro Stunde, bei unerfahrenen Beschäftigten 34 % mehr —
  bei erfahrenen kaum ein Effekt. Direkt relevant für Anwendungsfall 3
  (automatische Beantwortung von Standard-Kundenanfragen): der Nutzen
  hängt stark vom Erfahrungsstand der Person ab, die das Ergebnis prüft.

## 6. Was hier bewusst fehlt

Keine pauschale Tabelle "Modell X kostet Y Cent" — das wäre in wenigen
Monaten veraltet und würde gegen die Regel verstoßen, keine erfundenen
oder ungeprüften Preise zu nennen. Aktuelle Zahlen gehören in den
jeweiligen Anwendungsfall, mit Datum der Prüfung.
