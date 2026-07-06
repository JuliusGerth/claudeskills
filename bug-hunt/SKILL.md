---
name: bug-hunt
description: 'Fix web bugs systematically instead of guessing - reproduce first, read the real error, isolate by binary search, classify the bug type against standard-suspect tables, fix the root cause, and add a guard so it cannot return. Use this skill whenever something is broken in a web app, site, or artifact: "het doet het niet", "kapot", "werkt niet meer", "gisteren deed het het nog", layout that explodes, buttons that do nothing, data that will not show, or when a previous fix did not fix it. Specialized for frontend/web; for backend/infra incidents use engineering:debug.'
---

# Bug Hunt

Guessing at bugs ("misschien is het X, laat ik Y proberen") burns time and often plants new bugs. Debugging is a search problem: shrink the space where the bug can hide until only the cause remains. Follow the loop in order — skipping to "fix" is how the same bug returns next week.

## The loop

### 1. Reproduce reliably
Get exact steps that trigger it every time: which page, which input, which browser/device, logged in or not. A bug you cannot reproduce, you cannot verify as fixed — "ik denk dat het nu werkt" is not a fix. If it is intermittent, that is itself a clue: suspect timing/async or environment differences.

### 2. Read the ACTUAL error
Before forming any theory: open the console (errors AND warnings), the network tab (red requests, status codes, response bodies), and read the stack trace to the first line in YOUR code. Most bugs announce themselves verbatim; theorizing before reading is solving a riddle while the answer is on screen. No console error but wrong behavior? Log the values at the point of divergence — verify assumptions, do not trust them.

### 3. Isolate by binary search
Halve the search space repeatedly: comment out half the recent changes / half the component — gone or still there? "Wanneer deed het het nog wel?" — walk changes since then. Build a minimal reproduction if it is stubborn; the act of shrinking usually exposes the cause.

### 4. Classify — standard suspects per type

**State bugs** (UI shows wrong/old data): stale closure capturing an old value; mutating state directly instead of replacing (UI never re-renders); two sources of truth drifting apart; state that should have been derived/computed instead of stored.

**Async/timing bugs** (works sometimes, "flikkert", wrong order): missing `await`; race between two requests resolving out of order (see api-integration-craft); reading data before load finished; effect running before/after you assumed.

**Layout bugs** (overlap, overflow, "op mijn scherm wel"): fixed heights on variable content; flex children refusing to shrink (`min-width: 0` missing); z-index war caused by stacking contexts; absolute positioning against the wrong ancestor; content wider than viewport from an unwrapped element.

**Data-shape bugs** (`undefined is not a function`, blank sections): response field is `null`/missing/renamed; array expected but object received; number arriving as string ("2" + 1 = "21"); timezone/locale differences in dates.

**"Works here, not there"**: caching (hard refresh / incognito first!); env vars missing in production; http vs https; browser differences; ad blockers.

### 5. Fix the root cause, not the symptom
If a value is `undefined`, a `?.` shuts the error up but the real question is WHY it is undefined — upstream, a real cause is now hidden and will resurface elsewhere. Ask "why" until the answer is a decision, not another symptom. Symptom patches are only acceptable as explicitly-labeled temporary measures.

### 6. Verify + guard
Re-run the exact reproduction from step 1 — in a clean state (hard refresh, fresh data). Check you did not break neighbors (the two most similar flows). Then make the bug impossible to return silently: a validation at the boundary, a regression test, or at minimum a comment at the trap explaining the why.

## Anti-patterns

- **Shotgun debugging**: changing five things at once. When it "works", you do not know why, and four changes are noise. One change per test.
- **Fix by deletion**: removing the feature that errors. The error was information.
- **Blaming the tool**: "React doet raar" — in 99% of cases the bug is in our code. Assume that first; it is the productive assumption.

## When stuck (30+ minutes, no progress)

Say so honestly. Then: re-read the error as if seeing it for the first time, explain the problem out loud to the user (rubber-ducking works on models too), question the assumption you are most certain of — the bug lives in "dat kan het niet zijn" surprisingly often.
