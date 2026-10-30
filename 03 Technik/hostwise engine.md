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
| Agent | Überblick, Training (Wissen, Leitplanken, Selbstständigkeit), Verbindungen, Verlauf |
| Freigaben | Ergebnisse prüfen und freigeben oder zurückgeben |
| Marktdaten | Preise je Saison von Airbnb und Booking.com, Großveranstaltungen und Ausstattung pro Region; Regionen aufnehmen oder pausieren |
| Wissen | Alle Wissensquellen |
| Einstellungen | Platzhalter |

## Stand 30.10.2026

- **Login:** nur die drei Admins (E-Mail und Passwort). Oskar und Maximilian brauchen noch ein Konto, das Lukas im Supabase-Dashboard anlegt.
- **Freigaben und Aktivität** kommen live aus Supabase.
- **Agenten-Einstellungen** (Pause, Selbstständigkeit, Leitplanken, Wissen, Anbinden) werden gespeichert und erscheinen bei allen Admins ohne Neuladen. Seit Pull Request #2 (29.10.2026) in der engine.
- **Report-Agent** in n8n: Formular „Kurz-Check“ → Anfrage in Supabase → Claude schreibt den Kurz-Check → wartet in der engine unter „Freigaben“. Er liest die Leitplanken aus der engine bei jedem Durchlauf neu. Der Ablauf ist gebaut und getestet, aber noch nicht veröffentlicht.
- **Report-Agent** rechnet seit 30.10.2026 mit echten Marktdaten: Er ruft den Marktdaten-Agenten auf und bekommt Preise je Saison, den Vergleich mit gleich vielen Schlafzimmern und die Großveranstaltungen der Region. Das Formular fragt dafür optional nach der Zahl der Schlafzimmer.
- **Marktdaten-Agent** (n8n-Workflow „hostwise · Scraping-Agent (Marktdaten)“): liest pro Region und Saison ein Wochenende (Fr–So, 2 Gäste) auf Airbnb und Booking.com über Firecrawl, speichert Kennzahlen und anonyme Einzelangebote und sucht einmal im Monat die Großveranstaltungen. Läuft am 1. jedes Monats für alle aktiven Regionen und auf Abruf des Report-Agenten. Erste Region: Garmisch-Partenkirchen. Wie genau, steht in [[Marktdaten-Anbieter]].
- **Noch offen:** Beide Workflows in n8n veröffentlichen (Publish im Editor), sonst laufen Formular und Monatslauf nicht von selbst.

## Regeln für den Bau

- Alle Texte auf Deutsch, einfache Sprache.
- CI: Tannengrün #10312B, Creme #F6F2EA, Gold #E1A23E nur als Akzent; Schriften DM Serif Display, Inter, DM Mono. Kein Blau.
- Die Datenbank wächst mit jeder Funktion mit: neue Daten bekommen eine nummerierte Migration.
- Beta-Regel: Jeder Report und jede Budgetänderung über 20 % braucht menschliche Freigabe.

Die Anforderungen im Detail stehen im [[Pflichtenheft]].
