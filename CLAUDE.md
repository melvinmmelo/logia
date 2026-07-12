# CLAUDE.md

## What this is
**logia** — Logia Innovations' main marketing website (logiainnov.com).
ONE-page plain static site: `index.html` + `styles.css` + `tokens.css` +
`script.js`. No framework, no build step, no auth, no DB. The `steward/`
dir holds a DIFFERENT app's Play-Store docs (privacy policy Google requires
at a stable URL) — leave it alone; robots.txt excludes it from SEO.

## ⚠ Push = PRODUCTION deploy
`origin/main` auto-deploys to **logiainnov.com via Vercel** (behind
Cloudflare DNS). `git push` on main IS a production release → needs
Melvin's explicit per-instance GO (global rule 1), like /deploy. Merge
locally, hold the push, ask.

## Running & verifying
```bash
python3 -m http.server 8090        # local serve (check if already running)
npx lighthouse http://127.0.0.1:8090/ --output=json   # perf/SEO checks
```
No lint/test pipeline — the gate is: curl checks (title/canonical/JSON-LD
in initial HTML), screenshots at 1440/768/390, Lighthouse vs the committed
baselines in `docs/design/references/lighthouse-baseline/` (RESTYLE bar:
no regression) and `docs/design/review/*-lh.json`.

## Conventions
- Design system: `docs/design/ui-standards.md` — a MIRROR of the canonical
  Logia brand kit in `logia-admin/docs/design/ui-standards.md`; brand
  values change there first. Tokens live in `tokens.css` + re-valued
  `styles.css :root`; fonts are self-hosted latin woff2 in `fonts/` (no
  CDN).
- SEO: `docs/seo/` (audit, strategy incl. approved title/meta words —
  "Philippines" removed from customer-facing copy per Melvin 2026-07-12;
  og-card regeneration source: `docs/seo/og-card-source.html`).
- Branching: `feat/*` per group/concern, squash-merge to main (rule 9).

## Gotchas
- **`.vercelignore` excludes `docs/`** — the repo root is the webroot on
  Vercel; without it, internal docs get publicly served (happened
  2026-07-12, sealed same day). After any deploy touching new dirs:
  `curl -s -o /dev/null -w "%{http_code}" https://logiainnov.com/docs/seo/strategy.md`
  must be 404.
- www.logiainnov.com should 301 to the apex — Vercel dashboard setting
  (Melvin's toggle); the canonical tag mitigates until then.
- script.js scroll-reveal sets inline transforms (CSS hovers need
  !important) and ignores reduced-motion — PARKED in docs/STATE.md.
