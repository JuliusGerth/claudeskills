---
name: form-craft
description: 'Build forms people actually finish - right input types, validation at the right MOMENT (not on the first keystroke), specific error messages next to the field, accessible labels, and multi-step flows for long forms. Use this skill whenever building or reviewing ANY form: contact, signup, login, checkout, settings, search, upload, or a multi-step wizard; and whenever the user says "formulier", "invulveld", "mensen haken af", or a form feels frustrating. Forms are where conversion dies - pair with api-integration-craft for the submit plumbing and design:ux-copy for field microcopy.'
---

# Form Craft

Forms are the highest-friction moment in any interface: the user must work, and every irritation costs completions. Most form misery comes from three mistakes — yelling "ongeldig!" while someone is still typing, vague error messages, and asking too much. This skill removes all three.

## Fewer fields first

Every field costs completions. For each field ask: is this needed NOW? Kill nice-to-have fields, split first/last name only if truly required, never ask what can be derived (country from postcode). Mark optional fields with "(optioneel)" — marking required ones with * assumes people know the convention; when almost everything is required, marking the exceptions is clearer.

## The right input, configured

HTML does half the UX work free — if the right attributes are set:

- `type="email" / "tel" / "url" / "number" / "date"` → the matching mobile keyboard appears. A tel field with a letters keyboard is self-inflicted pain.
- `autocomplete="name / email / postal-code / street-address / current-password / new-password / one-time-code"` → browsers prefill; on mobile this is the difference between 30 seconds and 3.
- `inputmode="numeric"` for digit strings that are not math (postcode, OTP).
- Font-size ≥ 16px on inputs, or iOS zooms in on focus and the layout jumps.
- Labels are ALWAYS visible elements bound with `for`/`id`. A placeholder is not a label: it vanishes on typing, exactly when people forget what the field asked. Placeholders only for format hints ("bijv. 1234 AB").

## Validation timing: reward early, punish late

The rule that fixes 80% of form frustration:

- NEVER show an error while someone is still typing in an untouched field.
- Validate on **blur** (leaving the field) or on **submit**.
- Once a field has been marked invalid, THEN re-validate on every keystroke — so the error disappears the moment they fix it (instant reward), not at the next blur.
- Submit with errors → focus jumps to the first invalid field, all invalid fields marked simultaneously.

## Error messages that help

- Next to the field itself (plus color AND an icon — color alone fails color-blind users, see accessibility-review), bound via `aria-describedby` so screen readers announce it.
- Specific and actionable: "Wachtwoord heeft minimaal 8 tekens nodig" — never "ongeldige invoer". Write them with design:ux-copy discipline.
- Never clear filled fields on an error. Wiping a form is data loss and the moment people leave.
- Password fields: show-password toggle, and state requirements BEFORE typing, not as a surprise rejection after.

## Layout & flow

- One column. Multi-column forms cause skipped fields and zigzag eye paths.
- Group related fields (`fieldset` + `legend` for radio/checkbox groups — also the accessible way).
- Logical order, matching how people think (name → contact → details), tab order = visual order.
- Long form (7+ fields)? Split into steps with a progress indicator, one topic per step, back-navigation that keeps data. Ask the easy things first — invested people finish; a wall of fields up front scares them off.

## Submit (hand off to api-integration-craft)

Disable button while pending with progress in the button ("Versturen…"), keep input on failure, unmistakable success state that confirms WHAT happened ("We mailen je binnen een dag op jan@…"). Enter submits from any field.

## Verify before delivery

- [ ] Complete the form with keyboard only (Tab/Enter) — everything reachable, focus visible
- [ ] Trigger every validation: does it obey blur-then-live timing?
- [ ] Every error message names the fix, sits at its field
- [ ] Mobile: right keyboards, no zoom-jump, autofill fills sensibly
- [ ] Submit twice fast: no double submission
