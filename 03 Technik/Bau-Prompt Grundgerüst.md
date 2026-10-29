# Prompt: Grundgerüst der hostwise engine

> Diesen Prompt kannst du 1:1 in Claude Code (lokal oder im Web) einfügen, um das Grundgerüst neu aufzubauen oder zu erweitern. Der aktuelle Stand im Repo wurde genau nach diesem Prompt gebaut.

---

## Rolle und Ziel

Du bist Senior-Frontend-Entwickler und Produktdesigner für **hostwise**. hostwise verkauft Ferienimmobilien-Besitzern Reports, die zeigen, wie sie mehr aus ihrer Unterkunft holen (Preise, Auslastung, Inserat). Das Unternehmen soll zu etwa 90 % von KI-Agenten betrieben werden. Baue das Grundgerüst der **hostwise engine**: das zentrale "Gehirn"-Dashboard, in dem der Gründer alle Agenten sieht, trainiert, anbindet und ihre Ergebnisse freigibt.

Das Ergebnis ist ein **klickbarer Demonstrator** (Kurs-Abgabe 08.12.2026) mit realistischen Beispieldaten, der später Schritt für Schritt an Supabase und echte Agenten angeschlossen wird. Das Pflichtenheft ist am 10.11.2026 fällig, die Struktur soll es also gut abbilden.

## Tech-Stack

- **Next.js 16** (App Router, TypeScript, `src/`-Verzeichnis, Alias `@/*`). Lies vor dem Coden `node_modules/next/dist/docs/` (siehe `AGENTS.md`), weil sich APIs geändert haben (z. B. `params` ist ein Promise, Cache Components sind aktiv).
- **Tailwind CSS v4** mit Design-Tokens per `@theme` in `globals.css`.
- **motion** (`motion/react`, Nachfolger von Framer Motion) für alle Animationen.
- **lucide-react** für Icons (Strichstärke 1.75).
- **Supabase** (`@supabase/supabase-js`, `@supabase/ssr`), Projekt "hostwise" (Frankfurt, eu-central-1). Im Grundgerüst nur Client-Setup, `.env.example` und ein SQL-Schema unter `supabase/migrations/`. Noch nichts live anwenden.
- Hosting später auf **Netlify** (Vercel Hobby ist nicht-kommerziell).
- Keine weiteren UI-Bibliotheken (kein shadcn, kein MUI). Eigene, schlanke Komponenten.

## Corporate Identity (verbindlich, wie im Businessplan und in allen Decks)

Farben als Tokens:

| Token | Hex | Einsatz |
|---|---|---|
| `ink` | `#10312B` | Haupttext, Sidebar, dunkle Flächen |
| `cream` | `#F6F2EA` | Seitenhintergrund |
| `gold` | `#E1A23E` | Akzent, aktive Zustände, Logo |
| `gold-dark` | `#B8862F` | Hover auf Gold |
| `gold-tint` | `#F5E6C8` | Hinterlegung für Hinweise |
| `muted` | `#5C6B66` | Sekundärtext |
| `line` | `#D9D4C7` | Trennlinien |
| `sand` | `#ECE5D6` | Flächen, Skeletons |
| `card` | `#FFFDF8` | Karten, Rand `#E3DCCD` |
| `green` | `#2E8B67` | Erfolg, "aktiv" |
| `green-tint` | `#DDEDE3` | Erfolgs-Hinterlegung |
| `ink-card` | `#16382F` | Karten auf dunklem Grund |
| `ink-grid` | `#1A423A` | Rasterlinien auf dunklem Grund |
| `ink-text` | `#C6CFC7` | heller Text auf dunklem Grund |

Schriften (liegen als Dateien bei, per `next/font/local` einbinden):
- **DM Serif Display** für Headlines.
- **Inter** (Regular, Bold) für UI und Fließtext.
- **DM Mono** für Kicker-Labels (VERSALIEN, Sperrung ca. 0.14em), Zahlen und Status.

Logo: goldenes, abgerundetes Quadrat mit dunklem Haus und steigender Zickzack-Linie (`public/hw_icon.png`), Wortmarke "hostwise." mit goldenem Punkt, daneben "engine" in DM Mono.

Regeln: kein Blau, keine typische KI-Optik (keine Neon-Verläufe, kein Lila, keine Glitzer-Sterne). Gold nur als Akzent, nie für kleinen Text auf Creme (Kontrast). Ruhig, hochwertig, "Privatbank trifft Landhaus".

## Bedienung (sehr intuitiv)

