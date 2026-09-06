# Rechtlicher Rahmen: Orientierung, keine Rechtsberatung

Alle Aussagen in diesem Ordner sind Orientierung für die eigene Einschätzung,
keine Rechtsberatung. Für eine verbindliche Bewertung im Einzelfall ziehen
Sie eine Fachanwältin oder einen Fachanwalt für IT-Recht bzw. Ihren
Datenschutzbeauftragten hinzu. Stand aller Angaben: 2026-09-06. Rechtslage
und Auslegung ändern sich — prüfen Sie vor einer Entscheidung, ob eine
Angabe noch aktuell ist.

Ergänzende, tiefergehende Vorlagen Dritter zu diesem Thema: siehe
[`quellen/README.md`](../quellen/README.md#eu-ai-act-und-compliance).

## 1. DSGVO — die praktisch relevanten Fragen

Bei jedem Anwendungsfall in [`anwendungsfaelle/`](../anwendungsfaelle/)
werden unter Punkt 7 ("Datenschutz") folgende Fragen beantwortet:

- **Welche Daten verlassen das Haus?** Personenbezogene Daten
  (Kundennamen, Mitarbeiterdaten, Bewerbungen) unterliegen der DSGVO.
  Rein technische Daten (anonymisierte Maße, Stücklisten ohne Kundenbezug)
  in der Regel nicht.
- **Wer verarbeitet sie, und wo?** Bei Anbietern mit Sitz außerhalb der
  EU/des EWR (z. B. USA) ist eine Übermittlung in ein Drittland zu prüfen.
  Anbieter mit EU-Serverstandort (siehe [`werkzeuge/`](../werkzeuge/))
  vereinfachen das.
- **Ist ein Auftragsverarbeitungsvertrag (AVV) nötig?** Ja, sobald ein
  externer Dienst personenbezogene Daten in Ihrem Auftrag verarbeitet
  (Art. 28 DSGVO). Große Anbieter (OpenAI, Anthropic, Microsoft, Mistral)
  bieten Standard-AVVs an — Abschluss ist meist online möglich, wird aber
  häufig vergessen.
- **Ist eine Datenschutz-Folgenabschätzung (DSFA) nötig?** Bei
  systematischer, umfangreicher Verarbeitung oder besonderen
  Datenkategorien (z. B. Gesundheitsdaten, Bewerberdaten mit
  automatisierter Bewertung) im Zweifel ja — im Einzelfall prüfen.

## 2. EU AI Act — Transparenzpflichten nach Art. 50

Seit dem **2. August 2026** gilt die allgemeine Anwendung der Verordnung
(EU) 2024/1689; die konsolidierte Fassung steht bei
[EUR-Lex](https://eur-lex.europa.eu/eli/reg/2024/1689/oj). Art. 50 enthält
Transparenzpflichten für bestimmte KI-Systeme, nicht pauschal für jede
KI-Nutzung. Relevant für die Anwendungsfälle in diesem Repo sind vor allem:

- **Chatbots und KI-Assistenten mit Kundenkontakt** müssen für die
  Nutzerin oder den Nutzer erkennbar als KI gekennzeichnet sein — spätestens
  bei der ersten Interaktion, in einfacher, verständlicher Sprache.
- **KI-generierte Texte, Bilder, Audio- oder Videoinhalte**, die
  veröffentlicht werden (z. B. Marketingtexte, Bilder), müssen unter
  bestimmten Voraussetzungen als KI-generiert gekennzeichnet werden.
- Die Verordnung sieht in Art. 99 je nach Verstoß unterschiedliche
  Höchstgrenzen vor. Für Verstöße gegen Art. 50 nennt sie bis zu 15 Mio. Euro
  oder 3 % des weltweiten Jahresumsatzes. Für Unternehmen gilt nach Art. 99(6)
  die jeweils niedrigere Grenze. Das sind Höchstgrenzen, keine automatische
  Sanktion im Einzelfall.
- Für generative KI-Systeme, die bereits vor dem 2. August 2026 im Einsatz
  waren, gilt eine Übergangsfrist zur maschinenlesbaren Kennzeichnung bis 2. Dezember 2026.

**Praktische Konsequenz für dieses Repo:** Jeder Anwendungsfall mit
direktem Kundenkontakt (z. B. Chatbot für Auftragsstatus) weist unter
Punkt 7 explizit auf diese Kennzeichnungspflicht hin.

## 3. EU AI Act — Hochrisiko-Anwendungen (Anhang III)

Bestimmte Einsatzzwecke gelten unabhängig vom eingesetzten Modell als
Hochrisiko und unterliegen deutlich strengeren Pflichten (u. a.
Risikomanagement, menschliche Aufsicht, Dokumentationspflicht). Für den
Mittelstand am relevantesten:

- **Automatisierte Bewertung oder Auswahl von Bewerbungen** (Recruiting-
  Scoring). Deshalb enthält dieses Repo bewusst keinen Anwendungsfall zur
  automatisierten Bewerberauswahl — nur zur Formulierung von
  Stellenanzeigen, was kein Hochrisiko-Einsatzzweck ist.
- **Bewertung von Mitarbeiterleistung**, wenn sie automatisiert in
  Personalentscheidungen einfließt.
- **Bonitätsprüfung/Kreditwürdigkeit**, sofern automatisiert entschieden
  wird.

Im Zweifel: Fließt das KI-Ergebnis direkt und ohne wirksame menschliche
Prüfung in eine Entscheidung über eine Person ein, prüfen Sie vor dem
Einsatz, ob Anhang III einschlägig ist.

## 4. Technisches Risiko: Manipulierte Eingaben (Prompt Injection)

Kein DSGVO- oder AI-Act-Thema im engeren Sinn, aber eine Fehlerquelle, die
bei automatisierter Verarbeitung externer Inhalte (eingehende E-Mails,
hochgeladene Dokumente, Web-Inhalte) in jedem betroffenen Anwendungsfall
unter Punkt 6 ("Grenzen") genannt werden muss: Ein System, das Kunden-
E-Mails automatisch zusammenfasst oder beantwortet, verarbeitet auch
Inhalte, die ein Absender absichtlich so formuliert, dass sie Anweisungen
an das KI-System enthalten ("ignoriere die bisherige Anweisung und …").
Das Modell kann diese Anweisung befolgen, ohne dass ein Mensch das
bemerkt. Eingestuft als eines der Hauptrisiken im
[OWASP GenAI LLM Top 10 2025](https://github.com/GenAI-Security-Project/GenAI-LLM-Top10/tree/main/2025),
dem aktuellen OWASP-Referenzrahmen für Risiken bei LLM-Anwendungen
(Stand der Prüfung: 2026-09-06). Die ältere
[2023-Fassung](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/tab_archive.md)
ist archiviert.

**Praktische Konsequenz:** Automatisch aus externen Inhalten erzeugte
Aktionen (eine Antwort versenden, eine Zahlung auslösen, einen Auftrag
anlegen) benötigen eine menschliche Freigabe, bevor sie wirksam werden —
insbesondere bei den Anwendungsfällen 2, 3 und 9, die direkt auf
eingehenden externen Text reagieren.

## 5. Lokale Alternative als Grundsatz

Wenn Daten das Haus aus Datenschutz- oder Vertraulichkeitsgründen nicht
verlassen dürfen (z. B. Konstruktionsdaten, Preislisten mit
Wettbewerbsrelevanz), ist der Betrieb eines offenen Modells über Ollama
auf eigener oder EU-gehosteter Hardware die Alternative — siehe
[`werkzeuge/README.md`](../werkzeuge/README.md#lokaleoffene-modelle-daten-verlassen-das-haus-nicht).
Diese Alternative wird deshalb in jedem Anwendungsfall genannt, der einen
Cloud-Anbieter als Hauptweg vorschlägt.
