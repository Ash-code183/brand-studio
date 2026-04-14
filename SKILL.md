# Brand Studio — Full-Stack Brand Creation Agent

Turn any raw idea into a complete brand: name, domain, identity, landing page, and brand guidelines — all pushed to GitHub.

A team of 6 specialist agents working in sequence, each handing off to the next.

---

## Agent Roster

| # | Agent | Role | Output |
|---|-------|------|--------|
| 1 | Strategist | Deep discovery interview | ICP brief, positioning doc, `docs/discovery-interview.md` |
| 2 | Namer | Brand name generation + domain check | Shortlisted names + available domains |
| 3 | Designer | Visual identity + illustration direction | Palette, fonts, voice, illustration style, motion rules |
| 3.5 | Illustrator | AI illustration generation | Hero, section backgrounds, OG image in `site/images/` |
| 4 | Copywriter | Landing page copy | Hero, features, CTA, social proof |
| 5 | Builder | HTML landing page + brand guidelines | `site/index.html`, `site/brand-guidelines.html` |
| 6 | Publisher | Structured repo + GitHub push + Netlify deploy | Private GitHub repo URL + live site URL |

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

### Save Discovery Interview

After the brief is confirmed, **immediately save** the full Q&A transcript as `docs/discovery-interview.md`. This is a permanent record of the founder's words — not a summary, but the actual questions asked and answers given. Use this template:

```markdown
# [Brand Name] — Brand Discovery Interview

## Q1 — The Idea
**In one sentence, what does your product or service DO for the person using it?**

> [Founder's actual answer]

## Q2 — The Problem
**What's the pain, frustration, or inefficiency your customer has RIGHT NOW?**

> [Founder's actual answer]

## Q3 — The Customer
**Describe your ideal first customer.**

> [Founder's actual answer]

## Q4 — The Market
**Who else is trying to solve this?**

> [Founder's actual answer]

## Q5 — The Wedge
**What's the ONE thing you do that nobody else does?**

> [Founder's actual answer]

## Q6 — The Outcome
**When your product works perfectly, what changes for your customer?**

> [Founder's actual answer]

## Q7 — The Tone
**Pick 3 words that describe how you want your brand to feel. One brand you admire?**

> [Founder's actual answer]

## Q8 — The Ambition
**What's the 3-year vision?**

> [Founder's actual answer]

---

## Confirmed Brand Brief

- **WHAT IT DOES:** [one sentence]
- **CUSTOMER:** [vivid person description]
- **PAIN:** [specific before-state]
- **ALTERNATIVES:** [2-3 named competitors]
- **WEDGE:** [unfair advantage]
- **OUTCOME:** [transformation]
- **TONE:** [3 words]
- **REFERENCE:** [brand name]
- **AMBITION:** [3-year vision]

## Chosen Tagline
**"[tagline]"**

## Chosen Identity
- Aesthetic: [direction]
- Palette: [hex values]
- Fonts: [font names]
- Voice: [voice pairs]
- Logo: [description]
```

This file is updated as decisions are made through Agents 2–4 (tagline, identity, etc.) and saved to `$BRAND_DIR/docs/discovery-interview.md`.

---

## Agent 2: Namer — Brand Name Generation + Domain Check

The Namer generates 20 brand name candidates across 5 naming strategies, self-screens them against hard quality rules, then presents the survivors with rationale before checking domain availability.

### Pre-generation brief review

Before generating names, extract from `BRAND_BRIEF`:
- **Ambition scope**: local/regional vs. national vs. global
- **Tone words**: these constrain which strategies to lean into
- **Customer**: who will say this name out loud?
- **Category**: what sounds already own this space?

If ambition is global, avoid names that feel geographically coded to one country or language.

### Naming Strategies (4 names each)

**Strategy 1: Compound words**
Fuse two relevant words into one memorable unit. Draw from the emotional territory of the brief — transformation, care, presence, connection — not generic category words.
*Example: Dropbox, Snapchat, Salesforce — not "CareHub", "HealthPal", "ElderCare"*

