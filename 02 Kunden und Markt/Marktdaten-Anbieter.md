---
tags: [markt, daten, anbieter]
stand: 2026-10-30
---

# Marktdaten-Anbieter

Woher die Vergleichspreise und Belegungen für die Reports kommen. Seit dem 29.10.2026 gilt: Wir lesen Airbnb und Booking.com selbst aus, aber nur Marktdaten (siehe [[Entscheidungen]]). Die Anbieter unten sind die Alternative, falls das eigene Auslesen nicht trägt oder wir einen zweiten Datenstand zum Abgleich wollen.

## Eigenes Auslesen (aktueller Weg)

- **Werkzeug:** Firecrawl, angebunden in n8n (siehe [[Tools und Konten]]). Der Marktdaten-Agent läuft seit 30.10.2026 (n8n-Workflow „hostwise · Scraping-Agent (Marktdaten)“).
- **Wie gelesen wird:** Pro Region und Saison ein Stichproben-Wochenende (dritter Freitag im Januar, April, Juli und Oktober, Fr–So, 2 Gäste, nur ganze Unterkünfte), je einmal auf Airbnb und auf Booking.com. Aus der Suchseite werden nur Zahlen gelesen.
- **Was wir speichern:** pro Region, Saison und Portal die Kennzahlen (mittlerer Preis pro Nacht und Spanne, Zahl der Angebote, Anteil ausgebucht, Bewertungsschnitt, Anteil gewerblicher Gastgeber, Ausstattungsanteile) und die einzelnen Angebote anonym: Preis auf 5 € und Größe auf 5 m² gerundet, Schlafzimmer, Bewertung (Entscheidung 30.10.2026).
- **Was wir nicht speichern:** Gastgebernamen, Titel, Links, Fotos, Bewertungstexte, genaue Lage, Zahl der Bewertungen. Erfolgreiche Läufe speichern auch in n8n keine Seiteninhalte.
- **Archiv:** Jede Saison einer Region wird einmal im Jahr gelesen, nur die nächste anstehende Saison (in den nächsten 120 Tagen) monatlich. So entsteht ein Vorjahresvergleich.
- **Großveranstaltungen:** einmal im Monat sucht der Agent Veranstaltungsseiten der Region (Firecrawl-Suche, 3 Seiten) und Claude liest die Großveranstaltungen der nächsten 12 Monate heraus: Name, Datum, Art, Größe, Quelle.
- **Kosten:** 1 Credit pro Suchseite, also 2 Credits je Saison und Region; die Veranstaltungssuche etwa 5 Credits im Monat. Eine neue Region kostet beim ersten Mal etwa 13 Credits, danach etwa 7 im Monat.
- **Erster Lauf (30.10.2026, Garmisch-Partenkirchen):** 162 Vergleichsangebote, mittlerer Preis pro Nacht auf Airbnb 135–160 €, auf Booking.com 159–214 € je nach Saison; auf Booking.com sind die Stichproben-Wochenenden schon zu 85–90 % ausgebucht. 10 Großveranstaltungen, darunter Neujahrsskispringen und Ski-Weltcup.
- **Kleine Orte (seit 30.10.2026 abgefangen):** In Amberg hat Booking.com in den Filtern auch Unterkünfte aus der Umgebung gezählt, die Trefferzahl aber nur für den Ort. Dadurch kamen Ausstattungsanteile über 100 % heraus (z. B. Küche 422 %). Der Agent verwirft solche Ausstattungen jetzt und zählt nur so viele Angebote, wie Booking.com Treffer meldet; die falschen Werte von Amberg (Sommer, Winter) sind geleert. Die Preise von Amberg im Sommer enthalten noch Angebote aus der Umgebung, bis die Saison im nächsten Jahr neu gelesen wird.
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
