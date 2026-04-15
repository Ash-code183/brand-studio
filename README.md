# Brand Studio — Claude Code Skill

Turn any raw idea into a complete brand — or audit an existing one and fix what's broken. Name, domain, visual identity, AI illustrations, landing page, brand guidelines — all production-ready, deployed, and pushed to GitHub.

**Two modes:**
- **Create Mode** — 7 agents build a brand from scratch end-to-end
- **Audit Mode** — 5 agents scrape, score, diagnose, and fix an existing brand

---

## What it does

```
CREATE:  Idea → Discovery → Names → Identity → Illustrations → Copy → Landing Page → Deploy → GitHub
AUDIT:   URL → Scrape → Score (10 dimensions) → Diagnose → Fix Plan → Implement → Before/After
```

**You end up with:**
- A shortlisted brand name with domain availability checked
- A complete visual identity (palette, fonts, voice, tagline, illustration direction, motion rules)
- 5+ AI-generated illustrations (hero, features, how-it-works, CTA, OG image)
- A production-ready landing page (anti-slop design system, not generic AI templates)
- A 9-page printable brand guidelines document
- Discovery interview transcript preserving the founder's exact words
- A private GitHub repo with standardized `site/` + `docs/` structure
- Live Netlify deployment

---

## Agent Roster

### Create Mode

| # | Agent | Role | Output |
|---|-------|------|--------|
| 1 | **Strategist** | 8-question discovery interview | ICP brief, `docs/discovery-interview.md` |
| 2 | **Namer** | 20 name candidates, auto-screened, domain checked | Shortlist + recommendation |
| 3 | **Designer** | Visual identity + illustration direction + motion rules | Palette, fonts, voice, illustration style, animation system |
| 3.5 | **Illustrator** | AI illustration generation via pollinations.ai | 5+ images in `site/images/` |
| 4 | **Copywriter** | Landing page copy | Hero, features, CTA, testimonials, FAQ |
| 5 | **Builder** | HTML landing page + brand guidelines | `site/index.html`, `site/brand-guidelines.html` |
| 6 | **Publisher** | Structured repo + Netlify deploy + GitHub push | Live URL + repo URL |

### Audit Mode

| # | Agent | Role | Output |
|---|-------|------|--------|
| A1 | **Scanner** | Scrape site via firecrawl | Current identity snapshot |
| A2 | **Scorer** | Rate 10 dimensions 0-10 | Scorecard with letter grade (A-F) |
| A3 | **Diagnostician** | Identify issues with evidence | Prioritized issue list |
| A4 | **Prescriber** | Map fixes to create-mode agents | Improvement plan |
| A5 | **Surgeon** | Implement fixes, deploy, compare | Before/after scorecard, `docs/brand-audit.md` |

---

## Component & Template Sources

### 21st.dev — Component Registry

The largest marketplace of shadcn/ui-based React + Tailwind components (1.4M+ developers). Used for:
- **Static HTML builds:** Reference 21st.dev components as design patterns and code inspiration
- **React/Next.js builds:** Install directly via `npx shadcn@latest add "https://21st.dev/r/[slug]"`

Key component categories: hero sections, pricing tables, testimonial layouts, FAQ accordions, CTA blocks, navigation bars, feature grids.

Browse at: https://21st.dev

### Framer Motion (Motion) — Animation Library

The most popular React animation library (30.7K stars, 3.6M weekly downloads). Renamed from `framer-motion` to `motion` in 2025.

**For static HTML:** Motion patterns are translated to CSS equivalents:
- `whileInView` → IntersectionObserver + CSS class toggle
- Spring physics → `cubic-bezier(0.34, 1.56, 0.64, 1)`
- Stagger → `animation-delay` increments

**For React builds:** Install via `npm install motion`, import from `motion/react`

6 ready-to-use patterns included: staggered reveal, scroll-triggered sections, spring hover cards, number counters, parallax scroll, character-by-character text animation.

---

## Standardized Repo Structure

Every brand produced by Brand Studio follows this exact structure:

```
[brand]-brand/
├── site/                              # Deployable (Netlify publish dir)
│   ├── index.html                     # Landing page
│   ├── brand-guidelines.html          # 9-page printable brand book
│   └── images/                        # AI-generated illustrations
├── docs/                              # Brand documents
│   ├── discovery-interview.md         # Founder Q&A (REQUIRED)
│   ├── branding-context.md            # Full brief, identity, copy, research
│   └── brand-audit.md                 # Audit report (if audit mode)
├── netlify.toml                       # Deploy config (publish = "site")
└── README.md                          # Identity quick reference
```

---

## Anti-Slop Design System

Every landing page is built against an explicit anti-generic checklist:

**Banned:** Inter/Roboto/Arial fonts, purple gradients on white, equal-height card grids, centered-everything layouts, emoji icons, "powerful/seamless/comprehensive/robust" copy, scattered micro-animations, solid backgrounds without texture

**Required:** Distinctive font pairing, dominant color + sharp accent, asymmetric layouts, one orchestrated reveal system (staggered fade-in-up), GPU-only animations (transform + opacity), grain texture overlay, gradient nav border on scroll

Quality gate: "If someone sees it and immediately says 'AI generated' — it's slop."

---

## Usage

```bash
# Install
git clone https://github.com/Ash-code183/brand-studio.git ~/.claude/skills/brand-studio

# Create a brand from scratch
/brand-studio

# Audit an existing brand
/brand-studio audit https://example.com
```

---

## Brands Built with Brand Studio

| Brand | Repo | Live Site |
|-------|------|-----------|
| **annotate.fun** | [annotate-fun-brand](https://github.com/Ash-code183/annotate-fun-brand) | [annotate-fun.netlify.app](https://annotate-fun.netlify.app) |
| **haire.world** | [haire-world-brand](https://github.com/Ash-code183/haire-world-brand) | [haire-world.netlify.app](https://haire-world.netlify.app) |
| **HealBuddy** | [healbuddy-brand](https://github.com/Ash-code183/healbuddy-brand) | [healbuddy.org](https://healbuddy.org) |
| **0to1.space** | [0to1-space](https://github.com/Ash-code183/0to1-space) | [0to1.space](https://0to1.space) |

**Web app:** [brande.live](https://brande-live.vercel.app) — Brand audit & creation as a service (Next.js + Z.ai GLM-5.1)

---

## Built with

- [Claude Code](https://claude.ai/code) — Agent runtime
- [21st.dev](https://21st.dev) — Component registry for agent templates
- [Motion](https://motion.dev) — Animation library (formerly Framer Motion)
- [Pollinations.ai](https://pollinations.ai) — AI illustration generation
- [Firecrawl](https://firecrawl.dev) — Web scraping for audit mode
- [Fontshare](https://www.fontshare.com/) — Display fonts
- [Google Fonts](https://fonts.google.com/) — Body and mono fonts
- [Netlify](https://netlify.com/) — Deployment
- [Vercel](https://vercel.com/) — brande.live hosting

---

## License

MIT
