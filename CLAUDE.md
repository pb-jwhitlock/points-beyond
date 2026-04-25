# Points Beyond AI — Project Guide

## Overview
Company website for Points Beyond AI / Points Beyond LLC (John Whitlock).
AI content strategy consultancy in Fairfax County, VA — services: AI Voice Agents, Answer Engine Optimization (AEO), SEO.

**Live site**: https://pointsbeyond.ai — currently served from `points-beyond-frontend-1` (plain HTML repo).
**This repo**: GitHub repo is `pb-jwhitlock/points-beyond`; local directory is `~/points-beyond`. Astro 5 rebuild — in progress, not yet deployed.

## Stack / Architecture
- **Framework**: Astro 5.x (SSG, static output)
- **Fonts**: Urbanist (Google Fonts, primary) + Inter
- **Styling**: Raw CSS in `.astro` component `<style>` blocks — no Tailwind, no CSS framework
- **No content collections** — all page content is inline in `.astro` files
- **Layouts**: `Layout.astro` (light), `Layout-dark.astro`
- **Components**: `Header.astro`, `Footer.astro`

## Pages
| Route | File | Notes |
|---|---|---|
| `/` | `index.astro` | Hero, features, services overview |
| `/about/` | `about.astro` | |
| `/services/` | `services.astro` | |
| `/contact/` | `contact.astro` | |
| `/faq/` | `faq.astro` | |
| `/payment/` | `payment.astro` | |
| `/privacy/` | `privacy.astro` | |
| `/prototype-ctrl/` | `prototype-ctrl.astro` | Design exploration — not production |
| `/prototype-refined/` | `prototype-refined.astro` | Design exploration — not production |
| `/prototype-tech/` | `prototype-tech.astro` | Design exploration — not production |
| `/prototype-warm/` | `prototype-warm.astro` | Design exploration — not production |
| _(archived)_ | `index-original.astro` | Pre-redesign reference — delete when done |

## Design System
- **Primary accent**: `#2e1f7a` (rich indigo/navy-purple)
- **Background**: Pure white
- **Font**: Urbanist (headings + body), Inter (secondary)
- Note: went through many palette iterations before settling here

## Current State
- [x] All core pages built, content complete
- [x] SEO/AEO/Schema markup added
- [x] GitHub Actions deploy workflow configured (push to main → Astro build → Pages artifact)
- [x] Content parity audit completed (April 25, 2026) — 16 items identified, 5 are P1 blockers
- [ ] **P1 blockers not yet fixed** — do not cut over until resolved (see Pre-Cutover Blockers below)
- [ ] GitHub Pages not enabled on this repo — `pointsbeyond.ai` still serves from `points-beyond-frontend-1`
- [ ] Prototype pages present but not linked from nav
- [ ] `index-original.astro` still present for reference

## Deployment Workflow
Push to `main` → GitHub Actions builds Astro → uploads `dist/` → deploys to GitHub Pages.

**To cut over to this repo:**
1. Enable GitHub Pages on `pb-jwhitlock/points-beyond` (Settings → Pages → Source: GitHub Actions)
2. Set custom domain to `pointsbeyond.ai`
3. Verify DNS; then disable Pages on `points-beyond-frontend-1`

**Current live repo**: `pb-jwhitlock/points-beyond-frontend-1` — raw HTML, legacy build, custom domain `pointsbeyond.ai`.

## Pre-Cutover Blockers
**Audit (April 25, 2026) found 16 items; 5 are hard blockers that will break the site or silently lose leads:**