**Strategy 2: Invented / Coined words**
A meaningless word that becomes meaningful through use. Should be phonetically clean: easy to say in Hindi, English, and globally. Avoid words that sound like something embarrassing in another language.
*Example: Google, Kodak, Xerox, Zomato*

**Strategy 3: Metaphor / Feeling names**
A word that evokes the emotional transformation, not the category mechanics.
*Example: Amazon (vast), Slack (relief), Nest (home), Kin (belonging)*

**Strategy 4: Short punchy nouns**
1-2 syllable words with energy and recall. The test: can you say it in a noisy room and have someone spell it correctly first try?
*Example: Stripe, Notion, Linear, Calm*

**Strategy 5: Unexpected angles**
Names that break from category conventions entirely — take a word from a completely unrelated field that captures the emotional truth.
*Example: Apple (computers), Robin (personal finance), Anchor (podcasting)*

### Name Scoring — auto-screen before presenting

Before presenting any name, score it against 5 dimensions (1-5 each). Reject any name scoring below 3 on Recall or Own. Target total score ≥ 16/25.

| Dimension | 1 | 3 | 5 |
|-----------|---|---|---|
| **Recall** | Hard to remember | Sticks after 2-3 times | Instant recall, one hearing |
| **Spell** | People will guess wrong | Common misspellings exist | Sounds exactly like it reads |
| **Say** | Awkward in any target language | Minor tongue trip | Natural in all target languages |
| **Own** | Taken or generic category word | Similar names exist | Clean, distinctive, ownable |
| **Fit** | Feels off for this product | Loose connection | Resonates with the brief's core tension |

**Hard rejection rules** (auto-remove before presenting):
- Ends in `-ify`, `-ly`, `-hub`, `-pal`, `-app`, `-now`, `-go`, `-360` → generic tech/SaaS suffix
- Contains generic care/health words: *Care, Health, Heal, Elder, Senior, Assist* as the entire name or dominant component (metaphors that happen to use these words are OK if the full name is distinctive)
- 4+ syllables → too long for conversational use
- Sounds like an existing large brand within 1 edit distance
- Culturally awkward in Hindi, Tamil, or English (check your knowledge)

### Display Names with Rationale

After self-screening, present surviving names in a single table. Show one-line rationale per name — not just the name in isolation. The rationale should connect back to the brand brief.

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
BRAND NAME CANDIDATES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

COMPOUND (fusing two meaningful territories)
  [Name 1]    — [one-line rationale connecting to the brief]
  [Name 2]    — [one-line rationale]
  [Name 3]    — [one-line rationale]
  [Name 4]    — [one-line rationale]

INVENTED / COINED (meaningless but phonetically clean)
  [Name 5]    — [one-line rationale]
  [Name 6]    — [one-line rationale]
  [Name 7]    — [one-line rationale]
  [Name 8]    — [one-line rationale]

METAPHOR / FEELING (emotional resonance over category description)
  [Name 9]    — [one-line rationale]
  [Name 10]   — [one-line rationale]
  [Name 11]   — [one-line rationale]
  [Name 12]   — [one-line rationale]

SHORT PUNCHY NOUN (says it in one syllable)
  [Name 13]   — [one-line rationale]
  [Name 14]   — [one-line rationale]
  [Name 15]   — [one-line rationale]
  [Name 16]   — [one-line rationale]

UNEXPECTED ANGLE (breaks category convention)
  [Name 17]   — [one-line rationale]
  [Name 18]   — [one-line rationale]
  [Name 19]   — [one-line rationale]
  [Name 20]   — [one-line rationale]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Then add your **top 3 recommendation** with brief reasoning — which names you think work best and why, based on the brief.

Ask: "Which 4-5 of these do you want to take to domain check?"

### Domain Availability Check

For each shortlisted name, check TLDs based on the product's ambition:

