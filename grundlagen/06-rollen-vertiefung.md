# Modul 6: Vertiefung nach Rolle

Module 1–5 gelten für alle. Dieses Modul ergänzt, was zusätzlich für Ihre
Rolle im Betrieb gilt. Lesen Sie nur den für Sie passenden Abschnitt.

## Für Anwenderinnen und Anwender

Sie arbeiten im Alltag mit einem KI-Werkzeug (Textentwurf, Übersetzung,
Zusammenfassung). Zusätzlich zu Modulen 1–5 gilt für Sie:

- Sie prüfen jedes Ergebnis fachlich, bevor Sie es weitergeben oder
  verwenden — siehe Faustregel in
  [Modul 3, Abschnitt 6](03-grenzen-und-risiken.md#6-die-faustregel-für-jedes-ergebnis).
- Sie melden ungewöhnliches Verhalten des Werkzeugs (falsche Angaben, die
  wiederholt auftreten, unerwartete Kosten, verdächtige Eingabeaufforderung
  aus einer externen Quelle) an die IT- oder Datenschutzverantwortung,
  statt es selbst zu beheben.
- Sie verwenden nur Werkzeuge und Daten gemäß der Freigabeliste des
  Betriebs ([Modul 5, Abschnitt 2](05-werkzeuge-im-unternehmen.md#2-eine-eigene-freigabeliste-führen)).

## Für Führungskräfte

Zusätzlich zu Modulen 1–5 verantworten Sie als Führungskraft:

- **Freigabe:** Sie legen fest, welche Ergebnisse eine menschliche
  Freigabe brauchen, bevor sie nach außen gehen oder eine Wirkung
  entfalten (Versand, Zahlung, Auftrag) — Grundlage:
  [Modul 3, Abschnitt 5](03-grenzen-und-risiken.md#5-wann-ein-ki-werkzeug-nicht-eingesetzt-werden-sollte)
  und [`sicherheit/README.md#4-pilotfreigabe`](../sicherheit/README.md#4-pilotfreigabe).
- **Kosten- und Nutzenkontrolle:** Sie prüfen, ob eine behauptete
  Zeitersparnis tatsächlich als Rechnung vorliegt, nicht als Prozentzahl
  ohne Grundlage — siehe [`wirtschaftlichkeit/README.md`](../wirtschaftlichkeit/README.md).
- **Keine Personalentscheidung ohne menschliche Prüfung:** Ergebnisse zu
  Bewerbungen, Leistung oder Bonität dürfen nicht automatisiert in eine
  Entscheidung einfließen — siehe
  [Modul 4, Abschnitt 4](04-datenschutz-und-recht-in-kuerze.md#4-automatisierte-bewertung-von-personen-ist-tabu).
- **Schulungspflicht im Team:** Wenn Ihr Team ein KI-Werkzeug einsetzt,
  stellen Sie sicher, dass alle Beteiligten mindestens Module 1–5 kennen —
  Ablauf und Nachweis: [`schulungsleitfaden.md`](schulungsleitfaden.md).

## Für IT- und Datenschutzverantwortliche

Zusätzlich zu Modulen 1–5 verantworten Sie:

- **Technische Mindestkontrollen** vor jedem Pilotbetrieb:
  [`sicherheit/README.md`](../sicherheit/README.md) und
  [`werkzeuge/README.md#mindestkriterien-vor-dem-pilotbetrieb`](../werkzeuge/README.md#mindestkriterien-vor-dem-pilotbetrieb).
- **Messung statt Demo-Eindruck:** Ein Testset, Messgrößen und
  Regressionstests vor der Freigabe eines Systems —
  [`evaluation.md`](evaluation.md).
- **Auftragsverarbeitungsverträge und Serverstandorte** je Werkzeug
  dokumentieren und aktuell halten — [`recht/README.md`](../recht/README.md)
  und [`werkzeuge/README.md`](../werkzeuge/README.md).
- **Freigabeliste** aus [Modul 5](05-werkzeuge-im-unternehmen.md#2-eine-eigene-freigabeliste-führen)
  pflegen und bei Änderungen (neues Werkzeug, neue Datenkategorie) vor
  Freigabe aktualisieren.
- **Abschaltweg** für jedes produktive System festlegen, inklusive
  Kriterium, wann abgeschaltet wird (z. B. kritische Fehlerrate,
  Datenabfluss) — [`sicherheit/README.md#4-pilotfreigabe`](../sicherheit/README.md#4-pilotfreigabe).

## Nächster Schritt

[Wissenscheck](wissenscheck.md) — Selbsttest zu allen sechs Modulen.