1. **CSS variables undefined** — `--color-card-bg`, `--color-card-border`, `--color-card-hover`, `--color-accent`, `--color-accent-rgb` are used across about/contact/services/payment/privacy pages but not defined in `Layout.astro`. Cards will render broken.
2. **Payment page broken link** — `href="#REPLACE_WITH_STRIPE_LINK"` in `payment.astro`. Needs real Stripe URL.
3. **No contact form backend** — Homepage form has `action="#"`. `/contact/` page has no form at all. Leads cannot be captured.
4. **Footer missing Privacy Policy and Terms links** — Live site footer links to both; `Footer.astro` has neither.
5. **No `/terms/` page** — Live site footer links to Terms & Conditions; page doesn't exist in this repo.

**High-visibility content gaps (P2) — homepage missing vs live site:**
- Pain points section ("Every missed call...is lost revenue" — 4 pain points with 80%+ stat)
- Process/timeline section ("From strategy call to live AI system in 7 days")
- Testimonials section (3 named testimonials: Michael R., Sarah L., David T.)
- Inline FAQ on homepage (7+ Q&As)
- Booking form with service interest checkboxes + SMS consent checkbox

**Messaging/positioning drift (P3):**
- Homepage H1 differs: live = "Never Miss a Lead. Be the Answer AI Delivers." / Astro = "Strategic content for the AI search era."
- Brand name inconsistency: live = "Points Beyond AI" / Astro = "Points Beyond" — decide and unify
- Pricing wrong: live = "$397/mo", `faq.astro` FAQ #4 says "$599", services schema says "599", CLAUDE.md says $349 real estate floor
- Contact page copy is old federal/IT consulting messaging; has "Federal Clients" section
- About page overweights TS/SCI clearance and Navy/defense background vs small business AI pivot

**AEO/schema gaps (P4):**
- FAQPage schema only on `/faq/` — not on homepage where most traffic lands
- No LocalBusiness schema despite Northern VA local positioning
- WebSite SearchAction schema on homepage implies a search box that doesn't exist

**Note:** The live site is a **single-page marketing site** — all subpages (/about/, /services/, /contact/, /faq/) return 404. The Astro rebuild introduces multi-page architecture, which is an intentional upgrade but means returning visitors will experience a different UX.

## Known Issues
- **Contact form unconnected**: Homepage form has `action="#"`. `/contact/` page has no form at all. Need Formspree (or equivalent) before cutover — leads are being lost now.
- **Privacy page uses undefined CSS variables** (`--color-accent`, `--color-accent-rgb`) — SMS compliance section will render without styling.

## Known Gotchas
- `base: '/'` in `astro.config.mjs` is set for the apex domain — don't change to a subpath
- Local directory `~/points-beyond` now matches the GitHub repo name `pb-jwhitlock/points-beyond`. (Was `~/points-beyond-2` historically — resolved this session.)
- All content is hardcoded in `.astro` files; no CMS or data layer
- Prototype pages are reachable by URL but not in nav — safe to delete

## Last Session Summary (April 25, 2026)
- Decided to do production cutover today, staged with approval at each checkpoint
- Completed Stage 1: full content parity audit — fetched live site, read all Astro source files, identified 16 pre-cutover items (5 P1 blockers, see Pre-Cutover Blockers above)
- Key audit finding: live site is a single-page marketing site (all subpages 404); Astro rebuild is multi-page — major structural difference, but intentional upgrade
- No code changes made this session — audit report delivered, awaiting approval to proceed with fixes

## Last Session Summary (April 24, 2026)
- Finalized three-service structure (AI Voice Agents, Reputation Management, AEO+SEO) with real estate as the initial vertical and campaign target
- Built out full vertical-specific pricing model: reputation management and AEO scale with business size, voice AI scales with call volume; bundle tiers for solo/mid/multi-location
- Decided public site uses "Starting at" language anchored to real estate rates; higher-complexity clients get custom quotes
- Active cold outreach campaign in development: personalized Loom + SMS (personal phone for TCPA) + AI demo call; email via GHL
- CRM plan: Systeme.io free tier now, migrate to GHL ($97/mo) after first paying client

## Service Positioning & Pricing (decided April 24, 2026)

