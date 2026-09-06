# Modul 5: Werkzeuge im Unternehmen

Ziel dieses Moduls: Sie wissen, welche Art von KI-Werkzeug Sie im
Arbeitsalltag verwenden dürfen, und woran Sie ein nicht freigegebenes
Werkzeug erkennen.

Voraussetzung: [Modul 4](04-datenschutz-und-recht-in-kuerze.md).

## 1. Firmenwerkzeug versus privater Zugang ("Schatten-KI")

Viele Beschäftigte nutzen KI-Werkzeuge über einen privaten Zugang (eigenes
Konto, private E-Mail-Adresse), weil kein Firmenzugang vorhanden ist —
oft ohne bösen Willen, aber mit denselben Datenschutzrisiken wie in
[Modul 4](04-datenschutz-und-recht-in-kuerze.md) beschrieben. Das wird als
"Schatten-KI" bezeichnet: Nutzung außerhalb der Kontrolle und ohne
Auftragsverarbeitungsvertrag des Betriebs.

**Faustregel:** Ein privater Zugang zu einem KI-Werkzeug ist für rein
persönliche, nicht betriebliche Zwecke akzeptabel. Für betriebliche
Inhalte — auch nur zum Testen — gilt ausschließlich ein vom Betrieb
freigegebenes Werkzeug mit geklärtem Datenschutzstatus.

## 2. Eine eigene Freigabeliste führen

Jeder Betrieb sollte eine kurze, aktuelle Liste führen: welches Werkzeug
ist freigegeben, wofür, und mit welchen Daten es genutzt werden darf.
Beispielhafter Aufbau (Platzhalterzeile, an den eigenen Betrieb
anzupassen — keine reale Freigabe):

| Werkzeug | Freigegeben für | Nicht erlaubt für | Verantwortlich |
| --- | --- | --- | --- |
| [Beispiel: Firmenzugang Anbieter X] | interne Textentwürfe, Übersetzung | Kunden-/Personaldaten ohne gesonderte Prüfung | IT-Verantwortliche |

Kriterien für die technische Auswahl eines Werkzeugs (Serverstandort,
lokale Alternative, Lizenz): [`werkzeuge/README.md`](../werkzeuge/README.md).
Mindestprüfung vor dem Pilotbetrieb: [`werkzeuge/README.md#mindestkriterien-vor-dem-pilotbetrieb`](../werkzeuge/README.md#mindestkriterien-vor-dem-pilotbetrieb).

## 3. Wenn Daten das Haus nicht verlassen dürfen

Für Konstruktionsdaten, Preislisten mit Wettbewerbsrelevanz oder andere
vertrauliche Inhalte ist ein Cloud-Werkzeug oft nicht geeignet. Die
Alternative ist der Betrieb eines offenen Sprachmodells über
[Ollama](https://github.com/ollama/ollama) auf eigener oder EU-gehosteter
Infrastruktur — die Daten verlassen dabei die eigene Infrastruktur nicht.
Das ersetzt keine eigene Prüfung von Backups, Telemetrie und
Administrationszugängen. Details:
[`werkzeuge/README.md#lokale-eu-gehostete-und-cloud-modelle-getrennt-bewerten`](../werkzeuge/README.md#lokale-eu-gehostete-und-cloud-modelle-getrennt-bewerten)
und [`recht/README.md#5-lokale-alternative-als-grundsatz`](../recht/README.md#5-lokale-alternative-als-grundsatz).

## 4. Kosten im Blick behalten

Cloud-Werkzeuge berechnen meist nach Nutzung (Token, siehe
[Modul 1](01-grundbegriffe.md#2-token-kontextfenster-systemprompt)).
Ungewöhnlich hohe oder plötzlich steigende Kosten sind ein Hinweis auf
eine fehlerhafte Automatisierung (z. B. eine Endlosschleife) oder eine
zweckfremde Nutzung — beides an die IT-Verantwortung melden. Rechenweg:
[`wirtschaftlichkeit/README.md`](../wirtschaftlichkeit/README.md).

## Weiter mit Modul 6

[Modul 6: Vertiefung nach Rolle](06-rollen-vertiefung.md).
