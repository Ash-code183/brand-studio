# Brand Studio — Claude Code Skill

Turn any raw idea into a complete brand in one session: name, domain, visual identity, landing page, and brand guidelines — all production-ready.

A team of 6 specialist agents working in sequence inside Claude Code, each handing off to the next.

---

## What it does

```
Idea → Discovery interview → Brand names + domains → Visual identity system
     → Landing page copy → Landing page HTML + Brand guidelines HTML + PDF → GitHub repo
```

**You end up with:**
- A shortlisted brand name with domain availability checked
- A complete visual identity (palette, fonts, voice, tagline)
- A production-ready landing page (no frameworks, no emoji icons, no generic AI templates)
- A 9-page printable brand guidelines document
- A PDF export of the brand guidelines (auto-generated via puppeteer)
- A private GitHub repo with everything + Netlify deploy config

---

## Agent Roster

| # | Agent | Role | Output |
|---|-------|------|--------|
| 1 | **Strategist** | 8-question discovery interview | ICP brief, positioning doc |
| 2 | **Namer** | 20 name candidates across 5 strategies, auto-screened and scored | Shortlist + domain availability + recommendation |
| 3 | **Designer** | Visual identity system | Palette (hex), fonts, voice, tagline |
| 4 | **Copywriter** | Landing page copy | Hero, context strip, truth points, testimonials, FAQ |
| 5 | **Builder** | HTML files + PDF | `landing.html`, `brand-guidelines.html`, `brand-guidelines.pdf` |
| 6 | **Publisher** | GitHub repo | Private repo with README + Netlify config |

---

## Usage

This is a [Claude Code](https://claude.ai/code) skill. Install it and run `/brand-studio` in any Claude Code session.

### Install

```bash
# Clone into your Claude skills directory
git clone https://github.com/Ash-code183/brand-studio.git ~/.claude/skills/brand-studio
```

Then add to your Claude Code user settings (`~/.claude/settings.json`):

```json
{
  "skills": [
    {
      "name": "brand-studio",
      "path": "~/.claude/skills/brand-studio/SKILL.md"
    }
  ]
}
```

### Run

Open Claude Code and type:

```
/brand-studio
```

That's it. The Strategist starts the interview immediately.

---

## What the landing page actually looks like

No emoji icons. No radial gradient blobs. No 3-column card grids.

The Builder uses a specific editorial layout:
- **Hero**: two-column with a real product moment card (daily summary, message thread, or dashboard mini-card) built from brand colors — not a placeholder
- **Context strip**: dark background, 3 data points at large scale
- **Truth points**: 4 numbered points in a 2×2 grid, typographic numbers, no icons
- **How it works**: full-bleed brand primary color section
- **Testimonials**: 1 featured card (60%) + 2 supporting (20% each), grid flush
- **CTA**: dark rounded block, text + buttons side by side

---

## What the Namer actually does

Not just 20 names in a table. Before presenting anything:

1. Reads the brand brief (ambition scope, tone, customer, category)
2. Generates names across 5 strategies: Compound, Coined, Metaphor/Feeling, Short Punchy Noun, Unexpected Angle
3. Auto-screens against hard rules (no -ify/-hub/-pal, no generic CareHub/HealthPal composites, no 4+ syllables)
4. Scores survivors on 5 dimensions: Recall, Spell, Say, Own, Fit
5. Presents with one-line rationale per name (not just the name)
6. Gives you a top 3 recommendation before domain check
7. Checks TLDs appropriate to the product: `.com`, `.io`, `.co`, `.ai`, `.care`, `.health`, `.in`

---

## Prerequisites

- **Claude Code** — [claude.ai/code](https://claude.ai/code)
- **GitHub CLI** (`gh`) — for repo creation in Agent 6
- **Node.js** — for PDF generation (puppeteer auto-installed on first run)
- **namecheap.sh** *(optional)* — for domain availability checking and registration. Without it, domain check is skipped but everything else works.

---

## Output files

All outputs land in `~/Desktop/brand-studio-output/`:

```
~/Desktop/brand-studio-output/
├── [brand-name]-landing.html           — production landing page
├── [brand-name]-brand-guidelines.html  — printable brand book
└── [brand-name]-brand-guidelines.pdf   — PDF export (auto-generated)
```

The GitHub repo (Agent 6) also includes:
- `brand-brief.md` — the ICP brief from the discovery interview
- `identity-system.md` — palette, fonts, voice, logo spec
- `netlify.toml` — deployment config for one-click Netlify deploy

---

## Built with

- [Claude Code](https://claude.ai/code) — the agent runtime
- [Fontshare](https://www.fontshare.com/) — for display fonts (Cabinet Grotesk, Satoshi, etc.)
- [Google Fonts](https://fonts.google.com/) — for body and mono fonts
- [Puppeteer](https://pptr.dev/) — for PDF generation
- [Netlify](https://netlify.com/) — for deployment

---

## Example output

HealBuddy — an AI elder companion service for Indian families:

- Landing page: [healbuddy-landing.netlify.app](https://healbuddy-landing.netlify.app)
- Identity: Forest green `#2D6A4F` + amber `#E07B39`, Cabinet Grotesk display, Plus Jakarta Sans body

---

## License

MIT
