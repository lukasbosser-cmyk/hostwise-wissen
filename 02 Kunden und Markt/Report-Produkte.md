---
tags: [markt, produkte, reports]
stand: 2026-10-30
---

# Report-Produkte

> [!info] Ausführliche Fassung
> Die Impulse, was 29 € und 149 € wert macht, stehen im Claude Doc [hostwise Reports – was 29 € und 149 € wert macht](https://claude.ai/artifact/VhEePYMqmT54KafSsk1fMN). Diese Notiz fasst zusammen, was davon gebaut ist.

Jede Stufe beantwortet eine größere Frage des Vermieters und rechnet mit unseren eigenen Marktdaten. Der Preis ist gerechtfertigt, wenn der Report eine Summe in Euro zeigt, die ihn um ein Vielfaches übersteigt, und jede Zahl nachprüfbar ist.

| Produkt | Preis | Frage des Vermieters | Was er bekommt |
| --- | --- | --- | --- |
| Kurz-Check | 0 € | Liege ich grob richtig? | Saisonpreise im Vergleich, drei Tipps |
| Quick-Check | 29 € | Welchen Preis soll ich nehmen? | Fester Preis je Saison (Wochenende und Werktag), Veranstaltungskalender mit Preis, Mehrertrag in Euro, drei Sofort-Maßnahmen |
| Komplett-Analyse | 149 € | Wo liegt mein Geld und was mache ich zuerst? | Alles aus dem Quick-Check, dazu Ertragslücke zum Markt, Ausstattung und Portale im Vergleich, Maßnahmenplan mit Beitrag in Euro |
| Monitor | 39 €/Monat | Hat sich etwas verändert? | Erster Report, danach jeden Monat ein kurzer Bericht: Preise der Vergleichsangebote, neue Veranstaltungen, Hinweis sechs Wochen vor Saisonbeginn |

Faustwert für den Verkauf: Der Quick-Check soll mindestens 300 € Mehrertrag im Jahr zeigen, die Komplett-Analyse mindestens 1.500 €. Zeigt die Rechnung weniger, sagt der Report das ehrlich und empfiehlt keine teurere Stufe. Beide Werte stehen in der Tabelle „Produkte“ und lassen sich in der engine ändern.

## Was einen Report sauber macht

- **Die KI rechnet nicht, sie schreibt.** Alle Zahlen kommen aus einem festen Rechenkern in Supabase. Zwei Kunden mit gleichen Angaben bekommen dieselben Zahlen.
- **Feste Gliederung je Produkt**, gepflegt in der engine unter „Daten“ → „Produkte“.
- **Prüfung vor der Freigabe:** Fehlt ein Kapitel oder steht ein Euro-Betrag im Text, der nicht aus dem Rechenkern stammt, steht das auf der Freigabe.
- **Ehrliche Kennzeichnung:** Werktagspreise sind Schätzungen (wir lesen nur Wochenenden), angenommene Nächte stehen als Annahme im Text.
- **Druckansicht im hostwise-Design**, daraus wird mit einem Klick ein PDF.

## So rechnet der Rechenkern

- Verglichen wird mit Angeboten mit gleich vielen Schlafzimmern, wenn es pro Saison mindestens fünf gibt, sonst mit allen Größen. Airbnb und Booking.com zählen zusammen.
- Empfehlung am Wochenende: die Mitte der Vergleichsangebote, auf 5 € gerundet, höchstens 25 % über dem heutigen Preis, höchstens im teuren Viertel und nie unter dem heutigen Preis. Werktag: ca. 85 % davon.
- Ohne Angabe rechnet er mit 120 belegten Nächten im Jahr, gleich auf die vier Saisons verteilt.
- Veranstaltungen: große +30 %, mittlere +15 % auf den Wochenendpreis, höchstens vier Nächte je Veranstaltung.
- Die **Ertragslücke** ist der Abstand zur Mitte des Marktes mal Nächte plus Veranstaltungen. Sie zeigt, was langfristig drin ist; der Mehrertrag zeigt, was mit der Empfehlung sofort geht.

## Erste Testläufe (30.10.2026, Testdaten)

- Komplett-Analyse Garmisch-Partenkirchen, 1 Schlafzimmer, 95 € pro Nacht: Ertragslücke 5.550 € im Jahr, davon 2.100 € sofort mit 120 € statt 95 €.
- Monitor Amberg, 2 Schlafzimmer, 140 € pro Nacht: Preis passt zum Markt, Mehrertrag nur über Veranstaltungen, ca. 220 € im Jahr.

> [!warning] Noch offen
> - Monitor als 39 € im Monat oder als Jahrespreis anbieten? In den simulierten Interviews lehnen 3 von 6 das Monatsabo ab.
> - Das eigene Inserat des Kunden auslesen (Fotos, Titel, Beschreibung)? Bis dahin fragt das Formular die Ausstattung ab.
> - Werktage zusätzlich lesen? Kostet 2 Firecrawl-Credits mehr je Saison und Region.
> - Bezahlung (W3) und E-Mail-Versand nach der Freigabe (M7) fehlen noch.

Siehe auch: [[hostwise engine]], [[Marktdaten-Anbieter]], [[Simulierte Interviews]], [[Pflichtenheft]].
