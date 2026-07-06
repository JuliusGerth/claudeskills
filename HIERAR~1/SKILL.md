---
name: hierarchy-craft
description: 'Control what the eye sees first, second, and third on every screen - one primary message per view, contrast via size/weight/color/position, grouping by whitespace instead of boxes, alignment to invisible lines, and deliberate de-emphasis of everything secondary. Use this skill when composing ANY screen or page layout, and whenever a design feels "druk", "onrustig", "je weet niet waar je moet kijken", everything competes for attention, or important actions get overlooked. Sits between ui-concept-forge (which picks the visual direction) and pixel-polish (which perfects the details) - this skill decides the ORDER in which a screen communicates.'
---

# Hierarchy Craft

A screen is read in a fraction of a second before it is read at all: the eye lands, jumps to the loudest elements, and forms a judgment. Design that order deliberately, or it happens by accident — and accidental hierarchy is why screens feel "druk" and CTAs get missed. The discipline: per screen, decide what must win, make it win, and make everything else lose gracefully.

## Step 1 — One screen, one winner

Before styling anything, answer: what is the ONE thing this screen must communicate, and the ONE action most users should take? (feature-spec / ux-blueprint know.) That element wins the visual contest. Two winners = no winner: when everything is groot, vet en gekleurd, is niets het.

This also settles button policy: één primaire knop per view; alle andere acties zijn secundair (outline/ghost) of tertiair (tekstlink). Twee primaries naast elkaar ("Opslaan" én "Versturen" allebei vol accent) dwingen de gebruiker te raden wat jij belangrijk vindt.

## Step 2 — The contrast toolbox (in order of power)

Make the winner win using these levers — a couple used decisively beat all five used timidly:

1. **Grootte**: het krachtigste signaal. De hero-kop mag 2–3× de broodtekst zijn; een timide 1.2× zegt niets. Max 3 grootte-niveaus per scherm (pixel-polish schaal) — meer niveaus = geen niveaus.
2. **Gewicht**: vet voor het belangrijkste woord of getal, niet voor hele zinnen. In dashboards: het getal groot en vet, het label klein en muted (data-viz-craft).
3. **Kleur**: accent trekt de blik — daarom is accent alléén voor het belangrijkste interactieve element (theme-craft token-regel). Accent als sfeerkleur overal = accent nergens.
4. **Positie**: bovenaan en (in LTR) links wint; de eerste fixatie landt daar. Het belangrijkste nieuws staat niet onder de vouw van het eigen scherm.
5. **Witruimte**: ruimte rondom = spotlight. Het element met de meeste lege ruimte eromheen voelt automatisch het belangrijkst — gratis nadruk zonder extra decoratie.

## Step 3 — Group by space, not by boxes

Wat bij elkaar hoort, staat dichter bij elkaar dan bij de rest — proximity groepeert sterker dan kaders en lijnen. De vuistregel die schermen opruimt: **afstand-binnen < afstand-tussen** (label dicht op zijn veld, ver van het vorige veld; kaarttitel dicht op zijn kaartinhoud). Meestal kunnen de meeste borders en dividers weg zodra de spacing dit doet — elke lijn die spacing kan vervangen is visuele ruis (pixel-polish ruimt de rest).

Consistentie is zelf een signaal: elementen die er hetzelfde uitzien, beloven hetzelfde gedrag. Drie knopstijlen voor dezelfde soort actie breken die belofte.

## Step 4 — Align everything to something

Onzichtbare lijnen maken rust: elk element deelt zijn linkerlijn (of raster) met iets anders. Gecentreerd, links en rechts door elkaar = onrust die niemand kan aanwijzen maar iedereen voelt. Kies per scherm een klein aantal verticale lijnen en houd je eraan; getallen in tabellen rechts uitgelijnd, tekst links (data-viz-craft).

## Step 5 — De-emphasis is half the work

Hiërarchie maak je net zozeer door te DEMPEN als door te versterken: metadata, timestamps en secundaire acties gaan naar muted (theme-craft `--color-text-muted`), kleiner, of achter een overflow-menu. Vraag per element niet "mag dit opvallen?" maar "verdient dit aandacht ten koste van de winnaar?" — meestal is het antwoord nee. Snoeien is hier de vaardigheid; content die niemand op dit scherm nodig heeft, verhuist of verdwijnt (ux-blueprint beslist waarheen).

## Verify — three tests, ten seconds each

- [ ] **Squint test**: knijp je ogen dicht (of blur het screenshot). Zie je precies de winnaar en de scan-volgorde? Zie je grijze pap → geen hiërarchie.
- [ ] **5-secondentest**: laat iemand (of beoordeel als koude bezoeker) 5 seconden kijken: wat is dit, wat moet ik doen? Fout antwoord = hiërarchie fout, niet de gebruiker.
- [ ] **Tel de schreeuwers**: meer dan ~3 elementen die om aandacht vechten (groot/vet/gekleurd/bewegend)? Demp tot er één wint.

Fails hier zijn ontwerpfouten op compositieniveau — los ze op met de stappen hierboven, vóór pixel-polish de details gaat schaven.
