---
name: dependency-scout
description: 'Evaluate a library, framework, API, or SaaS before adopting it - health signals (releases, maintainers, issues), true cost (bundle size, transitive deps, pricing at 10x usage), license check, lock-in assessment, and an exit plan, ending in a short documented recommendation. Use this skill BEFORE adding any dependency or external service to a project; whenever the user asks "welke library", "React of Vue", "Supabase of Firebase", "is dit pakket veilig", or wants to replace something. Also for auditing an existing dependency list. Research half per research-rigor; security red flags escalate to web-security-gates.'
---

# Dependency Scout

Every dependency is a small marriage: je erft de bugs, het release-tempo, de prijsverhogingen en het einde-van-onderhoud van iemand anders. The choice takes an hour of scouting; a bad one costs a rewrite. This skill front-loads that hour and documents the decision so it never gets relitigated (project-continuity).

## Step 0 — Does this need a dependency at all?

The best dependency is none. Ask first:

- Kan ~30 regels eigen code dit? Een datum formatteren, een debounce, een simpele carousel — daarvoor haal je geen 300KB binnen (speed-craft JS-budget).
- Kan het platform het al? Moderne browser-APIs en CSS dekken veel waar vroeger libraries voor nodig waren.
- Vuistregel: een dependency moet ~10× zijn kosten opleveren. Twijfel = zelf schrijven; de rule of three (component-craft) geldt ook hier.

## Step 1 — Health check (10 minutes, hard signals)

Voor libraries/frameworks — check de repo en registry, niet de marketing:

- **Pols**: laatste release en commits — maanden stilte op een actief-gebruikt pakket is een signaal; jaren = kies iets anders (uitzondering: klein en ÁF kan prima zijn).
- **Busfactor**: één maintainer = één vakantie/burn-out verwijderd van stilstand. Team of organisatie erachter weegt zwaarder.
- **Issues/PRs-trend**: groeit de open stapel zonder reactie? Reageren maintainers op bugmeldingen?
- **Adoptie**: downloads en afhankelijke projecten — populariteit is geen kwaliteit, maar wel garantie op documentatie, antwoorden en opvolgers.
- **Docs**: 15 minuten docs lezen voorspelt de hele relatie. Geen migration guides bij breaking changes = pijn later.

## Step 2 — True cost

- **Gewicht**: bundle-impact gecomprimeerd (bundlephobia-achtige check) en het aantal transitieve dependencies dat meelift — je installeert nooit één pakket.
- **Breaking-change-historie**: hoe vaak braken majors de API? Dat is jouw toekomstige migratie-agenda.
- **Voor APIs/SaaS — reken de prijs bij 10× gebruik**: gratis tiers zijn marketing; de vraag is wat het kost als het wérkt. Check ook: rate limits, uptime-status-historie, en data-locatie (EU? — web-legal-kit wil het weten voor de privacyverklaring).

## Step 3 — Security & license (blockers, no judgment calls)

- Bekende kwetsbaarheden check (`npm audit` / advisory database); install-scripts bij twijfelachtige pakketten zijn een rode vlag.
- **Exacte naam** — typosquatting bestaat: `lodash` vs `1odash`. Kopieer de naam van de officiële bron, nooit uit een forum-antwoord.
- **Licentie**: MIT/Apache/BSD/ISC = vrij te gebruiken. (A)GPL of "non-commercial" op iets dat in een commercieel product gaat = juridische vraag, geen technische — flag het (web-legal-kit grens: bij twijfel jurist).
- Rode vlaggen hier zijn diskwalificerend, hoe mooi de feature-lijst ook is. Escaleer patronen naar web-security-gates.

## Step 4 — Lock-in & exit plan

Vraag vóór adoptie: hoe komen we er ooit weer VANAF?

- Hoe diep raakt het de codebase? Een utility raakt niets; een framework raakt alles. Middencategorie (date-libs, HTTP-clients, analytics): wikkel achter een eigen interface (`lib/dates.js`) zodat vervangen één bestand kost — component-craft compositie.
- Voor SaaS: is er data-export? Open standaard? Een dienst zonder exportpad verdient extra wantrouwen bij prijswijzigingen — jouw data is dan hun onderhandelingspositie.
- Schrijf het exit-plan in één zin op. Kan dat niet, dan is de lock-in het echte prijskaartje.

## Deliver — the one-paragraph verdict

```markdown
**Keuze**: [pakket X versie Y] voor [taak]
**Waarom**: gezond onderhoud (laatste release <datum>), 12KB, MIT, team-maintained — [2-3 doorslaggevende feiten met bron]
**Afgewezen**: [Y] (1 maintainer, 2 jaar stil), [Z] (AGPL)
**Exit**: gewrapt in lib/x.js; alternatief is [Y] — omschakelen kost ~een dag
```

Log het in PROJECT.md Beslissingen. Vergelijk maximaal 2–3 serieuze kandidaten diep — een matrix van tien opties is uitstelgedrag met celranden. En herhaal de check kort bij major upgrades: een dependency die van eigenaar of licentie wisselt, is een nieuwe dependency.
