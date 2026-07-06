---
name: github-polish
description: 'Turn a GitHub profile into the second portfolio it secretly is - profile README, 4-6 pinned repos each with a screenshot-topped README and live link, clean commit history on showcase repos, secrets scrubbed, and embarrassing old repos archived. Use this skill whenever the user shares a GitHub link on CV or portfolio (sollicitatie-kit links there!), asks "hoe maak ik mijn GitHub netter", prepares for dev-stage applications, or when a repo needs a README. Developers WILL click through and judge - curate it like portfolio-craft: you are judged on the weakest visible repo.'
---

# GitHub Polish

Voor developer-rollen klikt de technische beoordelaar vrijwel altijd door naar GitHub — het CV zegt wat je claimt, de repos tonen wat je doet. En anders dan het portfolio (dat jij regisseert) toont GitHub álles: ook de rommel. Cureren is dus het halve werk; de andere helft is elke showcase-repo laten lezen als een mini-case.

## Step 1 — Cureer eerst (je zwakste zichtbare repo telt)

Loop alle publieke repos langs met de portfolio-craft-bril:

- **Archiveer of maak privé**: tutorial-restanten, gestrande experimenten, cursus-opdrachten, alles waarvoor je je bij doorklikken zou generen. Archiveren is geen wissen — het haalt het alleen uit de etalage.
- **NDA/klantwerk hoort privé** — klantcode publiek zetten voor je portfolio is dezelfde self-own als in portfolio-craft.
- **Secrets-check op wat blijft**: geen API-keys of wachtwoorden in code óf historie (git-safety-net: gecommit = verbrand, roteren). Elke showcase-repo krijgt een `.env.example`.

Wat overblijft: je 4–6 beste, als **pinned repos** in de volgorde van je portfolio, elk met een goede one-line description en link naar de live demo in het repo-veld.

## Step 2 — Elke showcase-repo krijgt een README die verkoopt

Een repo zonder README is onzichtbaar werk — niemand leest code om te ontdekken wat iets is. Het format (mini-versie van case-study-writer):

```markdown
# Projectnaam — wat het is in één zin
[hero screenshot — showcase-assets regels: echte content, scherp]

**Live**: [link] · **Stack**: React, Supabase

## Wat het doet
2-3 zinnen: voor wie, welk probleem.

## Beslissingen
2-3 regels: de interessantste keuze en waarom (de case-study-ruggengraat, ingedikt).

## Lokaal draaien
npm install && npm run dev — met .env.example verwezen.
```

Screenshot BOVENAAN — de lezer beslist in seconden, en beeld verslaat tekst. De live link is het verschil tussen "leuk geprobeerd" en "die shipt" (side-project-picker: live telt dubbel).

## Step 3 — Profiel-README (de voorpagina)

Kort en gericht, geen dashboard van badges en stats-widgets (dat is decoratie zonder informatie):

- Wie je bent en welke richting (dezelfde éne zin als portfolio en CV — sollicitatie-kit consistentie)
- 3–4 uitgelichte projecten met één regel + link (naar repo én live)
- Link naar portfolio en contact
- Toon rustig-professioneel; één emoji mag, een regenboog niet (brand-kit tone geldt ook hier)

## Step 4 — Historie-hygiëne op showcase-repos

Beoordelaars die dieper kijken, lezen commits — als steekproef van hoe je werkt:

- Recente commits op showcase-repos: nette berichten die wat+waarom zeggen (git-safety-net-regels zichtbaar in het wild); geen reeks "fix", "fix2", "aaaah".
- Regelmaat verslaat streaks: de groene grafiek hoeft niet vol, maar een profiel dat al acht maanden stil ligt terwijl je "actief bouwend" claimt, spreekt je CV tegen. Commit-farming (lege commits voor de graph) wordt doorzien en oogt erger dan stilte.
- Zet een licentie op showcase-repos (MIT is de veilige standaard voor eigen werk — dependency-scout-kennis, nu als aanbieder).

## Verify (uitgelogd, incognito)

- [ ] Bekijk je profiel als vreemde: klopt het 30-secondenverhaal (wie, wat, kan die het — portfolio-craft-test)?
- [ ] Elke pinned repo: README met screenshot + werkende live link + kloonbaar zonder vragen?
- [ ] Geen secrets, geen klantwerk publiek, geen gênante repos in zicht?
- [ ] Profiel-link staat op CV, portfolio en LinkedIn — en andersom linken ze terug?