- **Global ambition**: check `.com`, `.io`, `.co`, `.ai` (if AI product), `.app`
- **India-first**: additionally check `.in`, `.co.in`
- **Healthcare/care/companion product**: additionally check `.care`, `.health`

```bash
# For each shortlisted name (run relevant TLDs only):
bash "$NC_CLI" search "[name].com" 2>/dev/null
bash "$NC_CLI" search "[name].io" 2>/dev/null
bash "$NC_CLI" search "[name].co" 2>/dev/null
bash "$NC_CLI" search "[name].ai" 2>/dev/null    # if AI product
bash "$NC_CLI" search "[name].care" 2>/dev/null  # if care/health product
bash "$NC_CLI" search "[name].in" 2>/dev/null    # if India-first
```

Display results with pricing:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DOMAIN AVAILABILITY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Name]    .com ✅ $12/yr   .io ✅ $35/yr   .co ❌   .care ✅ $18/yr
[Name]    .com ❌           .io ✅ $35/yr   .co ✅ $25/yr
[Name]    .com ✅ $12/yr   .io ❌           .care ✅ $18/yr
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Recommend a specific combination: "I'd go with [Name] + [TLD] because [reason tied to brief]."

Ask: "Want to go with this, or register a different combination?"

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

**Illustration Style Direction** (REQUIRED — feeds into Agent 3.5):
Define the illustration world for the brand. This is NOT optional — every brand gets custom illustrations, not stock or template graphics.

Choose ONE primary style based on the brand brief's tone words and reference brand:
- **Anime / Cyberpunk** — Neon-lit scenes, anime characters, Makoto Shinkai vibes. For: tech, gaming, Gen-Z, crypto.
- **Warm Painterly** — Soft gradients, golden hour light, human warmth. For: care, health, family, community.
- **Bold Flat** — Geometric shapes, saturated colors, Memphis-inspired. For: SaaS, productivity, B2B.
- **Editorial Illustration** — Sophisticated, magazine-quality art, full-bleed compositions. For: premium, luxury, content.
- **3D / Isometric** — Floating objects, depth layers, glossy materials. For: fintech, enterprise, developer tools.
- **Hand-drawn / Organic** — Textured, imperfect, human-feeling linework. For: food, local, artisanal, education.

For the chosen style, specify:
```
ILLUSTRATION_STYLE: [chosen style]
SCENE_DESCRIPTIONS:
  hero: [describe the hero scene — characters, setting, mood, key elements]
  features: [describe the features background — what environment/objects/metaphors]
  how_it_works: [describe the process illustration — visual metaphor for the workflow]
  cta: [describe the closing scene — emotional resonance, aspiration]
  og_image: [describe the social sharing preview — brand-representative close-up]
COLOR_MOOD: [dominant colors for illustration palette, pulled from brand palette]
CHARACTERS: [describe any recurring character types — age, style, accessories, energy]
KEY_OBJECTS: [signature objects that appear across illustrations — e.g., glowing glasses, floating labels, golden coins]
```

**Motion & Animation Guidelines:**
Define how the brand moves (CSS animations for the landing page):
```
ANIMATION_SPEED: [fast/medium/slow — based on brand energy]
HOVER_STYLE: [what happens on hover — lift, glow, color shift, scale]
SCROLL_BEHAVIOR: [parallax, fade-in, slide-up, none]
TRANSITION_EASING: [ease-out for playful, ease-in-out for premium, linear for minimal]
SIGNATURE_MOTION: [one branded animation — e.g., "sunset gradient pulse", "floating labels", "neon flicker"]
```

**Tagline** (3 options):
Generate 3 taglines based on the brand brief:
1. Action-oriented: starts with a verb, customer-outcome focused
2. Declarative: bold claim about what you are
3. Question-based: provokes curiosity

Display the full identity system and ask: "Which tagline fits best? Any adjustments to the palette, illustration style, or fonts before I brief the illustrator?"

Store: `IDENTITY_SYSTEM` (all hex values, font names, voice pairs, illustration direction, motion rules, chosen tagline)

