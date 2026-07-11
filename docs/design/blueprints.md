# Screen blueprints — logia restyle (one page, one rollout group)

Designer mapping 2026-07-11. Legend: CHANGE = restyle edit · KEEP = frozen.
Line refs are styles.css unless noted. Copy is FROZEN (SEO round owns copy).
States: responsive (1440/768/390), reduced-motion, hover/focus. Parity: every
section/anchor/nav item/link and the mobile menu survive; Dropped: none.

## 0. <head>
- CHANGE remove Google Fonts preconnects + link (index L18–20); add
  `<link rel="stylesheet" href="tokens.css">` before styles.css; add favicon
  set (favicon-32/16 png, apple-touch-icon 180, favicon.ico) — none exist today.
- CHANGE twitter:image (L15) → https://logiainnov.com/logo-indigo.png.

## 1. Banner (.banner L38–45)
- CHANGE bg #FF2D20 → var(--wash); color → Ink; trailing arrow indigo.
- KEEP text verbatim, padding, single-line phone wrap.

## 2. Nav (.navbar)
- KEEP sticky/blur/layout/5 anchors/toggle behavior.
- CHANGE logo markup (index L32–37): `<picture><source srcset="img/logo-128.webp"
  type="image/webp"><img src="logo-indigo.png" alt="Logia Innovations"
  class="logo-img"></picture>` (fixes current bug: webp <source> pointed at JPEG).
- CHANGE a11y: toggle gets aria-expanded="false" + aria-controls="nav-menu";
  .nav-menu gets id="nav-menu"; hamburger spans aria-hidden="true"; JS flips
  aria-expanded (ONE line in script.js — the sole JS touch, a11y remit).
- Hover states indigo via token flip.

## 3. Hero — signature lands here
- CHANGE delete .hero-gradient (L189–197), .hero-pattern (L199–209),
  @keyframes patternFloat (L211–214). Hero gets dot-grid background
  (radial-gradient hairline dots, 32px pitch) + this lattice SVG as first
  child of .hero-background (classes/keyframes from tokens.css):

```html
<svg class="lattice-svg hero-lattice" viewBox="0 0 1440 560" preserveAspectRatio="xMidYMid slice" aria-hidden="true">
  <path class="lattice-line" style="animation-delay:0ms"   d="M1140 90 L1240 170"/>
  <path class="lattice-line" style="animation-delay:80ms"  d="M1240 170 L1160 300"/>
  <path class="lattice-line" style="animation-delay:120ms" d="M1240 170 L1320 110"/>
  <path class="lattice-line" style="animation-delay:180ms" d="M1320 110 L1380 260"/>
  <path class="lattice-line" style="animation-delay:220ms" d="M1380 260 L1280 380"/>
  <path class="lattice-line" style="animation-delay:260ms" d="M1160 300 L1280 380"/>
  <path class="lattice-line" style="animation-delay:300ms" d="M60 170 L160 220"/>
  <path class="lattice-line" style="animation-delay:340ms" d="M160 220 L90 360"/>
  <path class="lattice-line" style="animation-delay:380ms" d="M160 220 L240 180"/>
  <path class="lattice-line" style="animation-delay:420ms" d="M90 360 L200 420"/>
  <circle class="lattice-node"       style="animation-delay:600ms" cx="1240" cy="170" r="6"/>
  <circle class="lattice-node"       style="animation-delay:660ms" cx="1320" cy="110" r="6"/>
  <circle class="lattice-node"       style="animation-delay:720ms" cx="1280" cy="380" r="6"/>
  <circle class="lattice-node"       style="animation-delay:780ms" cx="160"  cy="220" r="6"/>
  <circle class="lattice-node-plain" style="animation-delay:640ms" cx="1140" cy="90"  r="4"/>
  <circle class="lattice-node-plain" style="animation-delay:700ms" cx="1160" cy="300" r="4"/>
  <circle class="lattice-node-plain" style="animation-delay:760ms" cx="1380" cy="260" r="4"/>
  <circle class="lattice-node-plain" style="animation-delay:820ms" cx="60"   cy="170" r="4"/>
  <circle class="lattice-node-plain" style="animation-delay:860ms" cx="240"  cy="180" r="4"/>
  <circle class="lattice-node-plain" style="animation-delay:900ms" cx="90"   cy="360" r="4"/>
  <circle class="lattice-node-plain" style="animation-delay:940ms" cx="200"  cy="420" r="4"/>
</svg>
```
  Nodes stay in x<300 / x>1140 margins — never behind the centered headline.
  .hero-content gets position:relative;z-index:1.
- CHANGE .hero-title (L220–229): clamp(2.75rem,5vw,4.25rem)/1.02,
  font-family var(--font-display). KEEP fadeInUp (+ reduced-motion guard).
- CHANGE .text-highlight (L231–239): delete gradient/background-clip lines →
  solid color var(--primary-color).
- CHANGE .btn (L259–269): radius → var(--radius-pill); transition 150ms.
  .btn-primary (L271–281): no rest shadow; hover indigo-deep + translateY(-1px)
  + shadow rgba(46,37,147,.28). .btn-secondary (L283–294): 1px hairline,
  hover Ground tint + lift; drop dark fill/heavy shadow.
- CHANGE .code-snippet (L296–316): border-left indigo, bg wash, font mono;
  DROP typewriter: code{width:auto}, remove animation + border-right cursor;
  .code-prompt static indigo.
- CHANGE dead-code hygiene .stat-number gradient (L339–349) → solid
  var(--primary-color) (hero-stats is commented out; no stray red survives).
- Phone ≤768: H1 2.25rem; hide lattice LINES keep nodes:
  `@media(max-width:768px){.hero-lattice .lattice-line{display:none}}`.

