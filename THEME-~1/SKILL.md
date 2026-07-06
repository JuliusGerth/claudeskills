---
name: theme-craft
description: 'Build theming that scales - design tokens as CSS variables (semantic, not literal), dark mode that is designed rather than inverted, a toggle that respects system preference and persists, and no flash of the wrong theme. Use this skill whenever the user asks for dark mode, "donkere modus", light/dark toggle, huisstijl-kleuren doorvoeren, white-label varianten, or seasonal themes; and whenever colors are hardcoded all over a codebase making any restyle a find-and-replace nightmare. Builds on brand-kit (which decides the colors) and feeds pixel-polish (which polishes with them).'
---

# Theme Craft

Hardcoded hex values scattered through a codebase make every restyle a risky find-and-replace, and make dark mode impossible. One token layer fixes both — and dark mode itself is a design job, not a color filter. "Gewoon inverteren" is how you get glowing text on pure black.

## Layer 1 — Tokens: components never see hex

Define once on `:root`, from BRAND.md if it exists:

```css
:root {
  --color-bg: #ffffff;
  --color-surface: #f6f7f9;      /* cards, panels */
  --color-text: #1a1d21;
  --color-text-muted: #5c6470;
  --color-accent: #2563eb;       /* actions only — see brand-kit */
  --color-border: #e3e6ea;
  --color-danger: #b91c1c;
  --shadow-1: 0 1px 3px rgb(0 0 0 / .1);
  --radius: 8px;
  --space-1: 4px; --space-2: 8px; --space-3: 16px; --space-4: 24px; --space-5: 40px;
}
```

Rules that make the layer hold:

- **Semantic names, not literal**: `--color-danger`, never `--color-red` — in another theme danger might not be red, and the name must survive that.
- Components use ONLY tokens. One raw hex in a component is a leak; leaks multiply until the layer is decoration. (Same discipline as component-craft: one source of truth.)
- Spacing/radius/shadows are tokens too — pixel-polish consistency becomes automatic when there are only five spacing values to choose from.
- Tailwind projects: same principle via the theme config — extend the theme with brand tokens; never sprinkle arbitrary values.

## Layer 2 — Dark mode is designed, not inverted

Redefine ONLY the token values; zero component changes — that is the payoff of Layer 1:

- **No pure black, no pure white**: bg ~`#15181c`, text ~`#e8eaed`. Maximum contrast glows and strains eyes at night — exactly when dark mode is used.
- **Elevation flips medium**: shadows are invisible on dark; higher surfaces become slightly LIGHTER instead (`--color-surface` boven `--color-bg`). Redefine `--shadow-*` to near-none + rely on surface steps and borders.
- **Desaturate accents**: saturated brand colors vibrate on dark backgrounds; shift accents lighter and softer. Check contrast in BOTH themes (accessibility-review) — muted text is the classic dark-mode contrast failure.
- Media: full-bleed photos dim slightly (`filter: brightness(.85)` on dark), pure-white illustration backgrounds get a surface-colored wrapper.
- `color-scheme: light dark` on `:root` so scrollbars and form controls follow along natively.

## Layer 3 — The switch, done right

Priority order the user expects: **handmatige keuze (indien ooit gemaakt) > systeemvoorkeur > light**.

- Default path: `@media (prefers-color-scheme: dark)` overrides the tokens — users who never touch the toggle get their OS preference automatically.
- Manual toggle sets `data-theme="dark|light"` on `<html>`; token overrides hang off `[data-theme="dark"]`. Persist the choice (localStorage on real sites — but NOT in Claude artifacts, where storage APIs fail: keep it in-memory state there and default to system preference).
- **No flash of the wrong theme (FOUT... eigenlijk FOUC)**: apply the stored choice in a tiny inline script in `<head>`, before CSS paints — reading it after hydration gives the white-flash-then-dark that makes dark mode feel broken.
- The toggle itself: icon + accessible name, visible in both themes, instant effect. Optional: transition `background-color` ~200ms (motion-craft), but never transition EVERYTHING — text repaints look smeary.

## More themes than two

White-label, seasonal, or per-club varianten are the same mechanism: another `[data-theme="…"]` block redefining the same semantic tokens. If a variant needs new token NAMES, the semantic layer was too literal — fix the names, not the mechanism.

## Verify

- [ ] Grep the components for `#`-hex en rgb( — hoort (bijna) leeg te zijn buiten de tokenlaag
- [ ] Beide thema's: contrastcheck op tekst, muted tekst, accent-op-bg, focus-ringen
- [ ] Systeemvoorkeur dark + eerste bezoek → direct donker, geen flits
- [ ] Keuze overleeft refresh en navigatie; toggle werkt met toetsenbord
- [ ] Afbeeldingen, schaduwen, borders kloppen in dark — niet alleen tekstkleuren
