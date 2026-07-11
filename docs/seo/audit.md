# SEO audit — logiainnov.com (2026-07-11)

Surface: PUBLIC static one-pager (+1 orphan legal page `/steward/privacy-policy.html`).
Audited: LOCAL restyled (feat/ui-g1-restyle @ :8090, curl 200, full content in
initial HTML) + PROD https://logiainnov.com (old version, Vercel behind
Cloudflare). Full evidence in the strategist run 2026-07-11.

## BLOCKER
- **B1. Google's index holds a stale "Apache2 Ubuntu Default Page: It works"**
  — `site:logiainnov.com` returns exactly one result: the placeholder from a
  past unconfigured server. The real site has NEVER been indexed; even the
  brand query doesn't resolve to it. Site is crawlable today → this is a
  re-indexing problem: GSC verify + sitemap submit + re-index request
  (Step 4) gates all other value.

## FOUNDATION
- **F1.** No sitemap.xml (prod 404). Hand-write the one-URL sitemap.
- **F2.** www + non-www both 200 with identical content, NO canonical tag —
  Google guesses the host. Fix: canonical host `https://logiainnov.com`
  `[assumed]`, 301 www at the Vercel/Cloudflare layer, self-referencing
  `<link rel=canonical>`. (http→https already 301s; /index.html duplicate
  also resolved by the canonical.)
- **F3.** No canonical / no og:url (same duplication set).
- **F4.** No structured data. Correct type: **Organization** JSON-LD — NOT
  LocalBusiness (Google requires a postal address for LocalBusiness; Logia
  is home-based and exposes none — verified vs Google's structured-data
  docs). NO FAQPage (no real FAQ on the page; inventing one violates policy).
- **F5.** No og:image; twitter:image is a bare logo. Needs a real 1200×630
  social card (design system generates it).

## GROWTH
- **G1.** Title + H1 spend the strongest signals on the slogan ("Empowering
  Businesses…") — zero service/location keywords; keyword-bearing text sits
  in H3/H4. Rewrites in strategy.md (Melvin's gate — customer-facing words).
- **G2.** One-pager caps rankings: all queries compete for one URL. Content
  gap list in strategy.md.
- **G3.** Business name inconsistent on-page (4 variants) — NAP/entity
  clarity; standardize per strategy.
- **G4.** Dead `href="#"` links (social, Legal/Status, Vision items, nav
  logo) — fix or remove.
- **G5.** Obsolete meta keywords tag — delete (ignored since 2009; also
  telegraphs targets).

## Passes
- Rendering: full content + meta in initial HTML on both versions (static
  site; scroll-reveal only affects opacity, text exists in DOM — Googlebot
  sees it). No SSR concern.
- robots.txt (prod): Cloudflare auto-generated, nothing blocked; needs the
  `Sitemap:` line + `Disallow: /steward/` (keep the Play-Store privacy URL
  reachable but out of Logia's topical signal).
- Heading hierarchy technically clean; Lighthouse SEO category 100.