---

## Agent 3.5: Illustrator — AI Illustration Generation

The Illustrator generates custom brand illustrations using AI image generation. Every brand gets unique, non-generic visuals — no stock photos, no template graphics.

### Why This Agent Exists

Generic landing pages use geometric SVG shapes, gradient blobs, or stock photos. These are instantly recognizable as AI-generated templates. Custom illustrations — generated from the brand's identity system and scene descriptions — create emotional resonance and visual distinctiveness that templates cannot achieve.

### Image Generation Method

Use **pollinations.ai** (free, no API key) to generate images via URL:

```
https://image.pollinations.ai/prompt/{URL_ENCODED_PROMPT}?width={W}&height={H}&nologo=true&seed={N}&enhance=true
```

Download each image with curl:
```bash
mkdir -p "$REPO_DIR/site/images"
curl -s -o "$REPO_DIR/site/images/{filename}.jpg" "{URL}"
```

**Verify each image** — check `file` command output is JPEG/PNG, not JSON (rate limit error). If rate-limited, retry after a few seconds. Images under 1KB are usually errors.

### Required Illustrations (5 minimum)

Generate these based on `IDENTITY_SYSTEM.SCENE_DESCRIPTIONS` from Agent 3:

| Image | Dimensions | Filename | Purpose |
|-------|-----------|----------|---------|
| **Hero background** | 1440x810 | `hero-bg.jpg` | Full-bleed hero section background |
| **Features background** | 1440x600 | `features-bg.jpg` | Atmospheric behind feature cards (used at low opacity) |
| **How-it-works** | 1440x500 | `how-bg.jpg` | Section background for process/steps |
| **CTA background** | 1200x400 | `cta-bg.jpg` | Final call-to-action section |
| **OG preview image** | 1200x630 | `og-image.jpg` | Social sharing preview when URL is shared |

### Prompt Engineering for Brand Illustrations

Build prompts from the Designer's `ILLUSTRATION_STYLE` and `SCENE_DESCRIPTIONS`. Always include:

1. **Style prefix** — e.g., "anime illustration", "warm painterly", "bold flat design", "editorial illustration"
2. **Scene description** — from SCENE_DESCRIPTIONS (characters, setting, objects, mood)
3. **Color guidance** — "neon purple blue orange" or "warm earth tones green amber" from palette
4. **Quality suffix** — "detailed", "sharp", "cinematic", "wide composition"
5. **Brand-specific elements** — recurring characters, signature objects (from KEY_OBJECTS)

**Anti-patterns:**
- Never use "stock photo", "generic", "corporate"
- Never request text in images (AI text generation is unreliable)
- Always include character descriptions if the brand has personas
- Include environmental details specific to the brand's ICP

### Example Prompts by Style

**Anime / Cyberpunk (like annotate.fun):**
```
anime illustration shinjuku tokyo night street two anime characters girl with
glowing orange smart glasses holding camera boy with golden glasses holding
smartphone UFO hovering above neon purple blue orange cyberpunk Makoto Shinkai
detailed sharp cinematic wide
```

**Warm Painterly (like HealBuddy):**
```
warm painterly illustration elderly person and young companion sharing tea on
a sunlit verandah golden hour light soft green garden background warm amber
and forest green tones emotional genuine connection detailed illustration
```

**Bold Flat (SaaS product):**
```
bold flat design illustration floating dashboard screens data visualization
geometric shapes saturated blue and coral colors clean lines Memphis style
modern tech illustration wide composition
```

### Verification

After generating all images, **visually verify each one** using the Read tool:
```bash
file "$REPO_DIR/site/images/"*.jpg  # Confirm all are JPEG
ls -lh "$REPO_DIR/site/images/"     # Confirm reasonable file sizes (50KB-200KB)
```

Read each image file to visually confirm quality and brand alignment. If any image doesn't match the brand direction, regenerate with an adjusted prompt.

### Output

