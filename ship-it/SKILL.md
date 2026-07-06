---
name: ship-it
description: 'Take a finished build live safely - pick the right host, handle env vars and secrets, connect the domain with HTTPS, deploy, smoke-test on a real device, and have a rollback plan ready. Use this skill whenever the user says "zet live", "deploy", "publiceer", "hoe krijg ik dit online", "launch", mentions hosting/domein/DNS/Vercel/Netlify, or whenever a website or app build is finished and the obvious next step is getting it on the internet. This skill covers the MECHANICS of going live; run seo-ship-kit (findability) and web-security-gates (hardening) alongside it as the pre-launch trio.'
---

# Ship It

A build that only runs locally has delivered zero value. This skill turns "het werkt bij mij" into "het staat live" without the classic launch-day wounds: leaked secrets, broken forms discovered by visitors, and no way back after a bad deploy.

## Step 1 — Choose the host by what the project IS

Do not ask the user to pick from a jargon list; determine the project type and recommend one:

| Project type | Host | Why |
|---|---|---|
| Static site (HTML/CSS/JS, no server) | Netlify, Vercel, Cloudflare Pages, GitHub Pages | Free tier, deploy in minutes, HTTPS automatic |
| Framework app (Next.js, Astro, SvelteKit) | Vercel or Netlify | Build pipeline built in, preview per change |
| App with backend/database | Combine: frontend above + Supabase/Neon/Railway for the server | Separate responsibilities, free tiers |
| Quick internal tool / prototype | Vercel or an artifact link | Speed above all |

If the user already has hosting, work with that — migration is a separate decision, never a side effect.

## Step 2 — Pre-flight checklist

Run through this BEFORE the first deploy, not after:

- [ ] frontend-quality-gates and web-security-gates have been run on the code
- [ ] seo-ship-kit has been run (meta tags, OG image, sitemap)
- [ ] No secrets in code or git history: API keys, tokens, passwords. Actively search (`grep` for `key`, `secret`, `token`, `password`). Found one? Move it to env vars and treat the leaked key as burned — have the user rotate it.
- [ ] Env vars documented: which exist, where they are set (host dashboard, never in the repo). `.env` is in `.gitignore`; provide a `.env.example` without values.
- [ ] A 404 page exists and matches the design
- [ ] All links and assets are relative or use the production domain — zero `localhost` references
- [ ] Build runs clean locally (no errors, no console noise)

## Step 3 — Domain & HTTPS

- New domain: register at a registrar (e.g. Cloudflare, Namecheap), then point DNS at the host. The host provides the exact records (usually a CNAME or A record) — follow THEIR instructions, never guess IP addresses.
- DNS changes can take up to 24h; usually minutes. Say this up front so the user does not panic.
- HTTPS is automatic on all recommended hosts (Let's Encrypt). After go-live, verify http→https redirects.
- Pick one canonical form (with or without `www`) and redirect the other.

## Step 4 — Deploy

- Prefer git-connected deploys (push = deploy) over manual uploads: history, previews and rollback come free.
- First deploy goes to a preview URL; attach the real domain only after it checks out.
- Set env vars in the host dashboard BEFORE the first build — a build without them fails cryptically.

## Step 5 — Post-deploy smoke test

Test on the LIVE URL, not locally. Minimum:

- [ ] Open on a real phone, not just devtools emulation
- [ ] Click every primary flow: navigation, form submit (verify the submission actually ARRIVES), main CTA
- [ ] Console clean? Network tab: no 404s on assets, no mixed content (http assets on an https page)?
- [ ] Share the URL in a chat app: does the link preview look right (OG tags)?
- [ ] Visit a non-existent page: proper 404?

## Step 6 — Rollback plan (write it down BEFORE you need it)

- Git-connected hosts: rollback = re-activate the previous deploy in the dashboard (one click). Know where that button is before launch.
- Database migrations are the dangerous exception: a code rollback does not undo a migration. For schema changes: migrate additively first (add columns, do not drop), clean up old columns later.
- Define the trigger in advance: "if X is broken on prod, we roll back" — deciding during panic goes badly.

## Hard rule

Never mark a launch as done on "deploy succeeded". Done = smoke test passed on the live URL. The gap between those two states is where launches fail publicly.
