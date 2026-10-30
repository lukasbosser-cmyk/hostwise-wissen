---
tags: [technik, konten, werkzeuge]
stand: 2026-10-30
---

# Tools und Konten

Welche Werkzeuge wir nutzen, wer Zugang hat und wo Schlüssel liegen.

> [!danger] Keine Passwörter oder API-Schlüssel in dieses Vault
> Das Repo wird geklont und synchronisiert. Schlüssel gehören nur in die Zugangsdaten des jeweiligen Werkzeugs (z. B. n8n Credentials) oder in eine lokale `.env.local`, die nie committet wird.

| Werkzeug | Wofür | Konto / Zugang | Wo liegen Schlüssel |
| --- | --- | --- | --- |
| GitHub | Code (`hostwisedemo`) und dieses Vault (`hostwise-wissen`) | Konto von Lukas, Oskar und Maximilian werden eingeladen | keine im Repo |
| Supabase | Datenbank, Login, Live-Updates | Projekt „hostwise“, Frankfurt, kostenloser Tarif | Öffentlicher Schlüssel in `.env.local`; der geheime Service-Schlüssel nur in n8n |
| n8n Cloud | Abläufe der Agenten | hostwise.app.n8n.cloud | n8n Credentials |
| Firecrawl | Webseiten und Portale auslesen | Konto von Lukas, 1.000 Credits pro Monat kostenlos | nur n8n Credential |
| Claude | Bauen, Schreiben, Agenten-KI | KI in n8n läuft über n8n-Guthaben, kein eigener Schlüssel | – |
| Obsidian | Dieses Vault lesen und bearbeiten | Konto von Lukas | – |
| Meta Business (Facebook, Instagram) | Anzeigen des Vertriebs-Agenten schalten | noch nicht angelegt; bis dahin schlägt der Agent Anzeigen nur vor | später nur n8n Credential |

## Supabase

- Admins dürfen sich anmelden, sonst niemand. Die Liste steht in der Tabelle `admins`.
- Passwörter setzt Lukas im Supabase-Dashboard unter Authentication → Users, nie im Chat.
- Jede neue Datenart bekommt eine nummerierte Migration im Code-Repo unter `supabase/migrations/`.

## n8n

- Supabase-Zugang: Credential „Supabase account“.
- Firecrawl-Zugang: Credential vom Typ „Firecrawl API“. **Base URL muss `https://api.firecrawl.dev/v2` sein**, sonst meldet Firecrawl „Not Found“.
- Test-Ablauf „hostwise · Firecrawl-Test“: eine Suche mit drei Treffern, kostet 2 Credits.
- Report-Agent und Marktdaten-Agent (Workflow „hostwise · Scraping-Agent (Marktdaten)“): veröffentlicht seit 30.10.2026.
- Vertriebs-Agent (Workflow „hostwise · Vertriebs-Agent (Leads und Anzeigen)“): gebaut und getestet am 30.10.2026, wartet auf Veröffentlichung im n8n-Editor. Ein Lauf kostet nur KI-Guthaben, wenn es neue Anfragen gibt oder Anzeigen fällig sind.

## Obsidian und dieses Vault

Siehe [[README]] auf der Startseite. Kurz: Repo mit GitHub Desktop klonen, in Obsidian „Ordner als Vault öffnen“, vor dem Arbeiten „Pull“, danach „Commit“ und „Push“.

## Hosting

Die engine läuft auf **Netlify** (kostenloser Tarif). Netlify ist mit dem GitHub-Repo `hostwisedemo` verbunden und baut bei jedem Merge auf `main` automatisch neu; für jeden Pull Request gibt es eine eigene Vorschau-Adresse. Die Einstellungen stehen in `netlify.toml` im Repo.

- Die beiden Supabase-Werte (Adresse und öffentlicher Schlüssel, siehe `.env.example`) stehen im Netlify-Dashboard unter *Site configuration → Environment variables*. Fehlen sie, zeigt die Online-Version nur den Demo-Modus.
- In Supabase steht die Netlify-Adresse unter *Authentication → URL Configuration* als Site URL.
- Warum nicht GitHub Pages: Pages zeigt nur fertige Dateien an. Die engine braucht aber einen Server, der bei jedem Aufruf den Login prüft.
- Warum nicht Vercel: Der kostenlose Tarif ist nur für nicht-kommerzielle Projekte gedacht.

> [!info] Codespaces ist kein Hosting
> In einem GitHub Codespace startet die engine mit `npm install` und `npm run dev` im Browser. Die Adresse gilt aber nur, solange der Codespace läuft (er schläft nach 30 Minuten ohne Nutzung ein). Zum schnellen Ausprobieren gut, als feste Adresse für Team und Pitch nicht.
