---
name: api-integration-craft
description: 'Make every remote call in the frontend production-grade - loading, error, empty, and success states for EVERY fetch, plus aborts, race protection, timeouts, retries, and optimistic updates with rollback. Use this skill whenever frontend code calls an API, loads data, submits a form, or talks to a backend, database, or LLM; and whenever the user reports "blijft laden", "spinner stopt niet", "oude data", flickering content, or double submissions. Complements frontend-quality-gates: that skill checks the UI shell, this one hardens the data layer inside it.'
---

# API Integration Craft

The difference between a demo and a product is what happens when the network is slow, the server errors, or the response is empty. Demos assume success; products handle everything else. Every remote call gets this treatment — no exceptions for "simple" fetches, because users do not experience code, they experience states.

## The Four States rule

Every piece of UI backed by a remote call renders all four:

1. **Loading** — skeleton in the shape of the coming content (prevents layout shift) when the layout is known; spinner only for unknown shapes. Delay showing it ~150ms so fast responses never flash.
2. **Error** — human message ("Kon projecten niet laden"), never a raw error object, plus a working "Opnieuw proberen" button. Distinguish offline ("check je verbinding") from server errors.
3. **Empty** — success with zero items is NOT an error and NOT a blank screen. Show what belongs here and the action to create the first item (see ux-blueprint empty states).
4. **Success** — the happy path, the only one demos build.

Quick audit: for each fetch in the code, point to where each of the four renders. Cannot point? Not done.

## Submissions (POST/PUT/DELETE)

- Disable the submit button while in flight (prevents double orders/messages) and show progress in the button itself ("Versturen…").
- Keep the user's input on failure. Wiping a form on error is data loss.
- Idempotency: assume users double-click and networks retry. Server-side unique keys or an idempotency token stop duplicates.

## Race conditions & stale responses

Typing in a search box fires request A then B; A may resolve LAST and overwrite B's results with stale data. Guard every parameterized fetch:

- Abort the previous request via `AbortController` when a new one starts, or
- Tag requests with a sequence number and ignore responses older than the latest.

Also abort in-flight requests on unmount/route change — setting state on a dead component wastes work and causes warnings. In React, do this in the effect cleanup.

## Timeouts & retries

- Every request gets a timeout (8–15s). Without one, "loading" can last forever — the spinner that never stops.
- Retry ONLY idempotent reads (GET), max 2–3 attempts, exponential backoff + jitter (500ms, 1500ms). Never auto-retry mutations — that is how duplicate payments happen; give the user the retry button instead.
- Debounce user-typed triggers (search: ~300ms) so you are not hammering the API per keystroke.

## Never trust the response shape

APIs change, fields come back `null`, arrays arrive as `undefined`. Runtime-guard at the boundary: check the fields you use exist before rendering (`data?.items ?? []`), and fail into the Error state with a logged detail — not a white-screen TypeError in production.

## Optimistic updates (only where it pays)

For instant-feel toggles (like, favorite, check-off): update the UI immediately, fire the request, and on failure roll back the UI and inform the user. Keep the pattern honest: snapshot previous state → apply → await → rollback on error. Do not use optimistic updates for anything with money or irreversible effects.

## Centralize the plumbing

If the same timeout/error/JSON logic appears in three fetches, extract one `apiFetch()` wrapper (base URL, auth header, timeout, error normalization, JSON parsing) so every call is consistent and fixes land in one place. In React projects, prefer an established data library (e.g. TanStack Query) over hand-rolling caches — hand-rolled caching is a bug farm.

## Delivery checklist

- [ ] Four states per remote call, pointable in code
- [ ] Submit buttons disable in flight; input survives errors
- [ ] Parameterized fetches abort/ignore stale responses
- [ ] Timeouts everywhere; retries only on GETs
- [ ] Response shapes guarded at the boundary
- [ ] Secrets are NOT in frontend code (API keys belong server-side — see web-security-gates)
