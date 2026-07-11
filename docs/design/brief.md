# Design brief — logia (main website, logiainnov.com)

Status: Approved direction (inherits the Logia brand kit Melvin approved
2026-07-11 on logia-admin — same company, same brand)
Mode: RESTYLE (static HTML/CSS/JS stays; token layer + overrides; behavior
frozen — anchor nav, mobile menu, all sections keep working)

## Product
Logia Innovations' public marketing site — one page, static, deployed at
logiainnov.com. Melvin 2026-07-11: "this is our main website. update this
also, activate also seo."

## Users & top tasks
| User group | Top tasks (by frequency) | Device mix |
|---|---|---|
| Prospective SMB clients | understand what Logia does, judge legitimacy, contact (email/phone) | mixed, phone-heavy |
| Existing clients from emails | recognize the company, find contact | phone-likely |

## Local run & test logins
Static — `python3 -m http.server 8090` in the project dir. No auth.

## Brand inputs
**The approved Logia brand kit** (logia-admin `docs/design/ui-standards.md`,
approved + logo-recolor reversal 2026-07-11): Logia Indigo #3A2FB5 accent,
Ink/Ground/Surface/Muted/Hairline/Indigo-wash palette, Bricolage Grotesque
display + Inter body + JetBrains Mono utility, logic-lattice signature,
indigo transparent-background logo mark (master `logo-indigo.png` in
logia-admin — copied here). Current site is Laravel-red #FF2D20 — replaced
everywhere (it was never a chosen brand color).

## References
| Ref (file in references/) | What to take from it |
|---|---|
| logia-current-desktop.png | the parity record — every section survives |
| lighthouse-baseline/*.json | RESTYLE bar: mobile 92 / desktop 99 perf, LCP 2.7s/0.8s, SEO 100 — no regression. Desktop a11y 88 is pre-existing debt: improve, don't inherit |
| (logia-admin approved design: its docs/design/proof.html + live home page) | the brand execution to match — this site is the same company's face |

## Scope
One page (index.html + styles.css + logo assets). Content/copy stays
(SEO pass owns copy changes separately); this restyle is visual: tokens,
type, logo swap, icon cleanup (the letter-block data-URI icons → Lucide
inline SVGs), lattice signature in hero/footer, red → indigo everywhere.
`steward/` untouched.

## Parity (RESTYLE rule)
Every section, anchor, nav item, contact link, and the mobile menu appear
in the restyled page. Dropped: none.

## Decision log
- `[assumed]` Proof gate skipped per RESTYLE proceed-mode: the reference is
  Melvin's own approved brand executed on logia-admin — he corrects in review.
- `[assumed]` Copy unchanged in the restyle round (SEO round may retitle
  per strategy — separately gated).
- `[assumed]` Google-Fonts CDN replaced by self-hosted woff2 (brand rule:
  no external font CDN) — also removes a third-party call.

## Progress
- [x] Brief drafted; baseline + parity captured (mobile 92/desktop 99)
- [x] ui-designer section mapping → blueprints.md + ui-standards.md written
- [x] Restyle implemented (one rollout group) — gates + parity green
- [x] ux-reviewer pass 2026-07-11: PASS, 0 blockers — desktop 100/100/100/100, mobile 98/100/100/100, a11y 88→100
- [x] /add-seo activated — audit + strategy in docs/seo/ (gate: Melvin)
- [ ] Melvin acceptance
