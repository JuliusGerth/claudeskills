---
name: prod-radar
description: 'Know when your live site breaks BEFORE users tell you - set up error tracking, uptime monitoring, and a weekly health check sized for a solo builder, and read the signals correctly when something fires. Use this skill right after any launch (the follow-up to ship-it), whenever the user asks "hoe weet ik of het nog werkt", "is mijn site down", mentions Sentry/uptime/monitoring/logs, or discovers breakage late ("stond er al dagen uit"). Also use it when errors or alerts come in and need triage. Feeds bug-hunt: radar detects, bug-hunt fixes.'
---

# Prod Radar

A launched site without monitoring is flying blind: it can be down for days, or erroring for every mobile visitor, and the owner finds out from an awkward email — or never. Users do not report bugs; they leave. The fix is not enterprise observability; it is three lightweight signals that take ~30 minutes to set up.

## The three signals (in priority order)

### 1. Uptime — "staat hij aan?"
An external service pings the live URL every few minutes and mails/apps when it does not respond. Free tiers of uptime monitors (e.g. UptimeRobot or the host's built-in checks) are plenty.

- Monitor the real page, and if there is a backend, also one API endpoint (`/api/health`) — the frontend can be up while the database is down.
- A trivial `/api/health` endpoint that touches the database turns "site is traag/raar" into a binary answer.

### 2. Error tracking — "gooit hij fouten?"
Console errors on visitors' devices are invisible to you. An error tracker (e.g. Sentry — free tier suffices) captures them with stack trace, browser, and frequency.

- Install in frontend AND backend if both exist.
- Upload sourcemaps so stack traces point at readable code, not minified line 1.
- Filter noise at setup: browser-extension errors and bot traffic will otherwise bury real signals — mute what is not yours.

### 3. Reality pulse — "doet hij wat hij moet?"
Uptime and errors miss silent functional breakage (form posts to a dead endpoint, payment provider config expired). Two defenses:

- A weekly 5-minute manual pulse: run the ship-it smoke test on prod (main flow, form submit arrives, console clean). Schedule it (schedule skill) so it actually happens.
- Watch the trend, not just failures: analytics suddenly at zero usually means tracking broke or the site is unreachable for a segment — treat "verdacht stil" as an alert.

## Alert hygiene (the part everyone skips)

Alerts only work if they stay rare. Rules:

- Alert = actionable. "Site down" mails you; a single 404 does not. Everything else goes to a dashboard you check weekly.
- Every alert either gets fixed or gets muted-with-reason. An inbox of ignored alerts equals no monitoring — worse, it feels like monitoring.
- After two false alarms from the same check, fix the check. Trust in the radar is the actual asset.

## When something fires — triage before fixing

1. **Verify scope**: down for everyone or just one browser/region? Check the uptime dashboard + open the site yourself (incognito — see bug-hunt caching).
2. **Check the timeline**: what changed last? A deploy right before the errors started is the suspect 90% of the time → rollback first (ship-it keeps that button warm), investigate second. Restore service, then debug calmly.
3. **Read the error tracker**: frequency (1 user or all users?), first-seen (which deploy?), stack trace → hand to bug-hunt.
4. Nothing deployed and still down? Check the host/provider status page before debugging your own code — sometimes it is genuinely them.

## Weekly health check (5 minutes, scheduled)

- [ ] Uptime dashboard: any dips this week?
- [ ] Error tracker: new error types? One error spiking?
- [ ] Analytics trend: normaal patroon?
- [ ] Smoke test main flow on prod
- [ ] Domain + certificate not near expiry (registrar auto-renew AAN)

## Scope guard

This is solo-builder monitoring: know-it-broke + know-what-broke. Dashboards-of-dashboards, tracing, SLO math — that is team territory (engineering plugins). The radar is done when breakage reliably reaches you before it reaches your users' patience.