### Three-Service Structure
1. **AI Voice Agents** — lead offer
2. **Reputation Management** — Google reviews
3. **Answer Engine & Search Optimization** — AEO + SEO bundled

### Pricing by Vertical / Business Size

**AI Voice Agent** — scales with call volume (est. monthly minutes × $0.10 + $200 margin minimum)
| Vertical | Setup | Monthly |
|---|---|---|
| Real estate (solo/team) | $1,500 | $349/mo |
| HVAC / plumbing | $1,500 | $599–799/mo |
| Multi-provider clinic | $1,500 | $799–1,200/mo |

**Reputation Management** — scales with business size
| Size | Setup | Monthly |
|---|---|---|
| Solo / small | $750 | $249/mo |
| Mid-size | $1,000 | $349/mo |
| Multi-location | $1,500–2,500 | $499–799/mo |

**AEO Foundation** — scales with content complexity
| Size | Setup | Monthly retainer (optional) |
|---|---|---|
| Solo / single service | $2,500 | $599/mo |
| Multi-service | $3,500–4,500 | $599/mo |
| Multi-location | $5,000–7,500 | $599/mo |

**Bundle (all three services)**
| Size | Setup | Monthly |
|---|---|---|
| Solo | $3,995 | $797/mo |
| Mid-size | $5,500 | $1,199/mo |
| Multi-location | $7,500–10,000 | $1,599–2,499/mo |

**Early adopter offer**: First 5 clients get 40% off setup in exchange for case study + testimonial.

**Public site pricing**: Use "Starting at" language — real estate rates are the published floor; higher-complexity clients get custom quotes.

### Active Campaign (in development)
Cold outreach to mid-tier Northern VA real estate agents via personalized Loom video + SMS + AI demo call workflow.
- **SMS**: Sent from personal phone (not GHL) for TCPA safety
- **Email automation**: Via GHL

### CRM Decision (pending)
Considering Systeme.io free tier vs. GHL ($97/mo) for own agency CRM and email automation.
- Lean toward GHL once first paying client lands
- Use Systeme.io until then

## Next Steps
Staged cutover in progress — resume at Stage 2 (fixing P1 blockers):

**Stage 2 — Fix P1 blockers (do first, in this order):**
1. Define missing CSS variables in `Layout.astro` (card-bg, card-border, card-hover, accent, accent-rgb)
2. Wire up contact form with Formspree — add to both `index.astro` CTA form and build a real form on `contact.astro`
3. Add Privacy Policy + Terms links to `Footer.astro`
4. Create `/terms/` page (`terms.astro`) — port from live site footer link text
5. Decide Stripe link for `payment.astro` (or note it's not linked from nav so lower urgency)

**Stage 3 — Homepage content parity (P2):**
6. Add pain points section to `index.astro`
7. Add process/timeline section to `index.astro`
8. Add testimonials section to `index.astro`
9. Update homepage H1 to match live site ("Never Miss a Lead. Be the Answer AI Delivers.")
10. Update homepage form fields to match live (service checkboxes, SMS consent)

**Stage 4 — Messaging cleanup (P3):**
11. Fix pricing everywhere: $349/mo floor on homepage, FAQ answer, services schema
12. Decide brand name ("Points Beyond" vs "Points Beyond AI") — update consistently
13. Rewrite contact page copy — remove IT/federal language
14. Soften about page federal-first framing

**Stage 5 — Cutover:**
15. Enable GitHub Pages on `pb-jwhitlock/points-beyond` (Settings → Pages → Source: GitHub Actions)
16. Set custom domain to `pointsbeyond.ai`
17. Verify DNS; then disable Pages on `points-beyond-frontend-1`

**Backlog (post-cutover):**
- Update services page to reflect three-service structure + "Starting at" pricing language
- Add FAQPage schema to homepage
- Consider LocalBusiness schema
- Set up Systeme.io for email automation; revisit GHL after first paying client