- Linke Sidebar (dunkel, `ink`) mit maximal 5 Hauptpunkten: **Cockpit**, **Agenten**, **Freigaben** (mit Zähler-Badge), **Wissen**, **Einstellungen**. Aktiver Punkt mit goldenem Indikator, der animiert zwischen den Einträgen gleitet.
- Auf dem Handy wird die Sidebar zur unteren Tab-Leiste.
- **Befehlspalette** mit `⌘K` / `Strg+K`: Agenten und Seiten suchen und direkt springen.
- Jede Seite beginnt mit Kicker, Serif-Headline und einem Satz, der erklärt, was man hier tut.
- Einfache Sprache, keine Fachbegriffe ("Freigeben" statt "Approve", "Selbstständigkeit" statt "Autonomy Level").
- Leere Zustände erklären den nächsten Schritt. Jede Aktion gibt sichtbares Feedback (Toast unten rechts).
- Tastatur-bedienbar, sichtbare Fokus-Ringe in Gold, `prefers-reduced-motion` wird respektiert.

## Seiten

1. **Cockpit** (`/`)
   - Begrüßung mit Tageszeit ("Guten Abend, Lukas").
   - 4 Kennzahlen-Kacheln mit hochzählenden Zahlen: Reports diese Woche, offene Freigaben, neue Leads, Werbebudget heute.
   - **Engine-Kern**: große, dunkle Visualisierung. Das hostwise-Logo als atmendes Zentrum, alle Agenten als Knoten auf einem Ring. Verbindungslinien, auf denen kleine goldene Impulse zwischen Agent und Zentrum wandern, wenn ein Agent arbeitet. Langsam rotierender Orbit-Ring. Klick auf einen Knoten öffnet den Agenten.
   - **Live-Aktivität**: Feed, in den alle paar Sekunden neue Ereignisse animiert hineingleiten.
   - **Wartet auf dich**: die nächsten 3 Freigaben mit Direkt-Buttons.

2. **Agenten** (`/agenten`)
   - Übersicht aller Agenten, die man trainieren oder anbinden kann.
   - Filter-Tabs: Alle, Aktiv, Im Training, Pausiert, Verfügbar. Beim Filtern ordnen sich die Karten animiert neu (Layout-Animation).
   - Karte pro Agent: Icon, Name, Aufgabe in einem Satz, Status mit pulsierendem Punkt, Trainingsstand als animierter Ring, Selbstständigkeit (Vorschlagen / Mit Freigabe / Selbstständig), Kennzahl der letzten 7 Tage, Mini-Verlauf (Sparkline).
   - Hover: Karte hebt sich leicht, goldene Kante.
   - Bereich **"Agent anbinden"** mit verfügbaren Agenten und Integrationen (z. B. Google Ads, E-Mail-Postfach, Rückruf-Kalender, Buchhaltung). Klick startet einen 3-Schritte-Assistenten im Modal: Was soll er tun → Womit verbinden → Wie selbstständig.

3. **Agent-Detail** (`/agenten/[id]`)
   - Kopf mit Status-Schalter (aktiv/pausiert, animiert).
   - Tabs: **Überblick** (Kennzahlen, letzte Aufgaben), **Training** (Wissensquellen hinzufügen, Beispiele bewerten mit Daumen hoch/runter, Leitplanken als Schalter, Regler für Selbstständigkeit), **Verbindungen** (angebundene Dienste mit Status), **Verlauf** (Zeitstrahl).
   - Tab-Wechsel mit gleitendem Unterstrich.

4. **Freigaben** (`/freigaben`)
   - Warteschlange aller Ergebnisse, die ein Mensch prüfen muss (in der Beta jeder Report, Budgetänderungen über 20 %).
   - Karte mit Vorschau, Agent, Begründung und Buttons "Freigeben" / "Zurückgeben". Beim Freigeben gleitet die Karte nach rechts in Grün weg, beim Zurückgeben nach links, der Rest rückt animiert nach.
   - Leerer Zustand: "Alles erledigt" mit kleiner Animation.

5. **Wissen** und **Einstellungen**: einfache Platzhalter mit sinnvollem leeren Zustand und dem Hinweis, was hier kommt.

## Agenten (Beispieldaten)

