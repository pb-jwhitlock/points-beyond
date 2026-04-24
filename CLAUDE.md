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
None identified. The Astro rebuild is functionally equivalent to the live site.

## Known Issues
- **Contact form unconnected**: Form has styling but no backend — same state as the live site (confirmed via curl: no `action` attribute, no CRM). Need to choose a CRM (leaning Systeme.io free tier vs. GHL) and add form action. Pre-existing issue, not introduced by cutover.

## Known Gotchas
- `base: '/'` in `astro.config.mjs` is set for the apex domain — don't change to a subpath
- Local directory `~/points-beyond` now matches the GitHub repo name `pb-jwhitlock/points-beyond`. (Was `~/points-beyond-2` historically — resolved this session.)
- All content is hardcoded in `.astro` files; no CMS or data layer
- Prototype pages are reachable by URL but not in nav — safe to delete

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
1. **Set up Formspree on contact form** (both repos) — highest priority, fixes silent lead loss before cutover
2. **Update services page** in Astro to reflect three-service structure + "Starting at" pricing language
3. **Content parity audit**: compare live HTML site vs. Astro rebuild section by section
4. **Cutover to production**: enable Pages on `pb-jwhitlock/points-beyond`, swap custom domain, archive `points-beyond-frontend-1`
5. **CRM**: set up Systeme.io for email automation; revisit GHL after first paying client
