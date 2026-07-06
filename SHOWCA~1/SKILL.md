---
name: showcase-assets
description: 'Produce the visual evidence that makes work look as good as it is - hero screenshots with real content, consistent framing across the whole portfolio, short clips for interaction and motion, before/after comparisons for redesigns, and everything compressed and privacy-safe. Use this skill whenever capturing or preparing screenshots, GIFs, videos, mockups, or OG-images of a project for a portfolio, case study, GitHub README, LinkedIn post, or presentation; or when existing project images look inconsistent, blurry, or full of lorem ipsum. The visual half of case-study-writer; consistency rules from brand-kit and pixel-polish apply to the assets themselves.'
---

# Showcase Assets

Werk wordt beoordeeld via de plaatjes ervan — vaker dan via de live link. Een sterk project met wazige, inconsistente screenshots vol lorem ipsum leest als een zwak project. Goed beeldmateriaal is een ambacht met regels, en de belangrijkste is consistentie over het hele portfolio heen: de assets vormen samen één tentoonstelling, geen rommelmarkt.

## De hero shot (één per project)

Elk project krijgt één beeld dat het werk in één oogopslag verkoopt — het beste scherm, niet het eerste scherm (hierarchy-craft: één winnaar):

- **Echte content**: geen lorem ipsum, geen "Test test 123". Vul de app met geloofwaardige voorbeelddata voordat je schiet — content maakt het ontwerp af.
- **Privacy eerst**: geen echte namen, mails, adressen of klantdata in beeld (AVG én fatsoen — web-legal-kit-reflex). Vervang door voorbeelddata; blurren oogt rommelig, faken oogt af.
- **Scherp**: schiet op hoge resolutie (2x), toon verkleind — nooit een klein screenshot opblazen.
- De staat klopt: geen half geladen spinners, geen devtools open, geen 3 notificatie-badges, consistente (licht/donker) modus.

## Framing: kies één stijl voor ALLES

Browser-frame voor websites, device-frame voor mobiel — prima. Maar: één stijl, één achtergrond-aanpak, één schaduw (pixel-polish), voor het hele portfolio. Vijf mockup-stijlen door elkaar maken vijf projecten tot rommel; dezelfde framing maakt ze tot een oeuvre (brand-kit-consistentie). Subtiel frame boven spektakel-mockup: het werk is de ster, de lijst hoort niet op te vallen.

## Beweging: clips voor interactie

Motion en interactie (motion-craft-werk!) verdienen bewegend bewijs — een statisch screenshot van een animatie bewijst niets:

- **Kort en gericht**: 5–15 seconden, één interactie per clip. Geen zwabberende cursor, geen zoektocht door de app — script de handeling, neem twee keer op, gebruik de strakke take.
- **Formaat**: mp4/webm boven zware GIF (factor 10 kleiner — speed-craft); autoplay + muted + loop op de portfoliopagina, met vaste afmetingen tegen layout shift.
- Begin en eindig in rust, zodat de loop niet schokt.

## Before/after (voor redesigns)

Zelfde sectie, zelfde viewport, zelfde zoom — anders vergelijkt de lezer appels met de fotografie in plaats van het ontwerp. Naast elkaar met labels, of een slider. De "before" mag lelijk zijn (dat is het punt) maar wel scherp en eerlijk: een bewust verpeste before doorziet iedereen.

## Technische pass (voor publicatie)

- [ ] Compressie: hero < 200KB, WebP/AVIF, video's < 2MB per clip (speed-craft budget geldt óók voor het portfolio zelf — juist daar)
- [ ] `width`/`height` op elk beeld (CLS), lazy loading onder de vouw, hero mét prioriteit
- [ ] Alt-teksten die het werk beschrijven ("dashboard met weekplanning voor sportclub" — a11y én vindbaarheid)
- [ ] Bestandsnamen die iets betekenen (`sportclub-booking-dashboard.webp`, niet `Screenshot 2026-07-07 (3).png`)
- [ ] OG-image per case-pagina (seo-ship-kit): de hero shot met eventueel een korte titel — dit beeld IS je linkpreview op LinkedIn

## Hiërarchie van bewijs

Werkende live demo > clip > screenshot — maar alleen als hij BLIJFT werken (prod-radar dode-link-check; een kapotte demo is erger dan geen demo). Praktische mix per case: hero shot bovenaan, één of twee clips bij de beslismomenten uit case-study-writer, live link prominent. Meer assets dan dat gaat vervelen: cureer zoals portfolio-craft cureert — beste drie beelden, rest weg.