| ID | Name | Aufgabe | Status |
|---|---|---|---|
| `vertrieb` | Vertrieb | Schaltet Meta-Ads, qualifiziert Leads, bucht Rückrufe | aktiv, mit Freigabe |
| `marketing` | Marketing | Schreibt Beiträge, Newsletter und Landingpage-Texte | aktiv, vorschlagen |
| `scraping` | Marktdaten | Sammelt Preise und Auslastung vergleichbarer Unterkünfte | im Training |
| `analyse` | Analyse | Berechnet Saisonpreise, Marktvergleich und Score | aktiv, mit Freigabe |
| `report` | Report | Erstellt Kurz-Check, Quick-Check und Komplett-Analyse als PDF | aktiv, mit Freigabe |
| `support` | Support & Monitor | Beantwortet Fragen, überwacht Monitor-Kunden | pausiert |

Verfügbar zum Anbinden: Bewertungs-Agent (Gästebewertungen auswerten), Foto-Agent (Inseratsfotos bewerten), Buchhaltung (Rechnungen), Google Ads.

Produkte für Beispieldaten: Kurz-Check 0 €, Quick-Check 29 €, Komplett-Analyse 149 €, Monitor 39 €/Monat. Beispiel-Kunden aus den Interview-Personas (Monika in Garmisch, Thomas auf Usedom, Petra in Lindau, Sabine im Allgäu, Jonas im Harz).

Inhaltliche Leitplanken aus den Interviews, die als Trainings-Leitplanken auftauchen: Saisonpreis-Tabelle und Marktvergleich vor den Score, Rechenweg und Datenquellen offenlegen, einfache Sprache, jeder Report mit Prüf-Hinweis und Rückruf-Angebot.

## Animationen (Agenten-Dashboard)

Alle mit `motion/react`, weich und ruhig (Federn mit `stiffness` ca. 260, `damping` ca. 30, Dauer 0.3 bis 0.6 s):
- Seitenwechsel: sanftes Einblenden mit 8 px Aufwärtsbewegung.
- Karten erscheinen gestaffelt (Stagger 0.05 s).
- Engine-Kern: atmendes Zentrum, rotierender Orbit, wandernde Impulse auf den Linien, Knoten skalieren beim Hover.
- Status-Punkt pulsiert bei aktiven Agenten.
- Trainingsring zeichnet sich beim Erscheinen.
- Zahlen zählen hoch.
- Filter: Layout-Animation, Karten blenden ein und aus.
- Sidebar-Indikator und Tab-Unterstrich gleiten per `layoutId`.
- Freigaben gleiten seitlich heraus, Liste rückt nach.
- Live-Feed: neue Einträge gleiten von oben herein.
- `MotionConfig reducedMotion="user"` global.

## Architektur

```
src/
  app/
    layout.tsx            Schriften, Shell, Provider
    template.tsx          Seitenübergang
    page.tsx              Cockpit
    agenten/page.tsx
    agenten/[id]/page.tsx
    freigaben/page.tsx
    wissen/page.tsx
    einstellungen/page.tsx
    fonts/                lokale Schriftdateien
  components/
    shell/                Sidebar, MobileNav, CommandPalette, Logo
    engine/               EngineCore, ActivityFeed, KpiTile
    agents/               AgentCard, AgentGrid, ConnectWizard, TrainingRing, Sparkline, StatusDot
    approvals/            ApprovalCard, ApprovalList
    ui/                   Button, Badge, Tabs, Toggle, Toast, PageHeader, EmptyState
  lib/
    data.ts               Beispieldaten (Agenten, Freigaben, Aktivität)
    types.ts              Typen
    store.tsx             Client-State (React Context): Freigaben, Agenten-Status, Toasts
    supabase/client.ts    Browser-Client (nur wenn Env-Variablen gesetzt)
supabase/migrations/0001_engine.sql   Tabellen agents, agent_connections, training_sources, guardrails, approvals, activity (mit RLS)
```

Daten fließen im Grundgerüst aus `lib/data.ts` in einen Client-Store, damit alle Klicks echt wirken. Die Typen entsprechen dem SQL-Schema, sodass später nur die Datenquelle getauscht wird.

## Qualität

- `npm run build` und `npm run lint` laufen fehlerfrei.
- Responsiv ab 360 px Breite.
- Alle Texte auf Deutsch.
- README mit Start-Anleitung (`npm install`, `npm run dev`) und Hinweis auf `.env.example`.
- Keine Geheimnisse committen.

## Nicht im Grundgerüst

Echte KI-Aufrufe, Login, Zahlungen, echtes Scraping (rechtlich bei Airbnb/Booking ungeklärt), Supabase-Migration live anwenden. Das kommt in späteren Schritten.