## 4. Section-header pattern (applies §4–10)
- .section-icon (L414–416): Lucide 24px 1.75px indigo. Per section: About →
  layers, What We Do → boxes, Approach → code-xml, Why Logia → sparkles,
  Services list → layout-grid, Technology → cpu, Contact → message-square.
- .section-label (L418–424): mono 500, 0.8125rem, 0.08em, indigo, uppercase.
- .ecosystem-title (L426–432): var(--font-display), 2rem/1.1, Ink.
- .ecosystem (L402–405): background var(--bg-light); add body{background:
  var(--bg-light)}. Descriptions → Muted (auto). Copy KEEP.

## 5. What We Do — 4 cards with icons
- .package-card (L487–502): white/hairline/12px KEEP radius; 150ms; hover
  border indigo + shadow rgba(58,47,181,.10) + translateY(-1px).
- Replace 4 data-URI letter-blocks (index L179/191/203/215) with Lucide in
  48px wash squares (.package-icon restyle: 48px, radius 12, wash bg, flex
  center; svg 24px indigo 1.75): square-code / sparkles / trending-up /
  life-buoy.

## 6. Approach — 3 steps
- Same card treatment; icon slot = mono numeral 1/2/3 (JetBrains 500,
  1.25rem, indigo) inside the 48px wash square, replacing data-URIs
  (index L246/258/270).

## 7. Why Logia — 4 cards, no icons: card restyle auto. KEEP structure.
## 8. Services list — 9 title-only cards: restyle auto. KEEP all 9.
## 9. Technology — 5 cards: restyle auto; two descriptions stay Muted.

## 10. Contact — 4 cards, emoji → Lucide
- Replace emoji in .package-name (index L484/493/500/507) with 40px wash
  squares centered ABOVE the label (.contact-icon: 40px, radius 12, wash,
  centered; svg 20px indigo 1.75): mail / phone / map-pin / globe.
- Email link: keep underline, color indigo `[assumed]` (primary action
  affordance; not color-alone — underline stays). KEEP inline grid styles.

## 11. Footer — dot-grid + small lattice
- .footer (L547–552): bg Ground + dot-grid; insert as first child (content
  z-index:1):

```html
<svg class="lattice-svg footer-lattice" viewBox="0 0 1440 360" preserveAspectRatio="xMidYMid slice" aria-hidden="true">
  <path class="lattice-line" style="animation-delay:0ms"   d="M1180 60 L1280 120"/>
  <path class="lattice-line" style="animation-delay:120ms" d="M1280 120 L1200 220"/>
  <path class="lattice-line" style="animation-delay:180ms" d="M1280 120 L1360 90"/>
  <path class="lattice-line" style="animation-delay:240ms" d="M1360 90 L1340 240"/>
  <path class="lattice-line" style="animation-delay:300ms" d="M1200 220 L1340 240"/>
  <circle class="lattice-node"       style="animation-delay:600ms" cx="1280" cy="120" r="5"/>
  <circle class="lattice-node"       style="animation-delay:680ms" cx="1340" cy="240" r="5"/>
  <circle class="lattice-node-plain" style="animation-delay:640ms" cx="1180" cy="60"  r="4"/>
  <circle class="lattice-node-plain" style="animation-delay:720ms" cx="1360" cy="90"  r="4"/>
  <circle class="lattice-node-plain" style="animation-delay:760ms" cx="1200" cy="220" r="4"/>
</svg>
```
- Footer logo (index L520–525): red SVG box → `<img src="logo-indigo.png"
  alt="Logia Innovations" width="48" height="48">`; CSS rule updated to img.
- .footer-tagline (L572–577): Muted (was red) `[assumed]`.
- Social links: Muted default, indigo hover; KEEP 4 brand glyphs (exception).
- .footer-logo-large h2 (L655–660): var(--font-display), indigo, opacity 0.05
  (`[assumed]` — 0.03 indigo nearly invisible; Melvin may bump to 0.06–0.08).
- Remove duplicate id="contact" from <footer> (index L516) — section owns it.
- Phone: KEEP existing collapses; hide footer lattice lines ≤768 like hero.

## A11y fixes (cosmetic scope; baseline desktop 88 → target ≥95)
1. :focus-visible (L890–893): outline 2px var(--primary-dark), offset 2px.
2. Muted contrast: token flip moves #6B7280→#5B6072 (5.8:1); remap #9CA3AF
   (--text-light) to Muted (kills latent fail in dead .search-shortcut).
3. Toggle ARIA (blueprint §2) + one-line JS aria-expanded flip.
4. Reduced-motion guard (NEW @media block): force opacity:1 on
   .hero-title/.hero-description/.hero-buttons/.code-snippet (they start at 0
   — latent invisibility bug), lattice static, card reveals static.
5. Duplicate id="contact" removed.
6. Alt text: nav + footer marks alt="Logia Innovations"; lattice + watermark
   aria-hidden="true".
7. Contact links keep underline (never color-alone).
PARKED (behavior, frozen): script.js scroll-reveal ignores reduced-motion and
hides cards if JS fails — record in docs/STATE.md, don't fix here.

## Rollout
One group: G1 = the whole page (index.html, styles.css, tokens.css, fonts/,
img/, script.js one-line ARIA touch) on feat/ui-g1-restyle. Verification:
1440/768/390 screenshots vs references/logia-current-desktop.png parity +
Lighthouse RESTYLE bar (baseline mobile 92 / desktop 99, LCP 2.7s/0.8s, SEO
100 — no per-metric regression; desktop a11y 88 must IMPROVE).

## Open questions (Melvin, at review)
1. Footer watermark opacity 0.05 — bump to 0.06–0.08 if too shy.
2. Typewriter dropped for the single-hero-moment rule — restorable one-line
   if he prefers it over the lattice draw.
