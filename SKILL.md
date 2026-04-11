# Brand Studio — Full-Stack Brand Creation Agent

Turn any raw idea into a complete brand: name, domain, identity, landing page, and brand guidelines — all pushed to GitHub.

A team of 6 specialist agents working in sequence, each handing off to the next.

---

## Agent Roster

| # | Agent | Role | Output |
|---|-------|------|--------|
| 1 | Strategist | Deep discovery interview | ICP brief, positioning doc |
| 2 | Namer | Brand name generation + domain check | Shortlisted names + available domains |
| 3 | Designer | Visual identity system | Palette, fonts, personality, voice |
| 4 | Copywriter | Landing page copy | Hero, features, CTA, social proof |
| 5 | Builder | HTML landing page + brand guidelines | landing.html, brand-guidelines.html |
| 6 | Publisher | GitHub repo creation + push | Private GitHub repo URL |

---

## Step 0: Environment Setup

```bash
# Find namecheap CLI
NC_CLI="$HOME/Desktop/namecheap.sh"
[ ! -f "$NC_CLI" ] && NC_CLI=$(find "$HOME" -name "namecheap.sh" -maxdepth 4 2>/dev/null | head -1)
[ -f "$NC_CLI" ] && chmod +x "$NC_CLI" && echo "NAMECHEAP_READY: $NC_CLI" || echo "NAMECHEAP_NOT_FOUND: domain checking will be skipped"

# Output dir
BRAND_DIR="$HOME/Desktop/brand-studio-output"
mkdir -p "$BRAND_DIR"
echo "OUTPUT_DIR: $BRAND_DIR"

# Check gh CLI
gh auth status 2>/dev/null && echo "GITHUB_READY" || echo "GITHUB_NOT_CONFIGURED: will skip push"
```

Store: `NC_CLI`, `BRAND_DIR`, `GITHUB_READY`

---

## Agent 1: Strategist — Discovery Interview

The Strategist conducts a focused 8-question interview, one question at a time, to build the brand brief. The goal is to understand the idea, the customer, and the emotional job-to-be-done deeply enough to brief all downstream agents.

### Discovery Questions (ask one at a time)

**Q1 — The Idea**
> "In one sentence, what does your product or service DO for the person using it? (Not what it is — what it does.)"

**Q2 — The Problem**
> "What's the pain, frustration, or inefficiency your customer has RIGHT NOW — before they find you? Be specific. What does their day look like without you?"

**Q3 — The Customer**
> "Describe your ideal first customer. Not a demographic — a PERSON. What's their job title? What are they trying to accomplish? What keeps them up at night?"

**Q4 — The Market**
> "Who else is trying to solve this? Name 2-3 alternatives your customer uses today (even imperfect ones). Why do those fall short?"

**Q5 — The Wedge**
> "What's the ONE thing you do that nobody else does, or does as well? This is your unfair advantage."

**Q6 — The Outcome**
> "When your product works perfectly, what changes for your customer? What can they do or feel that they couldn't before?"

**Q7 — The Tone**
> "Pick 3 words that describe how you want your brand to feel. Then tell me one brand (any industry) you admire the LOOK AND FEEL of — and why."

**Q8 — The Ambition**
> "What's the 3-year vision? How big, how many customers, what market position?"

### After Q8: Synthesize the ICP Brief

Display the synthesized brief for user confirmation:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
BRAND BRIEF
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
WHAT IT DOES: [one sentence]
CUSTOMER: [vivid person description]
PAIN: [specific before-state]
ALTERNATIVES: [2-3 named competitors]
WEDGE: [unfair advantage]
OUTCOME: [transformation]
TONE WORDS: [3 words]
REFERENCE BRAND: [brand name + why]
AMBITION: [3-year vision]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Ask: "Does this capture it? Any corrections before I brief the naming team?"

Store the confirmed brief as `BRAND_BRIEF` for all downstream agents.

---

## Agent 2: Namer — Brand Name Generation + Domain Check

The Namer generates 20 brand name candidates across 5 naming strategies, then checks domain availability for the shortlist.

### Naming Strategies (4 names each)

