---
tags: [technik, engine, agenten]
stand: 2026-10-30
---

# hostwise engine

Das „Gehirn“ von hostwise: ein Dashboard, in dem alle KI-Agenten sichtbar sind, trainiert, angebunden und ihre Ergebnisse freigegeben werden. Ziel ist, dass das Team mit 30–45 Minuten am Tag auskommt (US-14 in [[Vermieter-Perspektiven und User Stories]]).

![[engine-cockpit.png]]

## Wo was liegt

| Was | Wo |
| --- | --- |
| Code | GitHub-Repo [hostwisedemo](https://github.com/lukasbosser-cmyk/hostwisedemo) (Next.js) |
| Datenbank und Login | Supabase-Projekt „hostwise“ (Frankfurt) |
| Agenten-Abläufe | n8n Cloud: [hostwise.app.n8n.cloud](https://hostwise.app.n8n.cloud) |
| Webseiten auslesen | Firecrawl, nur über n8n |
| Ursprünglicher Bau-Auftrag | [[Bau-Prompt Grundgerüst]] |

## Seiten

| Seite | Inhalt |
| --- | --- |
| Cockpit | Kennzahlen, animierte Agenten-Übersicht, Live-Aktivität, offene Freigaben |
| Agenten | Alle Agenten mit Filter, Assistent zum Anbinden neuer Agenten |
| Agent | Überblick, Training (Wissen, Leitplanken, Selbstständigkeit), Verbindungen, Verlauf; beim Vertrieb zusätzlich die eingeschätzten Anfragen und die Meta-Anzeigen |
| Freigaben | Ergebnisse prüfen und freigeben oder zurückgeben, Druckansicht der Reports als PDF |
| Marktdaten | Preise je Saison von Airbnb und Booking.com, Großveranstaltungen und Ausstattung pro Region; Regionen aufnehmen oder pausieren |
| Wissen | Alle Wissensquellen |
| Daten | Alle Tabellen in Supabase: ansehen, durchsuchen, erlaubte Felder ändern, Einträge mit Rückfrage löschen, CSV herunterladen |
| Einstellungen | Platzhalter |

## Stand 30.10.2026

- **Login:** nur die drei Admins (E-Mail und Passwort). Oskar und Maximilian brauchen noch ein Konto, das Lukas im Supabase-Dashboard anlegt.
- **Freigaben und Aktivität** kommen live aus Supabase.
- **Agenten-Einstellungen** (Pause, Selbstständigkeit, Leitplanken, Wissen, Anbinden) werden gespeichert und erscheinen bei allen Admins ohne Neuladen. Seit Pull Request #2 (29.10.2026) in der engine.
- **Report-Agent** in n8n: Formular „Kurz-Check“ → Anfrage in Supabase → Claude schreibt den Kurz-Check → wartet in der engine unter „Freigaben“. Er liest die Leitplanken aus der engine bei jedem Durchlauf neu. Veröffentlicht seit 30.10.2026.
- **Report-Agent** rechnet seit 30.10.2026 mit echten Marktdaten: Er ruft den Marktdaten-Agenten auf und bekommt Preise je Saison, den Vergleich mit gleich vielen Schlafzimmern und die Großveranstaltungen der Region. Das Formular fragt dafür optional nach der Zahl der Schlafzimmer.
- **Report-Agent für die bezahlten Produkte** (n8n-Workflow „hostwise · Report-Agent (Quick-Check, Komplett-Analyse, Monitor)“, seit 30.10.2026): drei Bestellformulare → Bestellung in Supabase → Marktdaten holen → der **Rechenkern** in Supabase rechnet alle Zahlen (Empfehlung je Saison, Mehrertrag, Ertragslücke zum Markt, Veranstaltungen, Ausstattung) → Claude schreibt nur den Text nach der Gliederung des Produkts → eine Prüfung schaut, ob alle Kapitel da sind und jeder Euro-Betrag aus dem Rechenkern stammt → Freigabe in der engine. Der Monitor bekommt danach am 2. jedes Monats einen kurzen Monatsbericht (oder saisonal sechs Wochen vor Saisonbeginn). Preise und Gliederungen stehen in der Tabelle „Produkte“ unter „Daten“. Jeder Report hat eine **Druckansicht** (`/report/<id>`, Link in den Freigaben) zum Speichern als PDF. Was die Reports wert macht, steht in [[Report-Produkte]]. Bezahlung (W3) und E-Mail-Versand (M7) fehlen noch.
- **Marktdaten-Agent** (n8n-Workflow „hostwise · Scraping-Agent (Marktdaten)“): liest pro Region und Saison ein Wochenende (Fr–So, 2 Gäste) auf Airbnb und Booking.com über Firecrawl, speichert Kennzahlen und anonyme Einzelangebote und sucht einmal im Monat die Großveranstaltungen. Läuft am 1. jedes Monats für alle aktiven Regionen und auf Abruf des Report-Agenten. Erste Region: Garmisch-Partenkirchen. Wie genau, steht in [[Marktdaten-Anbieter]].
- **Vertriebs-Agent** (n8n-Workflow „hostwise · Vertriebs-Agent (Leads und Anzeigen)“, seit 30.10.2026): läuft jeden Morgen um 7 Uhr. Er schätzt jede neue Kurz-Check-Anfrage ein (heiß, warm oder kalt, passendes Produkt, Rückruf ja oder nein, mit Grund und nächstem Schritt) und schlägt einmal pro Woche 2–3 Meta-Anzeigen vor. Die Anzeigen nutzen die Einstiegsfragen aus seinem Wissen und Anlässe aus den Marktdaten, etwa Großveranstaltungen, und halten die Leitplanke „Tagesbudget höchstens 40 €“ ein. Sie landen unter „Freigaben“; geschaltet wird erst, wenn ein Meta-Werbekonto angebunden ist. Claude bekommt für die Einschätzung keine Namen und E-Mail-Adressen. Seit diesem Agenten lesen Agenten auch den Text ihrer Wissensquellen, nicht nur die Leitplanken.
- **Daten** (Seite `/daten`): Admins sehen alle Tabellen in Supabase, können darin suchen, Tippfehler korrigieren, Testzeilen löschen und alles als CSV herunterladen. Gelöscht wird erst nach einer Rückfrage, die auch sagt, was mit verschwindet (eine Region nimmt ihre Kennzahlen, Angebote und Veranstaltungen mit). Nur lesen lassen sich Agenten (Einstellungen auf der Agenten-Seite), anonyme Einzelangebote und Admins (neue Admins im Supabase-Dashboard). Freigeben oder Zurückgeben geht weiter nur über „Freigaben“, damit festgehalten wird, wer entschieden hat.

## Regeln für den Bau

- Alle Texte auf Deutsch, einfache Sprache.
- CI: Tannengrün #10312B, Creme #F6F2EA, Gold #E1A23E nur als Akzent; Schriften DM Serif Display, Inter, DM Mono. Kein Blau.
- Die Datenbank wächst mit jeder Funktion mit: neue Daten bekommen eine nummerierte Migration.
- Beta-Regel: Jeder Report und jede Budgetänderung über 20 % braucht menschliche Freigabe.

Die Anforderungen im Detail stehen im [[Pflichtenheft]].
