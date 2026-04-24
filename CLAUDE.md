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

## Last Session Summary
- Created CLAUDE.md and `/update-context` command; confirmed this is the Astro rebuild of the live plain-HTML site
- Confirmed live site (`points-beyond-frontend-1`) is raw HTML via GitHub Pages + Fastly with no form backend
- Resolved local directory chaos: repo was nested at `~/points-beyond/points-beyond-2/` due to accidental `mv`; cleaned up to canonical `~/points-beyond/` matching GitHub repo name

## Service Positioning & Pricing (decided April 24, 2026)

### Three-Service Structure
1. **AI Voice Agents** — lead offer
2. **Reputation Management** — Google reviews
3. **Answer Engine & Search Optimization** — AEO + SEO bundled

### Pricing (Real Estate Vertical)
| Service | Setup | Monthly |
|---|---|---|
| AI Voice Agent | $1,500 | $349/mo |
| Reputation Management | $750 | $249/mo |
| AEO Foundation | $2,500 (one-time) | $599/mo retainer (optional) |
| Bundle (all three) | $3,995 | $797/mo |

**Early adopter offer**: First 5 clients get 40% off setup in exchange for case study + testimonial.

### Active Campaign (in development)
Cold outreach to mid-tier Northern VA real estate agents via personalized Loom video + SMS + AI demo call workflow.
- **SMS**: Sent from personal phone (not GHL) for TCPA safety
- **Email automation**: Via GHL

### CRM Decision (pending)
Considering Systeme.io free tier vs. GHL ($97/mo) for own agency CRM and email automation.
- Lean toward GHL once first paying client lands
- Use Systeme.io until then

## Next Steps
1. Set up Formspree on contact form (both repos) — fixes silent lead loss
2. Content parity audit: live HTML site vs. Astro rebuild
3. Update services page in Astro to reflect three-service structure
4. Cutover to production (enable Pages, swap custom domain, archive old repo)
