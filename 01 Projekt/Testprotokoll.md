---
tags: [projekt, test, pflichtenheft]
stand: 2026-10-30
---

# Testprotokoll

Erster Testlauf der Abnahmetests T1 bis T13 aus dem [[Pflichtenheft]] am 30.10.2026: 5 bestanden, 4 zur Hälfte geprüft, 4 offen. Claude hat ohne eigenen Login getestet, also über die Datenbank, die Seiten ohne Login und den Demo-Modus. Was nur mit einem Admin-Login im Browser geht, steht unten als Aufgabe.

> [!info] Wo das Ergebnis steht
> Das Ergebnis jedes Tests steht im Pflichtenheft (Claude Doc, Spalte „Ergebnis“). Diese Notiz hält fest, wie getestet wurde und was auffiel.

## Ergebnisse

| Nr. | Ergebnis | So geprüft |
| --- | --- | --- |
| T1 | zur Hälfte | Supabase-Protokoll: Lukas hat sich am 29.10. um 22:36 Uhr angemeldet. Die Begrüßung nimmt seit 30.10. den Namen aus der Admin-Liste, vorher stand dort immer „Lukas“. |
| T2 | zur Hälfte | Login-Seite zeigt „Dieses Konto ist kein Admin der hostwise engine.“; die Datenbank gibt einer fremden Adresse keine Zahlen (Kennzahlen-Funktion mit fremder Adresse aufgerufen: alles 0). |
| T3 | bestanden | engine mit echten Zugangsdaten gestartet: `/`, `/freigaben`, `/daten` und `/report/…` leiten ohne Login auf `/login`. |
| T4 | zur Hälfte | Anfrage von Nils (München) um 10:39:37 Uhr, Freigabe 40 Sekunden später, Eintrag im Live-Feed. |
| T5 | bestanden | Kurz-Check für Nils: Saisontabelle, Marktvergleich, genau 3 Tipps, Prüf-Hinweis und Rückruf-Angebot. |
| T6 | zur Hälfte | Zurückgeben speichert Stand, Name und Zeit und erscheint als Aktivität (drei Kurz-Checks am 30.10. um 01:45 Uhr). Freigegeben wurde noch nie etwas. |
| T7 | offen | Noch keine Leitplanke über die engine angelegt. |
| T8 | offen | Noch kein Agent über die engine pausiert. |
| T9 | offen | Noch keine Wissensquelle über die engine hinzugefügt. |
| T10 | offen | E-Mail-Versand (M7) ist noch nicht gebaut. |
| T11 | bestanden | Alle 10 Seiten bei 360 px und 1366 px Breite: kein seitliches Scrollen, keine Fehler. |
| T12 | bestanden | Ohne `.env.local` startet der Demo-Modus, alle Seiten laden ohne Login. |
| T13 | bestanden | Anfrage „Lukas Bosser“ als warm mit Quick-Check und Grund eingeschätzt; 3 Anzeigen mit 15, 15 und 10 € am Tag unter „Freigaben“. |

## Was ein Admin im Browser noch testen muss

Etwa 20 Minuten, am besten zu zweit (für T8):

- [ ] T1: Oskar und Maximilian melden sich an, sobald ihre Konten angelegt sind, und sehen ihren Namen in der Begrüßung.
- [ ] T2: Mit einem Konto anmelden, das nicht auf der Admin-Liste steht.
- [ ] T4: Kurz-Check-Formular ausfüllen, während das Cockpit offen ist: Hinweis, Zähler +1, Report-Agent pulsiert, Kachel „Reports diese Woche“ zählt hoch.
- [ ] T6: Einen Kurz-Check wirklich freigeben, Kachel „freigegeben“ zählt hoch.
- [ ] T7: Leitplanke für den Report-Agenten anlegen, z. B. „Nenne immer zuerst den Herbst“, dann T4 wiederholen.
- [ ] T8: Zwei Admins öffnen denselben Agenten, einer pausiert ihn.
- [ ] T9: Wissensquelle hinzufügen, Seite neu laden, auf „Wissen“ nachsehen.

## Was beim Testen auffiel

- **Kurz-Check München:** Das Stichproben-Wochenende im Winter (15.01.2027) fällt auf ein großes Konzert; der Check sagt das selbst. Die Saisons heißen dort „Nebensaison“, „Zwischensaison“ und „Hauptsaison“, obwohl für München keine Saison gemessen wurde, die das trägt.
- **Ausstattung über 100 % (behoben):** siehe [[Marktdaten-Anbieter]]. Die Preise von Amberg im Sommer enthalten noch Angebote aus der Umgebung.
- **Agenten ohne Ablauf:** Marketing, Analyse und Support stehen als „aktiv“ bzw. „pausiert“ in der engine und zeigen Beispielzahlen (12 Entwürfe, 23 Analysen, 6 Monitor-Kunden), haben aber noch keinen Ablauf in n8n.
