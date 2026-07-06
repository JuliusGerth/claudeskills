---
name: responsive-craft
description: 'Make every interface work from a 320px phone to a 4K desktop - mobile-first build order, breakpoints where the CONTENT breaks, fluid type and spacing with clamp(), touch-safe interactions, and a fixed test matrix. Use this skill whenever building any page or app (most visitors are on phones), whenever the user says "op mobiel is het kapot", "werkt niet op mijn telefoon", "responsive", or shows a screenshot with overflow, squashed columns, or unreadable text. Goes deeper than the responsive gate in frontend-quality-gates - this is the dedicated multi-screen pass; layout-bug triage lives in bug-hunt.'
---

# Responsive Craft

More than half of web traffic is phones, yet interfaces are built on a wide desktop monitor — so mobile becomes an afterthought squeeze. Result: overflow, microscopic text, untappable buttons. The fix is a build order, not a pile of media queries.

## Mobile-first: build the smallest screen FIRST

Design and build at ~375px wide, then widen the window and enhance where space allows. This direction works because small screens force the real decisions — what matters most, what can go — while desktop-first hides those decisions until they explode on mobile. CSS agrees: base styles = mobile, `@media (min-width: …)` adds complexity upward. Desktop-first `max-width` queries mean overriding complexity downward, which is where responsive spaghetti comes from.

Mobile-first is also a priority filter: if something has no place on the phone layout, ask whether it earns its place at all.

## Breakpoints: where the content breaks

Set breakpoints by resizing until the layout becomes awkward — THAT is a breakpoint. Not at "iPad width": device widths are legion and change yearly; your content is the constant. In practice most projects land near ~640 / ~768 / ~1024px, but the content decides, and fewer breakpoints beats many.

Modern layout needs fewer breakpoints than you think:

- `grid-template-columns: repeat(auto-fit, minmax(250px, 1fr))` — a card grid that reflows itself, zero media queries.
- `flex-wrap: wrap` with `flex: 1 1 <basis>` — toolbars and tag rows that wrap naturally.
- For reusable components inside variable slots (sidebar vs main): container queries (`@container`) respond to the slot, not the viewport.

## Fluid beats stepped

- Type: `font-size: clamp(1rem, 0.9rem + 1vw, 1.25rem)` scales smoothly; headings roughly `clamp(1.5rem, 1.2rem + 3vw, 3rem)`. No jump at a magic width.
- Spacing: same trick for section padding (`clamp(2rem, 8vw, 6rem)`), so whitespace breathes with the screen (pixel-polish rhythm survives all widths).
- Reading width: cap prose at `max-width: 65ch` — full-width text on desktop is unreadable.
- Never fixed heights on text containers (bug-hunt layout suspect #1); let content size the box.
- Body text ≥ 16px always — smaller is unreadable AND triggers iOS zoom on inputs (form-craft).

## Touch is not hover

- Tap targets ≥ 44×44px with spacing between destructive neighbors — fingers are not cursors.
- Hover does not exist on touch. Anything ONLY reachable via hover (menus, tooltips, action buttons that appear) is unreachable for most visitors: give it a tap path. Use `@media (hover: hover)` to gate hover-only decoration (motion-craft effects included).
- Thumb zone: primary actions low on the screen are easier one-handed; do not park the main CTA top-right on mobile.
- Mobile browser chrome eats viewport: prefer `100dvh` over `100vh`, or the bottom of full-height sections hides behind the URL bar.

## The classic overflow killers

Horizontal scroll on mobile is almost always one of: a fixed `width` in px on a container, an unshrinkable flex child (`min-width: 0` missing), an unsized image, a long unbroken string (URL) needing `overflow-wrap: break-word`, or negative margins wider than the parent. Find it fast: outline everything (`* { outline: 1px solid red }`) or in devtools delete DOM halves — binary search, per bug-hunt.

## Test matrix (run BEFORE delivery, every time)

- [ ] 320px — the honest minimum: nothing overflows, everything readable
- [ ] ~375px — standaard telefoon: primaire flow werkt met duim
- [ ] ~768px — tablet: gebruikt de layout de ruimte of is het uitgerekt mobiel?
- [ ] ~1280px+ — desktop: leesbreedtes begrensd, geen zwevende eilandjes
- [ ] Browser-zoom 200% op desktop — layout houdt stand (en het is een a11y-eis, zie accessibility-review)
- [ ] Eén echte telefoon vóór livegang (ship-it smoke test) — de emulator vergeeft dingen die duimen niet vergeven

Deliver nothing that fails at 320px; that width is where all responsive sins surface first.
