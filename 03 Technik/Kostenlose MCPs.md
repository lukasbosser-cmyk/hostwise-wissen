---
tags: [technik, mcp, werkzeuge]
stand: 2026-10-29
---

# Kostenlose MCPs für hostwise

> [!info] Lebende Fassung
> Kopie vom 29.10.2026. Original im Claude Doc: [Kostenlose MCPs für hostwise](https://claude.ai/artifact/Dwgb4FrQVK8UAimuBYbFHh).

MCPs sind Anschlüsse, über die Claude direkt mit einem Werkzeug arbeiten kann, etwa mit GitHub oder Supabase.

## Empfehlungen

Für den Start reichen vier MCPs: **GitHub, Supabase, Context7 und Playwright**. Alle sind für hostwise kostenlos nutzbar. Die übrigen kommen dazu, sobald Zahlungen, Mails, Ads und Marktdaten anstehen. Brave Search fehlt bewusst: Der kostenlose Tarif wurde 2026 abgeschafft, es gibt nur noch ein Guthaben von 5 $ pro Monat mit hinterlegter Karte ([Quelle](https://www.implicator.ai/brave-drops-free-search-api-tier-puts-all-developers-on-metered-billing.md)).

| MCP | Wofür bei hostwise | Kosten | Wann |
| --- | --- | --- | --- |
| GitHub | Repo hostwisedemo, Issues als Backlog, Pull Requests | kostenlos | sofort |
| Supabase | Tabellen customers, properties, orders, reports anlegen und abfragen, Auth, Storage | kostenlos im Free Plan | sofort |
| Context7 | Aktuelle Doku zu Next.js, Supabase und Stripe während des Codens | kostenlos | sofort |
| Playwright | Funnel automatisch durchklicken: Landingpage → Checkout → Formular → Report | kostenlos, Open Source | sofort |
| Stripe | Produkte für 29 €, 149 € und 39 €/Monat anlegen, Checkout und Webhooks testen | kostenlos, Stripe nimmt nur Transaktionsgebühren | ab Checkout |
| Resend | Zustellmails für Reports und Upsell-Mails | kostenlos im Free Plan | ab Zustellung |
| n8n-mcp | Kennt alle n8n-Nodes und hilft, die Workflows (Kauf, Analyse, Upsell) zu bauen | kostenlos, Open Source | ab Automatisierung |
| Meta Ads MCP (Pipeboard) | Kampagnen-KPIs abrufen, Budgets verschieben, Creatives testen – der Kern des Vertriebs-Agenten | selbst gehostet kostenlos, gehostet mit Free Plan ([Quelle](https://github.com/pipeboard-co/meta-ads-mcp)) | ab Ads |
| Firecrawl | Webseiten von Wettbewerbern, Tourist-Infos und Event-Kalendern auslesen | 1.000 Credits pro Monat kostenlos ([Quelle](https://webscraping.ai/faq/firecrawl/is-firecrawl-free-and-what-are-the-free-tier-limitations)) | ab Marktdaten |
| Fetch | Einzelne Webseiten als Text holen, einfacher Ersatz für eine Such-API | kostenlos, Open Source | jederzeit |
| Notion | Content-Bibliothek: Report-Bausteine, Ad-Varianten, FAQ | kostenlos für Einzelnutzer | optional |
| Chrome DevTools | Ladezeit und Fehler der Landingpage prüfen | kostenlos, Open Source | optional |

> [!warning] Überholt seit 29.10.2026
> Im Original steht, dass Airbnb und Booking.com erst ausgelesen werden, wenn eine legale Marktdatenquelle geklärt ist. Das gilt nicht mehr: Lukas hat entschieden, dass beide ausgelesen werden dürfen, aber nur Marktdaten und zusammengefasst pro Region. Siehe [[Entscheidungen]] und [[Marktdaten-Anbieter]]. Firecrawl läuft inzwischen direkt in n8n, nicht als MCP in Claude Code.

Der kostenlose Hobby-Tarif von Vercel ist nur für nicht-kommerzielle Projekte gedacht. Für den Live-Betrieb ist Netlify oder ein bezahlter Tarif die sichere Wahl.

## Einrichtung in Claude Code

Im Ordner des Repos ausführen. Mit `--scope project` landen die Server in einer `.mcp.json` im Repo, sodass Oskar und Maximilian dieselben MCPs bekommen. API-Keys gehören nicht ins Repo, sondern in Umgebungsvariablen.

**Sofort** (ist im Repo `hostwisedemo` bereits in der `.mcp.json`, außer GitHub)

```bash
claude mcp add --scope project --transport http github https://api.githubcopilot.com/mcp -H "Authorization: Bearer ${GITHUB_PAT}"
claude mcp add --scope project --transport http supabase "https://mcp.supabase.com/mcp?read_only=true"
claude mcp add --scope project --transport http context7 https://mcp.context7.com/mcp
claude mcp add --scope project playwright -- npx @playwright/mcp@latest
```

**Später**

```bash
claude mcp add --scope project --transport http stripe https://mcp.stripe.com
claude mcp add --scope project n8n-mcp -e MCP_MODE=stdio -e LOG_LEVEL=error -e DISABLE_CONSOLE_OUTPUT=true -- npx n8n-mcp
claude mcp add --scope project firecrawl -e FIRECRAWL_API_KEY=${FIRECRAWL_API_KEY} -- npx -y firecrawl-mcp
claude mcp add --scope project fetch -- uvx mcp-server-fetch
claude mcp add --scope project --transport http notion https://mcp.notion.com/mcp
claude mcp add --scope project chrome-devtools -- npx chrome-devtools-mcp@latest
```

Meta Ads MCP und Resend werden nach der Anleitung im jeweiligen Repository eingerichtet, weil sie eine eigene Meta-App bzw. einen Resend-Key brauchen. Supabase zuerst nur lesend (`read_only=true`) verbinden und Stripe im Testmodus nutzen, bis der Funnel steht. Nach dem Hinzufügen in Claude Code `/mcp` aufrufen und bei Supabase, Stripe und Notion einmal einloggen.
