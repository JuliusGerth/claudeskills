---
name: brand-kit
description: 'Define a small, reusable brand identity - name, tagline, tone of voice, color palette, type pairing, and logo direction - captured in one BRAND.md so every page, mail, deck, and social post feels like the same sender. Use this skill when naming a product or company, when the user asks for a logo, huisstijl, merk, tagline, "hoe moet het klinken", or when outputs across a project look/sound inconsistent. Run it ONCE per product, before ui-concept-forge (which styles a single interface) - brand-kit decides the identity that ui-concept-forge and copy-that-converts then execute.'
---

# Brand Kit

Without a written identity, every asset gets invented from scratch: the site sounds formal, the mails sound jolly, slide decks use a third palette. Consistency — not beauty — is what makes something feel professional and trustworthy. This skill produces that identity on one page, small enough to actually be used.

## Step 1 — Positioning in three lines

Before any aesthetics (steal from feature-spec / copy-that-converts brief if present):

- **Voor wie** — the audience, specific.
- **Belofte** — the one thing this brand delivers.
- **Karakter** — three adjectives + their limits, e.g. "nuchter, warm, deskundig — maar nooit joviaal of corporate". The "maar nooit" half does the real work later.

Every later choice (name, color, tone) is tested against these three lines.

## Step 2 — Naming (if needed)

Generate 15+ candidates across types before judging: descriptive (zegt wat het is), evocative (roept het gevoel op), samengesteld/verzonnen woord. Use creative-spark to escape the obvious. Then filter hard:

- Uitspreekbaar aan de telefoon, spelbaar zonder "nee, met een K"
- Domein beschikbaar of acceptabele variant (.nl/.com check), geen bekende naamsbotsing in dezelfde markt (search it — and note that a real trademark check is the user's own step for serious ventures)
- Werkt het nog als het bedrijf groeit? ("PieterPizzaPunt" bindt aan pizza)
- Test the top 3 against the Step 1 karakter; pick with the user.

Tagline: the belofte in max 6 words, concrete over clever (copy-that-converts headline rules apply).

## Step 3 — Tone of voice (the most-skipped, most-used asset)

Define with examples, not adjectives alone — future sessions imitate examples:

- **Zo klinken we**: 2 sample sentences (a greeting, an error/apology).
- **Zo niet**: the same 2 rewritten wrong ("Oeps! Er ging iets mis 🙈" vs. "Er ging iets mis. We lossen het op.").
- Aanspreekvorm: je of u — decide once, forever.
- Woordenlijst: 5 words we use, 5 we never use (jargon, superlatieven).

This section feeds copy-that-converts, design:ux-copy, and every mail Claude ever drafts for the brand.

## Step 4 — Visual core (small on purpose)

- **Kleur**: 1 primary, 1 accent, 2–3 neutrals, as hex. Check contrast now (design:accessibility-review), not per-project. Name what each is FOR (accent = alleen acties).
- **Typografie**: one pairing — kop + broodtekst (max 2 families, see speed-craft budget). Name fallbacks.
- **Logo direction**: for solo builders, a well-set wordmark in the brand font + color beats an amateur pictogram. Describe the direction (wordmark/monogram/symbool + gevoel); execute in canvas-design. Require it to work in 1 kleur en klein (favicon-formaat) — effects that die at 16px are decoration, not identity.
- **Beeldstijl**: one line — foto's warm en menselijk / illustratie flat / screenshots met schaduw — so assets match.

## Step 5 — Capture in BRAND.md

Write the whole kit to `BRAND.md` next to PROJECT.md (project-continuity governs it): positioning, naam + tagline, tone-sectie met voorbeelden, kleuren (hex), fonts, logo-richting, beeldstijl. Under ~60 lines. From now on every skill in the pipeline reads BRAND.md first — ui-concept-forge executes this identity for interfaces instead of inventing one, and any deck (pptx), doc (docx), or mail inherits it too.

## Guardrails

- One brand per product; a second audience is a second conversation, not a mushier middle.
- Do not copy an existing brand's look or name — check, do not assume (and originality is also the legally safe path).
- Rebrand niet tijdens de bouw: identity churn kost al het eerdere werk. Wijzigingen gaan bewust, via een besluit in PROJECT.md.
