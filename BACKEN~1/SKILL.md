---
name: backend-blueprint
description: 'Design the server side BEFORE writing backend code - data model, API endpoints, auth strategy, and authorization rules on one page, sized for a solo builder (not enterprise architecture). Use this skill whenever an app needs accounts, saved data, user content, payments, or any server logic; whenever the user asks "hoe sla ik dit op", "moet ik een database", "welke backend", "hoe doe ik login", or mentions Supabase, Firebase, Postgres, or building an API. The server-side counterpart to ux-blueprint - run it after feature-spec and before writing any backend code.'
---

# Backend Blueprint

Frontends are cheap to change; data models are not. A wrong table structure or auth choice discovered after launch means migrations, data loss risk, and rewrites. Spend 15 minutes designing on one page first. This skill produces that page.

## Step 1 — Extract the entities

Read the feature-spec (or the user's description) and list the NOUNS that must survive a page refresh: user, project, order, message, upload. For each entity:

- Fields with types (`title: text`, `created_at: timestamp`, `price_cents: integer` — money is always integer cents, never floats)
- Relations: belongs-to / has-many. Draw them: `User 1—n Project 1—n Task`
- What is unique? What is required? What defaults?

Red flag: an entity called "data" or "info" means the modeling is not done yet.

## Step 2 — Choose persistence (decision table, not ideology)

| Need | Choose |
|---|---|
| Relational data, filtering, reporting | Supabase / Neon (Postgres) — default choice for most apps |
| Realtime sync, simple document data | Firebase / Supabase Realtime |
| Single-user tool, no accounts | localStorage or a JSON/SQLite file — do not build a backend that is not needed |
| Only a contact form | Form service (Formspree e.d.) — no backend needed |
| Files/images | Object storage of the platform (Supabase Storage, S3), NEVER in the database |

The strongest move is recognizing when the answer is "geen backend nodig". Every server component is permanent maintenance.

## Step 3 — Define the API as a table

One row per endpoint, before any code:

| Method + path | In | Out | Auth? | Errors |
|---|---|---|---|---|
| GET /api/projects | – | Project[] | ✔ owner | 401 |
| POST /api/projects | {title} | Project | ✔ | 400 invalid, 401 |
| DELETE /api/projects/:id | – | 204 | ✔ owner | 401, 403 not yours, 404 |

Rules that prevent later pain:
- Every list endpoint gets pagination from day one (`?limit=&cursor=`) — retrofitting it breaks clients.
- Validate ALL input server-side (type, length, range). The frontend validates for UX; the server validates for truth. Client input is always untrusted (see web-security-gates).
- Consistent error shape everywhere: `{error: {code, message}}`.

## Step 4 — Auth ladder (pick the lowest rung that works)

1. **No accounts** — if the app works without identity, skip auth entirely.
2. **Magic link / email code** — no passwords to store or reset. Best default for solo builders.
3. **OAuth (Google/GitHub login)** — when users expect it; use the platform's built-in provider (Supabase Auth, Firebase Auth). NEVER hand-roll password storage.
4. **Roles** (admin/member) — only when the spec actually demands it.

## Step 5 — Authorization matrix

Auth says who you are; authorization says what you may touch. For each entity × action, write the rule:

```
Project: read = owner or invited member; write = owner; delete = owner
```

On Supabase, implement these as Row Level Security policies — the database enforces them even if API code has a bug. Whatever the stack: the rule "users can only reach their OWN rows" must be enforced server-side. Forgetting this is the most common real-world data leak in solo-built apps.

## Step 6 — Deliver the blueprint

Output one page containing: entity diagram, persistence choice + why, endpoint table, auth rung, authorization matrix, and open questions. Get user sign-off, save it to the project (PROJECT.md or `BACKEND.md`), and only then write code.

## Scope guard

This is solo-builder architecture: one database, one deploy, boring technology. If genuine scale questions arise (queues, microservices, caching layers), switch to the engineering:system-design skill — do not gold-plate a hobby-scale backend.
