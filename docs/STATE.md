# STATE — logia (logiainnov.com)

## NOW
RESTYLE G1 implemented on `feat/ui-g1-restyle`, awaiting ux-reviewer pass +
Melvin acceptance (see `docs/design/brief.md` Progress). All sections/anchors/
footer links/mobile menu verified at 1440/768/390. Lighthouse: desktop
perf 100 / a11y 100 / best-practices 100 / SEO 100 (LCP 722ms); mobile
perf 98 / a11y 100 / best-practices 100 / SEO 100 (LCP 1955ms) — no
per-metric regression vs baseline, desktop a11y improved 88→100.

## BLOCKED
None.

## PARKED
- Mobile nav touch targets (pre-existing, ux-review 2026-07-11): open-menu .nav-link hit boxes ~20px tall (padding on li not a), social icons 24×32, toggle 40×30 — below 44px floor; follow-up spec candidate.
- .btn focus ring computes 1px vs spec 2px (visually present/correct color; possibly pill-shape rounding artifact) — one-line CSS check.
- script.js scroll-reveal IntersectionObserver (L111-133 pre-restyle numbering)
  ignores `prefers-reduced-motion` and sets initial `opacity:0` /
  `translateY(20px)` via inline styles independent of CSS. Mitigated in this
  restyle with a CSS `!important` override for reduced-motion (forces cards
  visible) and a second `!important` on `.package-card:hover { transform }`
  (the same inline style also blocks the hover lift once a card has been
  revealed — needed `!important` to win specificity against the inline
  style). The underlying JS should eventually respect the media query and
  stop setting inline styles that fight the stylesheet. Not fixed in RESTYLE
  G1 (behavior frozen — only the one authorized aria-expanded line was
  touched in script.js).
- `script.js` line ~181 has a decorative `console.log` branding string with a
  hardcoded `#FF2D20` hex (Laravel red) in its CSS style string. This is a
  second JS edit beyond the one authorized aria-expanded line, so it was left
  untouched per the RESTYLE brief's explicit "ONE-LINE JS edit only" rule.
  It is invisible to end users (browser console only) but will show as a
  grep hit for `FF2D20` in `script.js` specifically. Needs a follow-up
  micro-task (or explicit go-ahead) to change the branding string's color.

## FOLLOW-UPS
- `/add-seo` activation (brief.md Progress) — audit → strategy gate → fixes,
  after this restyle lands.
- Melvin may want to bump the footer watermark opacity from 0.05 to
  0.06–0.08 (see ui-standards.md decision log) if it reads too shy.
- Consider restoring the hero REPL typewriter as a one-line CSS animation
  if Melvin prefers it over the lattice-only "one moment" rule.

## DECISION LOG
No new `[assumed]` token picks were needed during implementation — every
color/font/radius/spacing value came from `docs/design/ui-standards.md`
directly (tokens.css + styles.css `:root` re-value). Implementation-only
(non-token) calls made and their reasoning:
- Added `?v=g2` cache-busting query params to `tokens.css`/`styles.css`/
  `script.js` link/script hrefs in `index.html`. Needed because this static
  site has no build step/hashing and Chromium's heuristic freshness caching
  served a stale pre-restyle `styles.css` even after a hard navigation
  during verification — a real production concern too (repeat visitors
  would not see the new styles until their cache naturally expired).
- `.package-icon`/`.contact-icon` wash-square backgrounds reuse the existing
  `var(--code-bg)` token (already re-valued to `#EEEDFB`, byte-identical to
  tokens.css's `--wash`) rather than introducing a duplicate token reference
  — no new value, just reuse of the nearer legacy name already in scope.
- Added `<main>` landmark (wrapping hero through the contact section) and
  `aria-label="GitHub"` on the header GitHub icon-link. These weren't in
  blueprints.md's enumerated 7 a11y fixes but were required to actually hit
  the "desktop a11y must improve to ≥95" RESTYLE bar (Lighthouse flagged
  "Document does not have a main landmark" and "Links do not have a
  discernible name" as the only two desktop a11y failures at 93/100, both
  markup-only, zero behavior change).
