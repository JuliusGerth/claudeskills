---
name: friction-audit
description: 'Walk the ONE flow that matters as a skeptical first-time visitor and remove what makes people quit - count every step, decision, input, and wait; classify friction (cognitief, motorisch, wachten, vertrouwen); then fix in kill order: schrap, stel uit, vul voor in, versimpel, leg uit - in die volgorde. Use this skill whenever a flow underperforms ("mensen haken af", "niemand rondt af", "waarom koopt niemand" together with copy-that-converts), before launching any signup/checkout/contact flow, and periodically on live products. Journey-level counterpart to design:design-critique (screen-level) - critique judges a screen, this audits the PATH.'
---

# Friction Audit

Users do not abandon flows at random — they quit at specific moments of doubt, effort, or waiting. Those moments are invisible to whoever built the flow, because the builder knows what every button does and trusts the site by definition. This audit makes the builder walk the path as the coldest possible visitor and produces a prioritized fix list.

## Step 1 — Pick ONE flow and its finish line

Audit the flow the product lives from: checkout, aanmelding, contactaanvraag, eerste-waarde-pad (onboarding-craft). Define DONE concretely ("betaling gelukt", "formulier aangekomen"). One flow per audit; a diffuse audit finds diffuse problems.

## Step 2 — Walk it cold (the hard part)

Op een telefoon (responsive-craft), incognito, alsof je het product niet kent en het maar half vertrouwt. Vanaf het échte startpunt — de advertentie/zoekresultaat/link, niet de homepage die insiders nemen. Log ELKE:

- **Stap** (schermwissel/pagina), **input** (elk veld telt), **beslissing** (elke keuze, ook "welke van deze twee knoppen?")
- **Wachtmoment** (laden, mail-verificatie, spinner — speed-craft meet ze)
- **Aarzeling**: elk punt waar je als koude bezoeker zou denken "wat gebeurt er als ik klik?", "waarom willen ze dit weten?", "wat kost dit eigenlijk?", "is dit veilig?"
- **Doodlopend punt**: fout zonder uitweg, terugknop die data sloopt (form-craft), verplichte stap die vastloopt

Noteer letterlijk, zonder meteen op te lossen — oplossen tijdens het lopen maskeert de volgende frictie.

## Step 3 — Classify (elke soort heeft een ander medicijn)

| Type | Herken je aan | Medicijn |
|---|---|---|
| **Cognitief** | keuzes, jargon, onduidelijke labels, "wat is het verschil?" | minder opties, duidelijkere woorden (ux-copy), één winnaar per scherm (hierarchy-craft) |
| **Motorisch** | veel velden, klikken, scrollen, typen op mobiel | velden schrappen/voorinvullen (form-craft), stappen samenvoegen |
| **Wachten** | laden, verificatiemails, trage overgangen | speed-craft; wachttijd die moet, benoemen ("±1 min") |
| **Vertrouwen** | prijs pas laat zichtbaar, verplicht account, "wat doen ze met mijn gegevens" | kosten vroeg tonen, gast-optie, bewijs bij de actie (copy-that-converts), privacy-duidelijkheid (web-legal-kit) |
| **Herstel** | fout wist invoer, vage foutmelding, geen weg terug | form-craft foutregels, api-integration-craft states |

## Step 4 — Fix in kill order

Voor elke frictie, in deze volgorde afwegen (de beste stap is de stap die verdwijnt):

1. **Schrap** — moet deze stap/dit veld überhaupt bestaan voor DONE?
2. **Stel uit** — kan het ná het doel (account na aankoop, profiel na eerste waarde — onboarding-craft)?
3. **Vul voor in** — slimme default, onthouden invoer, afleiden i.p.v. vragen (land uit postcode)
4. **Versimpel** — twee stappen samenvoegen, keuze terugbrengen tot aanbevolen default + "meer opties"
5. **Leg uit** — pas als laatste redmiddel: microcopy die de twijfel wegneemt op de plek zelf ("Geen creditcard nodig")

Uitleg toevoegen aan een stap die weg kon, is frictie decoreren.

## Step 5 — Deliver the friction log

```markdown
| # | Waar | Frictie | Type | Fix (kill order) | Impact |
|---|------|---------|------|------------------|--------|
| 1 | Checkout stap 2 | account verplicht vóór prijs zichtbaar | vertrouwen | gast-checkout (schrap) | hoog |
```

Sorteer op impact × vroegte in de flow (vroege frictie raakt iedereen; late frictie raakt bijna-klanten — beide zwaar, alles ertussen lichter). Fix de top, loop de flow OPNIEUW (stap 2) — fixes introduceren soms nieuwe frictie. Op een live product: leg de funnel vast in analytics (prod-radar) zodat de volgende audit meet i.p.v. voelt, en herhaal het ritueel na elke grote wijziging.
