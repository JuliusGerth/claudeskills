---
name: web-legal-kit
description: 'Make a public website or app AVG/GDPR-decent before launch - privacy statement, cookie policy (banner only when actually needed), cookieless analytics choices, form consent, and required business info, tuned for NL/EU rules. Use this skill whenever a site or app goes public (pair with ship-it and seo-ship-kit), collects ANY personal data (forms, accounts, analytics, newsletters), or when the user asks about privacyverklaring, cookiebanner, AVG, GDPR, "mag ik dit opslaan", or algemene voorwaarden. Produces practical drafts and checklists - not legal advice; flag when a real jurist is needed.'
---

# Web Legal Kit

Shipping publicly in the EU comes with obligations that solo builders discover too late — usually via an angry email. The good news: for a typical site the requirements are modest, and the best solution is usually collecting LESS data, not writing more policy. Always state clearly that this produces working drafts, not legal advice; for payments, health data, minors, or anything unusual, advise a professional review.

## Step 0 — Data inventory (drives everything)

List what the site actually collects, where it goes, and how long it stays:

- Forms (name, email, message) → mailbox? database? third party?
- Accounts (backend-blueprint has the entities) → what fields, why?
- Analytics → which tool, does it use cookies, where is the data processed?
- Embeds (YouTube, maps, chat widgets) → these often set third-party cookies silently
- Newsletter → which service?

Every item must answer "waarom heb ik dit nodig?" — no answer means delete the field. Data minimization is both the law's core principle and the cheapest compliance strategy.

## Step 1 — The cookie question (most sites get this backwards)

A cookie banner is NOT automatically required. The rule:

- **Functional cookies** (login session, cart, language) → no consent needed, no banner needed.
- **Analytics** → choose a cookieless/privacy-friendly option (privacy-configured or cookieless analytics tools) → no banner needed. This is the recommended default for solo builders: fewer obligations AND better UX than a consent wall.
- **Tracking/marketing cookies or third-party embeds** (ad pixels, YouTube embeds, social buttons) → consent required BEFORE placement: a real banner where "weigeren" is as easy as "accepteren", and nothing tracking loads until acceptance. Pre-ticked boxes and cookie walls are not valid consent.

The strongest move: eliminate the trackers, skip the banner entirely. For video embeds, use the privacy/no-cookie embed mode or click-to-load facades (speed-craft wants those anyway).

## Step 2 — Privacyverklaring (required as soon as ANY personal data is processed)

Generate a draft from the Step 0 inventory, in plain language (verplicht begrijpelijk — dat is een feature, geen beperking). Must cover:

- Who is responsible (naam/bedrijf + contact)
- What is collected and WHY (per purpose, from the inventory)
- Legal basis per purpose (meestal: uitvoering overeenkomst, gerechtvaardigd belang, of toestemming)
- How long data is kept (concrete terms, not "zo lang als nodig")
- Which third parties/processors receive data (analytics, mail service, host) and transfers outside the EU
- User rights: inzage, correctie, verwijdering, bezwaar + how to exercise them (an email address suffices)

Link it in the footer of every page. Keep it in sync when the data inventory changes — a stale privacy statement is worse than none for trust.

## Step 3 — Forms & newsletters

- Ask only what the purpose needs (a contact form needs no birthdate).
- Newsletter signup = separate, unticked opt-in; never bundled silently with a purchase or download. Every mail needs a working unsubscribe.
- Contact forms need no consent checkbox (answering IS the purpose), just the privacy link nearby.

## Step 4 — Required business info & voorwaarden

- Commercial NL sites: vermeld bedrijfsnaam, KvK-nummer, contactgegevens (webshops: ook btw-nummer en retour/herroepingsrecht-info — 14 dagen bedenktijd geldt bij verkoop op afstand).
- Algemene voorwaarden: only needed when actually selling or providing services; draft from a checklist of what the user promises and excludes, and recommend legal review for real revenue.

## Launch checklist (add to ship-it pre-flight)

- [ ] Data-inventaris klopt met wat de site echt doet
- [ ] Privacyverklaring live, gelinkt in footer
- [ ] Geen tracking zonder voorafgaande, weigerbare consent — of beter: geen tracking
- [ ] Formulieren minimaal; nieuwsbrief is losse opt-in met unsubscribe
- [ ] Bedrijfsinfo/KvK waar verplicht
- [ ] HTTPS aan (ship-it) — onversleutelde persoonsgegevens zijn ook een AVG-probleem
- [ ] Bij betalingen, gezondheidsdata, kinderen, of twijfel: échte jurist genoemd aan de user

## Hard boundary

Draft texts and checklists: yes. "Dit is juridisch waterdicht": never say it. When stakes rise (boetes, contracten, bijzondere persoonsgegevens), the deliverable includes the explicit advice to have it reviewed professionally.
