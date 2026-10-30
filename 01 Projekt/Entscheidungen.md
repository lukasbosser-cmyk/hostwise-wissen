---
tags: [projekt, entscheidungen]
---

# Entscheidungen

Was wir festgelegt haben, damit niemand es neu diskutieren muss. Neueste oben. Wer etwas ändert, trägt es hier mit Datum ein.

| Datum | Entscheidung | Warum | Wer |
| --- | --- | --- | --- |
| 30.10.2026 | Die engine wird online auf Netlify gehostet. Der Code bleibt auf GitHub, jeder Merge auf `main` geht automatisch online, Pull Requests bekommen eine Vorschau-Adresse. Codespaces bleibt nur zum Ausprobieren. | GitHub Pages kann keinen Login prüfen, eine Codespace-Adresse verschwindet, sobald der Codespace schläft. Netlify ist kostenlos und auch für eine Firma erlaubt. | Lukas |
| 30.10.2026 | Nächster Agent ist der Vertriebs-Agent (W1 im Pflichtenheft). Er schätzt jede Anfrage ein (heiß, warm, kalt, passendes Produkt, Rückruf) und schlägt einmal pro Woche Meta-Anzeigen vor, die das Team unter „Freigaben“ freigibt. Claude bekommt dafür keine Namen und E-Mail-Adressen. Geschaltet wird erst mit einem Meta-Werbekonto. | Der Vertrieb ist der nächste Engpass nach Report und Marktdaten; ohne Werbekonto lässt sich alles bis zur Freigabe schon bauen und testen. | Lukas |
| 30.10.2026 | Vor jedem Pull Request wird aufgeräumt: das ganze Code-Repo, dieses Vault und Supabase (Advisors, Testreste, alte Funktionen). Steht auch in der `CLAUDE.md` des Code-Repos. | Damit Code, Wissen und Datenbank nicht auseinanderlaufen und das Pflichtenheft stimmt. | Lukas |
| 30.10.2026 | Der Marktdaten-Agent sammelt pro Region auch Großveranstaltungen der nächsten 12 Monate (Weltcups, Konzerte, Festivals, Messen, große Feste). Gespeichert werden nur öffentliche Angaben: Name, Datum, Art, Größe, Quelle. | An solchen Tagen lohnen sich höhere Preise; das ist ein greifbarer Tipp im Report. | Lukas |
| 30.10.2026 | Marktdaten werden zusätzlich als anonyme Einzelangebote gespeichert (Preis pro Nacht auf 5 € und Größe auf 5 m² gerundet, Schlafzimmer, Bewertung; ohne Titel, Link, Gastgeber, genaue Lage). Die Daten sind ein Archiv: jede Saison einer Region wird einmal im Jahr gelesen, nur die nächste anstehende Saison monatlich. | Reports vergleichen so mit gleich großen Wohnungen. Saisonpreise ändern sich über die Jahre wenig, das spart Abrufe und baut einen Vorjahresvergleich auf. | Lukas |
| 29.10.2026 | Airbnb und Booking.com dürfen ausgelesen werden, aber nur Marktdaten (Preise, Belegung, Ausstattung, Bewertungsschnitt). Keine Gastgebernamen, Personenfotos oder Bewertungstexte; gespeichert wird nur zusammengefasst pro Region. Abrufe über Firecrawl in n8n. | Das sind die aussagekräftigsten Marktdaten. Risiken (AGB, Datenbankrecht, DSGVO) bewusst in Kauf genommen und durch Datensparsamkeit begrenzt. Vor dem Launch rechtlich prüfen lassen. | Lukas |
| 29.10.2026 | Gemeinsamer Wissensspeicher ist dieses Repo `hostwise-wissen`, geöffnet in Obsidian. | Kostenlos, mit Versionsverlauf, und Claude kann direkt hineinschreiben. | Lukas |
| 29.10.2026 | Agenten-Einstellungen (Status, Selbstständigkeit, Leitplanken, Wissen) liegen in Supabase; die Agenten in n8n lesen ihre Leitplanken bei jedem Durchlauf. | Das Team trainiert Agenten in der engine, ohne n8n zu öffnen. | Lukas |
| 29.10.2026 | Landingpage erst, wenn die Agenten stehen. | Erst muss der Ablauf hinter dem Formular funktionieren. | Lukas |
| 29.10.2026 | Report-Agent als fester Ablauf mit Formular in n8n, nicht als frei handelnder Agent. | Planbar, prüfbar, passt zur Beta-Regel. | Lukas |
| 29.10.2026 | Die Datenbank wächst mit jeder Funktion mit: jede neue Datenart bekommt eine nummerierte Migration, die auch auf Supabase angewendet wird. | Supabase ist das Rückgrat, keine Beispieldaten, die auseinanderlaufen. | Lukas |
| 29.10.2026 | Login nur für die drei Admins (E-Mail und Passwort über Supabase). | Interne Steuerzentrale, Kundendaten nur fürs Team. | Lukas |
| 29.10.2026 | Preise wie im Businessplan: Kurz-Check 0 €, Quick-Check 29 €, Komplett-Analyse 149 €, Monitor 39 €/Monat. | Besser als das Modell aus dem Kurs-Deck (0 €/99 €/9 €). | Lukas |
| 29.10.2026 | Idee „Stations-Cockpit“ (Tankstellen) wird nicht weiterverfolgt. | Fokus auf hostwise. | Lukas |
| 29.10.2026 | CI für alles: Tannengrün #10312B, Creme #F6F2EA, Gold #E1A23E als Akzent; DM Serif Display, Inter, DM Mono. Kein Blau, keine typische KI-Optik. | Einheitlicher Auftritt von Deck, Docs und engine. | Lukas |
| 29.10.2026 | Beta-Regel: jeder Report und jede Budgetänderung über 20 % braucht eine menschliche Freigabe. | Vertrauen und Qualität, solange die Agenten lernen. | Team |
