# UI standards — logia (logiainnov.com)

Status: **Approved direction (inherited)** — this is the Logia brand kit Melvin
approved 2026-07-11 on logia-admin, applied to the public marketing site.

## SHARED BRAND — keep in sync
This file is a MIRROR of logia-admin's `docs/design/ui-standards.md` (the
canonical brand kit). Palette hexes, the type trio, the lattice signature, and
the logo are ONE brand across both properties. If a brand value changes, it
changes in logia-admin FIRST, then this mirror is updated to match. Do not fork
brand values here — only the *mechanism* below is project-specific (static
CSS-variable stylesheet vs. the admin's Tailwind 4 `@theme`).

## Palette (identical to the kit — AA verified against real pairings here)
| Token | Hex | Role & pairing on THIS page |
|---|---|---|
| Ink | #17162B | body text, headings — 16:1 on Ground, 17:1 on white |
| Ground | #F6F7FB | page + section background (cool off-white) |
| Surface | #FFFFFF | cards, nav bar |
| Logia Indigo | #3A2FB5 | THE accent — CTA fill, links, eyebrows, icons, lattice nodes, logo. ~8.9:1 as text on white; 9.3:1 white-on-indigo. Spent sparingly |
| Indigo-deep | #2E2593 | button hover/active, focus ring; 11.6:1 white-on |
| Muted | #5B6072 | secondary text, footer tagline; 5.8:1 on Ground |
| Hairline | #E2E4EF | borders, dividers, dot-grid dots |
| Indigo-wash | #EEEDFB | banner bar, icon squares; Ink-on-wash 15:1 |

Red #FF2D20 (Laravel vermilion) is eradicated — it was never a brand color.
No status hues on this page (marketing surface).

## Typography
- Display: **Bricolage Grotesque 700**, tracking -0.02em — hero H1
  (`.hero-title`) + section titles (`.ecosystem-title`) + footer watermark ONLY.
- Body/UI: **Inter** 400/500/600 — everything else, incl. card titles.
- Mono: **JetBrains Mono 500** — eyebrows (`.section-label`), hero REPL line,
  Approach step numerals.
- Scale: H1 clamp(2.75rem,5vw,4.25rem)/1.02 · section title 2rem/1.1 · card
  title 1.125rem/1.3 · lead 1.125–1.25rem/1.6 · body 1rem/1.6 · eyebrow
  0.8125rem uppercase tracking 0.08em. Phone: H1 2.25rem, section title 1.5rem.
- Self-hosted woff2, latin subset, used weights only, `font-display: swap`.
  NO Google Fonts CDN.

## Spacing / radius / density
- 8px scale. `--radius: 0.625rem`; cards 12px (0.75rem, current value kept);
  CTA = pill 9999px; icon squares 12px; banner/wash chips 6px.
- **Airy** — the only airy Logia surface besides logia-admin's landing
  (section pad 96px desktop / 64px phone, current values kept).

## Signature element — the logic lattice
Faint hairline dot-grid (32px pitch) on **hero + footer**, sparse nodes joined
by hairline segments; **4 indigo junction nodes** (hero; 2 in footer). The ONLY
indigo background field. Replaces `.hero-gradient`/`.hero-pattern`. Adapted to
the centered hero: nodes live in the side margins (x<300 / x>1140), never
behind the headline column.

## Motion
- One orchestrated moment: hero lattice draws on load (~650ms lines
  cubic-bezier(0.4,0,0.2,1), nodes fade+scale staggered ~80ms; ~1s, once).
- Micro-feedback elsewhere: CTA 150ms translateY(-1px)+shadow; card hover
  150ms border+lift. Hero title/desc keep their gentle fadeInUp.
- Reduced-motion: lattice fully drawn; fadeInUp elements FORCED to opacity:1
  (they start at 0 — without the guard, reduced-motion users see nothing);
  CTAs color-change only.
- `[assumed]` Hero REPL typewriter/blink dropped — the lattice is the single
  hero moment (kit rule). Implementer: set `width:auto`, remove border-right
  cursor when removing the animation.

## Component rules
- Buttons: primary = indigo pill, white label, no rest shadow, hover →
  indigo-deep + translateY(-1px) + shadow. Secondary = ghost, ink, 1px
  hairline, hover Ground tint. Focus: 2px indigo-deep ring, 2px offset.
- Cards: white, 1px hairline, radius 12px, no rest shadow; hover border→indigo
  + soft indigo shadow + 1px lift. Flat (`[assumed]` no corner bleed across
  9-card grids — lattice carries the signature).
- Icon squares: 48px (grids) / 40px (contact), Indigo-wash bg, radius 12px,
  Lucide icon Indigo 1.75px stroke. Approach steps use mono indigo numerals
  1/2/3 in the square (`[assumed]` — numbers carry sequence meaning).
- Icons: Lucide only, 1.75px. EXCEPTION `[assumed]`: social brand glyphs
  (GitHub/X/YouTube/Discord) keep existing monochrome paths (Lucide has no
  brand marks) — Muted, Indigo on hover.
- Logo: indigo transparent mark (logo-indigo.png + webp variants copied from
  logia-admin). Footer's old red SVG box replaced by the real mark.
- Banner bar `[assumed]`: Indigo-wash bg + Ink text + indigo arrow (not solid
  indigo — would compete with the lattice; not dropped — parity).

## Mechanism (STATIC SITE — project-specific)
Two plain stylesheets, no build step:
1. **tokens.css** (NEW, linked BEFORE styles.css): @font-face blocks (5 latin
   woff2 files vendored to fonts/), brand additive tokens
   (--font-display/-sans/-mono, --indigo, --indigo-deep, --wash,
   --radius-pill), dot-grid utility, lattice classes + keyframes copied
   verbatim from logia-admin's proof.html so both properties animate
   identically.
2. **styles.css** `:root` re-valued (old names, brand values — the sheet
   already var()s every accent, so this recolors ~90% automatically):
   --primary-color:#3A2FB5; --primary-dark:#2E2593; --text-primary:#17162B;
   --text-secondary:#5B6072; --text-light:#5B6072; --bg-light:#F6F7FB;
   --bg-white:#FFFFFF; --border-color:#E2E4EF; --code-bg:#EEEDFB;
   Hardcoded hexes/gradients get surgical edits per blueprints.md.

@font-face spec (fonts/ from Fontsource latin):
Bricolage Grotesque 700, Inter 400/500/600, JetBrains Mono 500 — all
`font-display:swap`, woff2 only. Head drops both Google preconnects + the
fonts.googleapis link.

## Assets
logo-indigo.png master + img/logo-{64,128}.webp (from logia-admin public/);
favicon set (32/16 png, apple-touch 180, favicon.ico) derived from the master
— the site currently has NO favicon links; add them. Lattice SVG markup in
blueprints.md. twitter:image → https://logiainnov.com/logo-indigo.png.

## Decision log
- `[assumed]` entries above (banner wash, Ground sections, flat cards, mono
  numerals, typewriter dropped, social-glyph exception, footer watermark
  indigo at 0.05 opacity — Melvin may bump 0.06–0.08 in review).