**Strategy 1: Compound words**
Fuse two relevant words into one memorable unit.
*Example: Dropbox, Snapchat, Salesforce*

**Strategy 2: Invented / Coined words**
Meaningless word that becomes meaningful through use.
*Example: Google, Kodak, Xerox*

**Strategy 3: Metaphor names**
A word that evokes the feeling or transformation.
*Example: Amazon, Slack, Nest*

**Strategy 4: Founder-coded / Authority names**
Suggests expertise, origin, or category ownership.
*Example: McKinsey, Bloomberg, Shopify*

**Strategy 5: Short punchy nouns**
1-2 syllable words with energy and recall.
*Example: Stripe, Notion, Linear*

### Display Names as a Table

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
BRAND NAME CANDIDATES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

COMPOUND           COINED             METAPHOR
─────────────────  ─────────────────  ─────────────────
[Name 1]           [Name 5]           [Name 9]
[Name 2]           [Name 6]           [Name 10]
[Name 3]           [Name 7]           [Name 11]
[Name 4]           [Name 8]           [Name 12]

AUTHORITY          SHORT PUNCHY
─────────────────  ─────────────────
[Name 13]          [Name 17]
[Name 14]          [Name 18]
[Name 15]          [Name 19]
[Name 16]          [Name 20]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Ask: "Which 5-6 of these resonate most? I'll check domain availability for those."

### Domain Availability Check

For each shortlisted name, check 3 TLDs: `.com`, `.io`, `.co`

```bash
# For each shortlisted name:
bash "$NC_CLI" search "[name].com" 2>/dev/null
bash "$NC_CLI" search "[name].io" 2>/dev/null
bash "$NC_CLI" search "[name].co" 2>/dev/null
```

Display results:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DOMAIN AVAILABILITY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Name]    .com ✅ $X/yr   .io ✅ $X/yr   .co ❌
[Name]    .com ❌          .io ✅ $X/yr   .co ✅ $X/yr
[Name]    .com ✅ $X/yr   .io ❌          .co ❌
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Ask: "Which name + domain combination do you want? Want me to register it now?"

If yes, register:
```bash
bash "$NC_CLI" buy [domain]
```

Store: `CHOSEN_NAME`, `CHOSEN_DOMAIN`

---

## Agent 3: Designer — Visual Identity System

The Designer proposes a complete visual identity based on the brand brief and chosen name. No design software needed — outputs a structured identity system.

### Identity System Proposal

Based on `BRAND_BRIEF` (tone words, reference brand, product category), propose:

**Aesthetic Direction** (pick one that fits):
- Minimal / Precise — White space, one accent, geometric typography
- Bold / Energetic — High contrast, strong type, saturated accents
- Warm / Human — Earth tones, rounded forms, serif accents
- Dark / Premium — Dark backgrounds, neon accents, luxury feel
- Playful / Approachable — Bright palette, rounded type, friendly

**Colour Palette** (CSS hex values):
```
PRIMARY:     [hex] — [what it represents]
SECONDARY:   [hex] — [what it represents]
BACKGROUND:  [hex] — [light or dark base]
TEXT:        [hex] — [primary text colour]
TEXT_MUTED:  [hex] — [secondary text]
ACCENT:      [hex] — [CTA and highlight colour]
```

Rules for palette selection:
- Tone word "bold/energetic" → saturated primary, dark background
- Tone word "calm/trustworthy" → muted blues/greens, light background
- Tone word "premium/luxurious" → near-black + gold or deep purple
- B2B / enterprise → restrained palette, no more than 2 accent colours
- Consumer / lifestyle → can use 3+ complementary accents

**Typography Stack** (Google Fonts only for zero-dependency):
```
DISPLAY:  [font name] — [weight] — [character: commanding/playful/etc]
BODY:     [font name] — [weights: 400, 500, 700]
MONO:     [font name] — [for labels, tags, data]
```

Never recommend: Inter, Roboto, Arial, Helvetica, Open Sans, Montserrat (unless explicitly requested).

