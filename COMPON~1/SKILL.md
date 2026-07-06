---
name: component-craft
description: 'Structure frontend code so it stays editable - clear component boundaries, props-in/events-out, state in the right place, feature-based folders, and the rule of three against premature abstraction. Use this skill whenever building or growing any frontend beyond a single file (React, Vue, vanilla JS, artifacts), whenever a file passes ~150 lines or a component does two jobs, and whenever the user says "wordt onoverzichtelijk", "spaghetti", "waar moet dit staan", or a change in one place keeps breaking another. Architecture for solo builders - the code side of what ux-blueprint does for screens.'
---

# Component Craft

Frontend code rots in a predictable way: one file grows until every change risks everything, state gets copied until no one knows which copy is true, and abstractions built "voor straks" fit nothing. This skill prevents that rot — which matters double when Claude sessions edit the code, because clear boundaries are what make edits safe (see project-continuity).

## When to split a component

Split when at least one is true — not before:

- **Reuse**: the same UI appears in a second place (real reuse, not imagined future reuse).
- **One sentence test**: you cannot say what it does in one sentence without "en ook".
- **Own state**: a section manages its own state independent of siblings.
- **Size**: past ~150 lines, understanding cost beats splitting cost.

Do NOT split just because you can. "Eén div = één component" produces a maze of 15-line files where logic is impossible to follow. Fewer, clearer components beat many tiny ones.

## Props: data in, events out

- A component receives data via props and reports via callbacks (`onSelect`, `onSubmit`) — it never reaches outside itself to change the world. This keeps every component testable in isolation and safe to move.
- Boolean explosion (`isLarge isPrimary isOutline isDanger`) → one `variant` prop with names from the design system (pixel-polish/BRAND.md words).
- Props drilling deeper than ~2 levels through components that only pass them on → restructure: pass components as children (composition) or, for true app-globals (theme, ingelogde user), a context/store. Context is for globals, not a dumping ground.

## State: the core discipline

Most frontend bugs are state bugs (bug-hunt confirms). Three rules prevent them:

1. **Single source of truth.** Every fact lives in exactly one place. A second copy of the same fact WILL drift — then which is true?
2. **Derive, do not store.** `totaal`, `gefilterdeLijst`, `isValid` are computed from source state at render, never stored next to it. Stored derivations go stale; computed ones cannot.
3. **As low as possible, as high as necessary.** State lives in the lowest component that contains everyone who needs it. Two siblings need it → lift to the parent. The whole app needs it → store/context. Everything global = everything re-renders and nothing is reusable.

Server data is its own category: cache it via api-integration-craft patterns (or a data library), do not hand-copy it into component state.

## Folders: by feature, not by type

```
src/
  features/
    projecten/     ← component + logic + styles together
    facturen/
  shared/          ← genuinely reused: Button, formatDate, apiFetch
  App.jsx
```

Group by what things are FOR, not what they ARE (`components/` + `utils/` + `hooks/` bins scatter one feature across three folders). Everything for one feature sits together; a feature is deletable by removing one folder. `shared/` must EARN entries via the rule of three.

## The rule of three (anti-abstraction guard)

First time: write it inline. Second time: copy it, live with the duplication. Third time: NOW extract — three real cases show what the abstraction must actually be. Abstractions built at one case are guesses; wrong abstractions cost more than duplication ever does. The same rule governs helpers, custom hooks, and shared components.

Extract logic (custom hook / plain function) when the same stateful pattern repeats — but name it after the domain (`useProjecten`), not the mechanism (`useData2`).

## Naming

Components = what they ARE: `FactuurRij`, `ProjectKaart`. Handlers = what HAPPENED: `onRijSelect`, `handleSubmit`. Booleans read as questions: `isOpen`, `heeftFouten`. If naming something is hard, the split is wrong — naming pain is a design signal, not a vocabulary problem.

## Vanilla JS projects

Same principles, different syntax: ES-modules per feature, functions that get state passed in instead of reading globals, one `render(state)` path instead of scattered DOM pokes, event delegation at container level. No framework does not mean no architecture.

## Review pass

Walk the tree and ask per component: one sentence? props in / events out? state at the right height? any stored value that should be derived? any abstraction with fewer than three users? Fix the worst offender first — architecture improves by refactor steps (with git-safety-net commits between them), not by big-bang rewrites.