Display generated images to the user for approval:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ILLUSTRATIONS GENERATED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Style: [ILLUSTRATION_STYLE]

  hero-bg.jpg      — [brief description]
  features-bg.jpg  — [brief description]
  how-bg.jpg       — [brief description]
  cta-bg.jpg       — [brief description]
  og-image.jpg     — [brief description]

Saved to: $REPO_DIR/site/images/
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Ask: "Happy with the illustrations? I can regenerate any that don't feel right before building the page."

Store: `ILLUSTRATIONS_GENERATED = true`

---

## Agent 4: Copywriter — Landing Page Copy

The Copywriter writes all landing page copy using the brand brief and identity system as input. Every word is purposeful. No filler.

### Copy Architecture

**Hero Section**
- Headline (max 8 words): The transformation or outcome. No "we help you" constructions. Lead with the customer's changed life, not the product's features.
- Subheadline (max 20 words): Who it's for and the specific before-state being solved.
- Primary CTA (max 4 words): Action-oriented. What happens when they click.
- Secondary CTA (max 4 words): Lower commitment option.
- Hero Visual Moment: Describe a specific product moment that makes the value concrete — not a generic placeholder. A daily summary card, a message thread, an activity log, a before/after. One real use-case rendered as a UI element. This will be built as a styled HTML card by the Builder.

**Context Strip** (the "why this matters" section)
3 data points that give the problem scale and emotional weight. Use real statistics from the domain if available, or strong hypothetical proxies. Format: large number + one-line label.
- Data point 1: Size of problem or market
- Data point 2: Consequence or risk if unsolved
- Data point 3: What the solution replaces or removes

No emoji. No ✦ bullets. Just numbers that land.

**4 Core Truth Points** (the "what you actually get" section)
Do NOT use a 3-column grid with emoji icons. Use 4 numbered truth points in a 2-column asymmetric layout.

For each truth point:
- Number (01, 02, 03, 04) — typographic, not bulleted
- Headline (max 6 words): The specific outcome
- Description (max 30 words): The mechanism — how this actually works, not why it matters

Anti-patterns to avoid:
- No emoji as icons
- No "comprehensive", "seamless", "powerful", "robust"
- No generic benefit categories (Communication, Monitoring, Care, Peace of Mind) — go specific
- Each point should be something only THIS product can claim, not any product in the category

**How It Works** (3 steps max)
- Step number (typographic: 01, 02, 03)
- Step headline (max 5 words): Verb-first, action-oriented
- Step description (max 20 words): What happens at this step from the customer's perspective

**Proof Section** — 3 testimonials
One featured (longer, more specific) + two supporting (shorter, different customer type).

For the featured testimonial:
- Quote: 30-50 words, outcome-specific. Include a before-state and after-state. No generic praise ("game-changer", "love it", "amazing").
- Name, relationship to product context (e.g. "daughter of 74-year-old father in Mumbai"), optional location

For each supporting testimonial:
- Quote: 15-25 words, one specific claim
- Name + relationship

Write personas that represent real customer segments from the brief — not generic "happy user."

**FAQ** (4 questions)
Answer the most common objections from the brand brief's pain points:
1. The "how exactly does it work day-to-day" question
2. The "what does it cost and is it worth it" question
3. The "is this right for my specific situation" question
4. The "why should I trust you" question

Answers should be honest and direct — not marketing copy. If something is still being figured out, say "right now" to imply it's improving.

**Final CTA Section**
- Section headline (max 8 words): urgency or desire, not repetition of hero headline
- Supporting copy (max 20 words): addresses the last remaining hesitation
- Primary CTA button (same copy as hero primary)

Display all copy sections and ask: "Any edits before I build the landing page?"

Store: `LANDING_COPY`

---

## Agent 5: Builder — HTML Landing Page + Brand Guidelines

The Builder generates two complete, production-ready HTML files using the identity system and landing copy.

### File 1: landing.html

Self-contained HTML file. No frameworks. No emojis as icons. No radial gradient blobs. No 3-column card grids with hover lift animations. The quality bar is: does this look like a boutique studio made it, or like an AI tool output a template?