**Brand Voice** (3 pairs of adjectives):
```
[Adjective 1] not [Opposite]   e.g. "Direct, not blunt"
[Adjective 2] not [Opposite]   e.g. "Confident, not arrogant"
[Adjective 3] not [Opposite]   e.g. "Simple, not simplistic"
```

**Logo Concept** (text-based, no image needed):
Describe how the wordmark should look:
- Typography choice
- Capitalisation style (ALL CAPS / Title Case / lowercase)
- Any colour split (e.g., first word in accent, rest in primary)
- Letter-spacing guidance

**Tagline** (3 options):
Generate 3 taglines based on the brand brief:
1. Action-oriented: starts with a verb, customer-outcome focused
2. Declarative: bold claim about what you are
3. Question-based: provokes curiosity

Display the full identity system and ask: "Which tagline fits best? Any adjustments to the palette or fonts before I brief the copywriter?"

Store: `IDENTITY_SYSTEM` (all hex values, font names, voice pairs, chosen tagline)

---

## Agent 4: Copywriter — Landing Page Copy

The Copywriter writes all landing page copy using the brand brief and identity system as input. Every word is purposeful. No filler.

### Copy Architecture

**Hero Section**
- Headline (max 8 words): The transformation or outcome. No "we help you" constructions.
- Subheadline (max 20 words): Who it's for and the specific pain solved.
- Primary CTA (max 4 words): Action-oriented. What happens when they click.
- Secondary CTA (max 4 words): Lower commitment option.

**Social Proof Bar**
3-5 short trust signals (logos / numbers / names). Even for new brands, use placeholder structure:
"Trusted by [type of customer] at [company type]" or milestone numbers.

**3 Core Benefits** (the "why you" section)
For each benefit:
- Icon label (2 words max, use emoji as placeholder icon)
- Benefit headline (max 6 words)
- Benefit description (max 25 words, outcome-focused)

**How It Works** (3 steps max)
- Step number
- Step headline (max 5 words)
- Step description (max 20 words)

**Proof Section**
1 featured testimonial (can be hypothetical/placeholder for MVP):
- Quote (max 40 words, specific and outcome-focused, no generic praise)
- Name, Title, Company

**FAQ** (4 questions)
Answer the most common objections and concerns based on the brand brief:
1. The "how does it work" question
2. The pricing/cost question
3. The "is this for me" question
4. The trust/credibility question

**Final CTA Section**
- Section headline (max 8 words, urgency or desire)
- Supporting copy (max 20 words)
- CTA button (same as hero primary)

Display all copy sections and ask: "Any edits before I build the landing page?"

Store: `LANDING_COPY`

---

## Agent 5: Builder — HTML Landing Page + Brand Guidelines

The Builder generates two complete, production-ready HTML files using the identity system and landing copy.

### File 1: landing.html

Self-contained HTML file with:
- Google Fonts `<link>` for the chosen font stack
- CSS custom properties from the identity system
- Mobile-responsive layout (flexbox/grid, no framework)
- All copy sections from Agent 4
- Smooth scroll, hover states, subtle animations
- `<meta>` OG tags for social sharing
- Print styles

**Sections:**
1. Nav (logo + CTA button)
2. Hero (headline + subheadline + CTAs + hero visual placeholder)
3. Social proof bar
4. Benefits (3-column grid)
5. How it works (numbered steps)
6. Testimonial (blockquote card)
7. FAQ (accordion with CSS-only toggle)
8. Final CTA section
9. Footer (logo + tagline + links placeholder)

Quality bar: Should look like it was designed by a professional studio, not a template. Use the brand palette throughout. Typography hierarchy should be clear. Whitespace should breathe.

### File 2: brand-guidelines.html

Printable brand book (A4-ready) with `@media print` styles:

