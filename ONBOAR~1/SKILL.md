---
name: onboarding-craft
description: 'Design the first five minutes of a product so new users reach value before they reach doubt - aha-moment first, empty states that teach, setup friction deferred, sample data instead of a blank void, and progressive disclosure instead of feature tours. Use this skill whenever an app or tool gets its first-run experience, signup flow, or welcome screen; whenever the user says "onboarding", "eerste indruk", "mensen haken meteen af", "niemand snapt hoe het werkt", or an app opens as an intimidating blank page. Runs on top of ux-blueprint (which maps the flows) - this skill owns the NEW-user path specifically.'
---

# Onboarding Craft

New users arrive curious and leave at the first moment of confusion — usually within minutes. Most products spend those minutes on the wrong things: account setup, permission dialogs, and a tour of features the user cannot appreciate yet. Onboarding has ONE job: deliver the first moment of real value (the aha-moment) as fast as possible. Everything else is negotiable.

## Step 1 — Define the aha-moment first

Write down the specific moment a new user first thinks "oh, DIT is waarom ik dit wil": the first invoice sent, the first chart from their own data, the first automation that fires. Pull it from feature-spec if present. Every onboarding decision is then judged by one question: brengt dit de gebruiker dichter bij dat moment, of staat het ertussen?

If the aha-moment cannot be named, onboarding cannot be designed — go back to feature-spec.

## Step 2 — Clear the path (defer everything deferrable)

Count the steps between arrival and aha. Then attack the list:

- **Account/verificatie**: can the user try before signing up? Can signup wait until there is something to save? A magic link (backend-blueprint auth ladder) beats a password form.
- **Profielvragen, voorkeuren, teamnaam, avatar**: defer until AFTER first value — motivated users complete profiles; skeptical ones abandon forms.
- **Permissies** (notificaties e.d.): ask in context at the moment of need, never as a welcome barrage.
- If a setup step is truly unavoidable, prefill it with the smartest default and let the user correct later.

Target: aha-moment binnen enkele minuten, met zo min mogelijk beslissingen onderweg.

## Step 3 — Never open on a blank void

A new account with empty lists is the coldest possible welcome: the product looks broken and the user must invent their own first move. Choose one:

- **Voorbeelddata/template**: open with a sample project marked as example, deletable in one click. The user learns by looking — the interface explains itself with content in it.
- **Guided first creation**: one focused prompt ("Maak je eerste factuur") with most fields prefilled, not a 10-field form.

Every empty state in the product is onboarding (ux-blueprint screen states): instructie in één zin + de primaire actie-knop + eventueel een voorbeeld. "Nog geen projecten" alone is a dead end; "Nog geen projecten — begin met een template" is a path.

## Step 4 — Teach in context, not in a tour

Feature tours (8 tooltips over dingen die de gebruiker nog niet kan plaatsen) get clicked away and forgotten — knowledge does not stick before the need exists. Instead:

- Progressive disclosure: show the 20% of UI that serves the first task; advanced features reveal themselves when their context arrives (pattern-picker: tooltip vs helper text rules).
- Just-in-time hints: first time the user reaches a feature, ONE contextual hint — dismissible, never blocking, never twice.
- A starter checklist (3–5 taken, waarvan de eerste al afgevinkt) works because visible progress motiveert — but only if each item delivers value, not chores.
- Alles overslaanbaar. Onboarding die je gijzelt, went nooit meer goed.

## Step 5 — The first session ends well

The end of session one decides whether there is a session two. Close the loop: bevestig wat de gebruiker heeft bereikt ("Je eerste factuur staat klaar"), toon de logische volgende stap, en als er een e-mail volgt (welkom/activatie), laat die verwijzen naar dat succes — niet naar een feature-lijst (copy-that-converts voor de toon).

## Measure and verify

- [ ] Loop zelf de flow met een VERS account op een telefoon (responsive-craft matrix): tel stappen en beslissingen tot aha — elke stap moet zich verantwoorden (friction-audit is hier het gereedschap)
- [ ] Elke lege staat heeft instructie + actie
- [ ] Geen enkele blokkerende stap die uitstelbaar is
- [ ] Analytics op de funnel-stappen (prod-radar): wáár stoppen mensen? Dat punt is het volgende ontwerpprobleem