**Technical requirements:**
- `<link>` tags for the full font stack (Fontshare CDN for display fonts, Google Fonts for body/mono)
- CSS custom properties from the identity system — tokens for colors, fonts, spacing
- Mobile-responsive (flexbox/grid, tested at 375px and 1280px)
- Smooth scroll behavior
- `<meta>` OG tags for social sharing
- CSS-only FAQ accordion using `<input type="checkbox">` + `:checked ~ .faq-answer { display: block }`

**Design anti-patterns to avoid (hard rules):**
- No emoji icons (🎯 💡 ✅ 🚀 — none of these)
- No radial gradient blobs as decorative background elements
- No 3-column equal-height benefit card grids with icon circles at the top
- No ✦ or • as social proof bar separators
- No "powerful", "seamless", "comprehensive", "robust" in any visible text
- No generic stock-photo-style placeholder hero visuals (clipart laptop, smiling person)
- No centered-everything layouts with uniform padding

**Page structure — follow this specific architecture:**

**1. Nav**
- Left: wordmark (display font, brand primary)
- Right: one ghost link + one filled CTA button
- Fixed on scroll, subtle border appears on scroll (JS or CSS scroll-driven animation)
- No hamburger on desktop

**2. Hero**
- Two-column layout at desktop (left: copy / right: visual card)
- Headline: display font, large (clamp-based responsive size), max 2 lines
- Subheadline: body font, muted color, generous line-height
- Two CTAs: primary (filled, brand accent) + secondary (ghost or text link)
- Right column: a styled product moment card — NOT a placeholder image or generic illustration. Build this as a real HTML/CSS component using the brand colors. Options:
  - Daily summary card (if the product has recurring check-ins): show a date, time, 3-4 activity items with small colored indicators
  - Message thread preview (if the product has communication): show 2-3 messages in a chat UI
  - Dashboard mini-card (if the product tracks metrics): show 2-3 stat rows with labels
  Choose whichever fits the product from the brand brief. The card should use the identity system colors and feel like a real screen from the product.

**3. Context strip**
- Dark or tinted background (brand primary or deep surface color)
- 3-column data layout: large number (display font) + one-line label below
- Use the 3 data points from Agent 4's Context Strip copy
- Full-width, generous vertical padding
- No decorative elements — the numbers are the design

**4. Truth points ("What you actually get")**
- 2-column asymmetric layout: numbers (01-04) left, content right — OR 2×2 grid at desktop
- Each point: large typographic number (display font, muted/accent color) + headline + description
- No icons, no emoji, no icon circles
- Generous internal padding between points
- Background: off-white or light surface color (not white-white)

**5. How it works**
- Full-bleed colored background (brand primary color) — this section breaks the page rhythm intentionally
- 3 horizontal columns at desktop, vertical stack on mobile
- Each step: large step number (display font, accent/secondary color) + headline + description
- A thin colored line or dot sequence connecting steps (CSS-only, horizontal)
- White or light text on the dark background

**6. Testimonials — 3-card layout**
- Featured card (takes 60% width at desktop): larger quote, full name + persona description, brand primary background with white text
- Two supporting cards (20% each): shorter quotes, name only, surface background
- Cards are flush to each other (gap not gutter), rounded corners on outer edges only
- No quotation mark decorations (typography handles this)

**7. FAQ**
- Left-aligned, 2/3 page width, centered in container
- CSS-only accordion: `<input type="checkbox" id="faq-N">` + `<label for="faq-N">` + `.faq-answer`
- Clean expand/collapse with chevron that rotates on open
- Subtle border below each item (no bounding box per item)

**8. Final CTA block**
- Dark rounded rectangle (brand primary, border-radius ~16px), contained within page grid
- Two-column at desktop: left has headline + supporting copy, right has button(s)
- Primary button: contrasting color (accent/secondary), generous padding
- Optional: secondary text link below primary button