Pages:
1. Cover (brand name, tagline, "Brand Guidelines v1.0")
2. Who We Are (30-word brand positioning statement)
3. Mission & Vision (from brand brief)
4. Brand Personality (voice pairs, tone rules)
5. Colour System (swatches with hex values + usage rules)
6. Typography (specimens of all 3 fonts in all weights)
7. Logo & Wordmark (render rules, clear space, don'ts)
8. Applications (example social card, email header, OG image)
9. Quick Reference (1-page summary card)

### Save Both Files

```bash
# Save to output directory
cp /tmp/landing.html "$BRAND_DIR/[CHOSEN_NAME]-landing.html"
cp /tmp/brand-guidelines.html "$BRAND_DIR/[CHOSEN_NAME]-brand-guidelines.html"
echo "FILES SAVED:"
ls -lh "$BRAND_DIR/"
```

Tell user: "Both files saved. Open them to review before I push to GitHub?"

```bash
open "$BRAND_DIR/[CHOSEN_NAME]-landing.html"
open "$BRAND_DIR/[CHOSEN_NAME]-brand-guidelines.html"
```

---

## Agent 6: Publisher — GitHub Repo

The Publisher creates a private GitHub repo, writes a README, and pushes all brand assets.

### Repo Contents

```
[chosen-name]-brand/
├── README.md              — project overview + brand summary
├── landing.html           — production landing page
├── brand-guidelines.html  — printable brand book
├── brand-brief.md         — the ICP brief from Agent 1
├── identity-system.md     — colours, fonts, voice, logo spec
└── netlify.toml           — deployment config (HTTP→HTTPS + security headers)
```

### README Template

```markdown
# [Brand Name]

[Tagline]

## What It Is
[30-word positioning statement from brand brief]

## Brand Assets
- `landing.html` — Open in browser for the landing page
- `brand-guidelines.html` — Open in browser / print as PDF for brand book

## Deploy to Netlify
[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy)

1. Push this repo to GitHub
2. Connect to Netlify
3. Deploy — no build step needed (pure HTML)

## Domain
[CHOSEN_DOMAIN] — [registered/not yet registered]
```

### netlify.toml Template

```toml
[[redirects]]
  from = "http://[CHOSEN_DOMAIN]/*"
  to = "https://[CHOSEN_DOMAIN]/:splat"
  status = 301
  force = true

[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
    X-XSS-Protection = "1; mode=block"
    X-Content-Type-Options = "nosniff"
    Referrer-Policy = "no-referrer-when-downgrade"
```

### Push to GitHub

```bash
REPO_NAME="[chosen-name]-brand"
cd "$BRAND_DIR"
git init
git add .
git commit -m "Initial commit — [Brand Name] brand assets

- Landing page (landing.html)
- Brand guidelines (brand-guidelines.html)
- Brand brief and identity system docs
- Netlify deployment config

Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>"
gh repo create "$REPO_NAME" --private --source=. --remote=origin --push
echo "REPO_URL: https://github.com/$(gh api user --jq .login)/$REPO_NAME"
```

### Final Output

Display the complete delivery summary:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
BRAND STUDIO — DELIVERY COMPLETE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

BRAND NAME:      [Chosen Name]
TAGLINE:         [Chosen Tagline]
DOMAIN:          [domain] ([registered ✅ / available 🟡 / not registered ⚠️])

ASSETS:
  Landing page   → $BRAND_DIR/[name]-landing.html
  Brand book     → $BRAND_DIR/[name]-brand-guidelines.html
  Brand brief    → $BRAND_DIR/brand-brief.md
  Identity doc   → $BRAND_DIR/identity-system.md

GITHUB REPO:     https://github.com/[user]/[name]-brand (private)

NEXT STEPS:
  1. Review landing.html — adjust copy as needed
  2. Connect repo to Netlify for one-click deploy
  3. Point [domain] to Netlify (run: bash ~/Desktop/namecheap.sh point [domain] netlify)
  4. Set up Netlify Forms to capture leads

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Usage

```bash
# Run the full brand studio (interactive)
claude code # then type: /brand-studio

# Or invoke directly
# The skill starts at Agent 1 and walks through all 6 agents
```

## Notes

- Each agent can be re-run independently if you want to iterate (e.g., "generate new names")
- The `namecheap.sh` CLI handles domain checking and registration
- All outputs land in `~/Desktop/brand-studio-output/[brand-name]/`
- The GitHub repo is always private — you control when/if it goes public
- Landing page and brand book are pure HTML — no build step, works with Netlify, Vercel, GitHub Pages
