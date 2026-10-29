---
tags: [markt, daten, anbieter]
stand: 2026-10-29
---

# Marktdaten-Anbieter

Woher die Vergleichspreise und Belegungen für die Reports kommen. Seit dem 29.10.2026 gilt: Wir lesen Airbnb und Booking.com selbst aus, aber nur Marktdaten (siehe [[Entscheidungen]]). Die Anbieter unten sind die Alternative, falls das eigene Auslesen nicht trägt oder wir einen zweiten Datenstand zum Abgleich wollen.

## Eigenes Auslesen (aktueller Weg)

- **Werkzeug:** Firecrawl, angebunden in n8n (läuft seit 29.10.2026, siehe [[Tools und Konten]]).
- **Was wir speichern:** Preise, belegte Tage, Ausstattung, Bewertungsschnitt, nur zusammengefasst pro Region.
- **Was wir nicht speichern:** Gastgebernamen, Fotos von Personen, Bewertungstexte. Achtung: Suchergebnisse von Booking enthalten manchmal Sätze aus Gästebewertungen. Die werden vor dem Speichern entfernt.
- **Kosten:** Firecrawl hat 1.000 Credits pro Monat kostenlos. Eine Suche mit drei Treffern kostet 2 Credits.
- **Risiko:** AGB der Plattformen, Datenbankrecht, DSGVO. Bewusst in Kauf genommen und durch Datensparsamkeit begrenzt. Vor dem Launch rechtlich prüfen lassen.

## Anbieter mit Schnittstelle

Für uns kommen nur Anbieter mit Schnittstelle infrage, weil der Agent pro Kunde automatisch abfragen muss.

| Anbieter | Preis | Passt für uns? |
| --- | --- | --- |
| [Airbtics API](https://airbtics.com/airbnb-api) | pro Abfrage: Umsatzschätzung mit Vergleichsobjekten 0,50 $, Kurzfassung 0,10 $, Marktkennzahlen 0,25–0,50 $ | Ja, ca. 0,35–1 $ pro Report |
| [AirROI API](https://www.airroi.com/api) | ab 0,01 $ pro Abfrage, 10 $ Startguthaben, keine Grundgebühr | Ja, günstig zum Testen |
| [PriceLabs Market Dashboard](https://www.rakidzich.com/articles/how-much-does-pricelabs-cost-2026) | 19,99 $ pro Monat und Region | Nein, bei vielen Regionen zu teuer |
| [AirDNA](https://www.vaultstr.com/blog/airdna-pricing/) | 34–50 $ im Monat, nur Weboberfläche, keine API | Nein, nur für eigene Recherche |

Preise recherchiert am 29.10.2026.

> [!note] „Lizenziert“ ist ungenau
> Airbnb verkauft keine Daten. Diese Firmen erheben die Daten selbst und tragen damit das Risiko der Erhebung. Wir kaufen sie per Vertrag ein. Das ist sauberer als eigenes Crawlen, aber nicht ganz risikofrei.

## Offene Fragen

- Auf keiner der beiden API-Seiten wird Deutschland ausdrücklich genannt. Mit dem Startguthaben von AirROI ließe sich das für Garmisch testen.
- Dürfen wir eingekaufte Daten in Kunden-Reports zeigen? Vor einem Vertrag klären.