**9. Footer**
- 3-column: logo+tagline left, nav links center, secondary links right
- Thin border-top separator
- Muted text color, clean and minimal

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

### Save Files + Generate PDF

**Step 1: Save HTML files into standardized repo structure**

```bash
# Create standardized repo structure
REPO_DIR="$BRAND_DIR/[CHOSEN_NAME]-brand"
mkdir -p "$REPO_DIR/site/images" "$REPO_DIR/docs"

# Save site files
cp /tmp/landing.html "$REPO_DIR/site/index.html"
cp /tmp/brand-guidelines.html "$REPO_DIR/site/brand-guidelines.html"

# Copy any generated images to site/images/
cp "$BRAND_DIR/images/"*.{jpg,png,svg} "$REPO_DIR/site/images/" 2>/dev/null

echo "FILES SAVED:"
ls -lhR "$REPO_DIR/"
```

**Step 2: Generate brand guidelines PDF automatically**

```bash
# Set up puppeteer in a temp working dir (reuses existing install if present)
PDF_WORK="/tmp/brand-pdf-work"
mkdir -p "$PDF_WORK"

if [ ! -d "$PDF_WORK/node_modules/puppeteer" ]; then
  echo "Installing puppeteer (one-time, ~3 minutes)..."
  npm install puppeteer --prefix "$PDF_WORK" --silent
fi

# Write the PDF generation script
cat > "$PDF_WORK/gen.mjs" << 'GENEOF'
import puppeteer from './node_modules/puppeteer/lib/esm/puppeteer/puppeteer.js';

const HTML = process.env.HTML_PATH;
const PDF  = process.env.PDF_PATH;

const browser = await puppeteer.launch({
  headless: true,
  args: ['--no-sandbox', '--disable-setuid-sandbox', '--font-render-hinting=none']
});

const page = await browser.newPage();
await page.setViewport({ width: 794, height: 1123 });
await page.goto(`file://${HTML}`, { waitUntil: 'networkidle0', timeout: 30000 });
await page.evaluate(() => document.fonts.ready);
await new Promise(r => setTimeout(r, 3000)); // settle webfonts (Fontshare + Google)
await page.pdf({
  path: PDF,
  format: 'A4',
  printBackground: true,
  margin: { top: '0', right: '0', bottom: '0', left: '0' },
  preferCSSPageSize: true
});
await browser.close();
console.log('PDF saved to:', PDF);
GENEOF

# Generate PDF
HTML_PATH="$BRAND_DIR/[CHOSEN_NAME]-brand-guidelines.html" \
PDF_PATH="$BRAND_DIR/[CHOSEN_NAME]-brand-guidelines.pdf" \
  node "$PDF_WORK/gen.mjs"
```

If puppeteer install fails or the PDF generation errors, tell the user: "PDF generation failed — open `brand-guidelines.html` in Chrome and use File → Print → Save as PDF for a manual export. The HTML is fully print-ready."

**Step 3: Open files for review**

```bash
open "$BRAND_DIR/[CHOSEN_NAME]-landing.html"
open "$BRAND_DIR/[CHOSEN_NAME]-brand-guidelines.html"
```

Tell user: "Landing page and brand guidelines are open. PDF also saved alongside the HTML. Review them before I push to GitHub?"

---

## Agent 6: Publisher — Structured Repo + GitHub Push + Netlify Deploy

The Publisher assembles the standardized repo, deploys to Netlify, creates a private GitHub repo, and pushes all brand assets.

### Standardized Repo Structure

**Every brand MUST follow this exact structure:**

```
[chosen-name]-brand/
├── site/                              # Deployable website (Netlify publish dir)
│   ├── index.html                     # Production landing page
│   ├── brand-guidelines.html          # Printable brand book (open in browser)
│   └── images/                        # Generated illustrations, OG images
│       ├── hero-bg.jpg
│       ├── og-image.jpg
│       └── ...
├── docs/                              # Brand strategy & reference documents
│   ├── discovery-interview.md         # Q&A transcript from Agent 1 (REQUIRED)
│   ├── branding-context.md            # Full brief, identity, copy, research
│   └── [any-other-docs].md            # Whitepaper, plans, etc.
├── netlify.toml                       # Deploy config (publish = "site")
└── README.md                          # Project overview + identity quick ref
```

**Key rules:**
- `site/` contains ONLY deployable files — HTML, images, SVGs. No markdown.
- `docs/` contains ALL brand documentation — discovery interview, branding context, whitepapers, plans.
- `docs/discovery-interview.md` is **REQUIRED** — it preserves the founder's exact words from Agent 1.
- `netlify.toml` always sets `publish = "site"` so Netlify deploys from the right directory.
- Images go in `site/images/` — never loose in the root.

### Step 1: Assemble Docs

Save the discovery interview and branding context into `docs/`:

```bash
REPO_DIR="$BRAND_DIR/[CHOSEN_NAME]-brand"

# discovery-interview.md was saved during Agent 1
# Now save the full branding context (brief + identity + copy + research)
cat > "$REPO_DIR/docs/branding-context.md" << 'EOF'
# [Brand Name] — Brand Context & Findings
[Full brand brief, identity system, landing copy, market research, references]
EOF
```

### Step 2: Create netlify.toml

```toml
[build]
  publish = "site"

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

### Step 3: Create README.md

```markdown
# [Brand Name]

**[Tagline]**

[30-word positioning statement from brand brief]

## Live Site

**https://[CHOSEN_DOMAIN]**

## Structure

\```
[chosen-name]-brand/
├── site/                         # Landing page (deployed to Netlify)
│   ├── index.html                # Production landing page
│   ├── brand-guidelines.html     # Printable brand book
│   └── images/                   # Generated illustrations
├── docs/                         # Brand documents
│   ├── discovery-interview.md    # Founder Q&A from brand studio
│   └── branding-context.md       # Full brief, identity, copy, research
├── netlify.toml                  # Netlify deploy config
└── README.md
\```

## Deploy

Connected to Netlify. Pushes to `main` auto-deploy from the `site/` directory.

## Identity

| Token | Value |
|-------|-------|
| Primary | `[hex]` |
| Secondary | `[hex]` |
| Accent | `[hex]` |
| Display Font | [font name] |
| Body Font | [font name] |

## Domain

`[CHOSEN_DOMAIN]` — [registrar] → Netlify DNS
```

### Step 4: Deploy to Netlify

```bash
cd "$REPO_DIR/site"
netlify deploy --prod --dir=. --site-name=[chosen-name]
```

If `netlify` CLI is available, deploy directly. If not, tell the user to connect the GitHub repo to Netlify manually.

### Step 5: Push to GitHub

```bash
REPO_NAME="[chosen-name]-brand"
cd "$REPO_DIR"
git init
git add -A
git commit -m "Initial commit — [Brand Name] brand assets and landing page

- Landing page (site/index.html)
- Brand guidelines (site/brand-guidelines.html)
- Discovery interview Q&A (docs/discovery-interview.md)
- Branding context and research (docs/branding-context.md)
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
DOMAIN:          [domain] ([status])

LIVE SITE:       https://[chosen-name].netlify.app
GITHUB REPO:     https://github.com/[user]/[chosen-name]-brand (private)

REPO STRUCTURE:
  site/index.html              — Landing page
  site/brand-guidelines.html   — Brand book
  site/images/                 — Generated illustrations
  docs/discovery-interview.md  — Founder Q&A
  docs/branding-context.md     — Brief + identity + copy + research
  netlify.toml                 — Deploy config
  README.md                    — Project overview

NEXT STEPS:
  1. Review the live site
  2. Point [domain] DNS to Netlify:
     A record: @ → 75.2.60.5
     CNAME: www → [chosen-name].netlify.app
  3. Enable HTTPS in Netlify domain settings
  4. Connect GitHub repo to Netlify for auto-deploy on push

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
