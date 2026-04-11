# Visual Identity System Reference

## Colour Theory for Brand Palettes

### Palette Archetypes by Brand Personality

**Bold / Disruptive**
- Primary: Saturated primary (electric blue #0066FF, vivid red #FF2D2D, neon lime #C8FF00)
- Background: Near-black (#060608, #0D0D0D, #111111)
- Text: White (#FFFFFF) or near-white (#F5F5F5)
- Accent: Contrasting neon (cyan, magenta, orange)
- Pattern: High contrast, neon-on-dark, maximum energy

**Calm / Trustworthy (B2B, Fintech, Health)**
- Primary: Muted blue-green (#2D6A9F, #0E7C6B, #1A5E8A)
- Background: Off-white (#FAFAFA, #F8F9FA) or light grey (#F0F2F5)
- Text: Dark slate (#1A1A2E, #2D3142, #111827)
- Accent: Slightly saturated version of primary
- Pattern: Restrained, 2-colour, high legibility

**Premium / Luxury**
- Primary: Near-black (#0A0A0A) or deep navy (#060B27)
- Secondary: Gold (#C9A84C, #D4AF37) or platinum (#E8E8E8)
- Background: Very dark (#050505) or cream (#FAF8F3)
- Text: White or aged white (#F5F0E8)
- Pattern: Minimal colour, maximum contrast, precious

**Warm / Human (Consumer, Community, Education)**
- Primary: Warm amber (#FF6B35), terracotta (#C84B31), sage (#6B8F71)
- Background: Warm white (#FFFBF5, #FFF8F0)
- Text: Warm black (#1C1410, #2D1B0E)
- Accent: Complementary warm (mustard, rust, olive)
- Pattern: Earthy, inviting, approachable

**Playful / Gen Z**
- Primary: Bright primary (coral #FF6B6B, bubblegum #FF85A2, sky #4ECDC4)
- Background: White or light tinted (#FFF5F7)
- Text: Near-black (#1A1A2E)
- Accent: Multiple saturated accents (≥3 colours in harmony)
- Pattern: High saturation, bouncy, maximalist-friendly

---

## Typography Pairings

### Pairing 1: Editorial Authority
- Display: Fraunces (Optical Italic) — emotional, literary
- Body: DM Sans — clean, neutral workhorse
- Mono: JetBrains Mono — technical precision
- Works for: Media, journalism, premium consumer

### Pairing 2: Modern Technical
- Display: Clash Grotesk — geometric, commanding
- Body: Plus Jakarta Sans — versatile, internationally legible
- Mono: Geist Mono — Vercel-grade precision
- Works for: Developer tools, SaaS, AI products

### Pairing 3: Warm Human
- Display: Cabinet Grotesk — friendly geometric
- Body: Outfit — rounded, warm
- Mono: Space Mono — retro precision
- Works for: Consumer apps, community tools, education

### Pairing 4: Luxury Minimal
- Display: Instrument Serif — serene authority
- Body: Instrument Sans — its companion sans
- Mono: IBM Plex Mono — Swiss precision
- Works for: Finance, real estate, premium services

### Pairing 5: Bold Startup
- Display: General Sans ExtraBold — energetic, confident
- Body: Inter Variable — the trusted workhorse (acceptable here for clarity)
- Mono: Fira Code — developer-friendly
- Works for: B2B SaaS, marketplace, productivity

---

## Logo Wordmark Rules

### Capitalisation
- **ALL CAPS**: Authority, bold, commanding. Best with geometric sans.
- **Title Case**: Professional, accessible. Works with most typefaces.
- **lowercase only**: Approachable, modern, digital-native. Risky if typeface isn't distinctive.

### Colour Split Patterns
- **Two-colour split**: First word in accent, rest in primary (0TO1.SPACE pattern)
- **Single colour**: Clean and versatile. Recommended for most cases.
- **Gradient**: Use sparingly. Only if gradient is a core brand element.
- **Hollow/outline text**: Signature for bold aesthetics (stroke only, no fill)

### Sizing Rules
- Minimum digital: 120px wide
- Minimum print: 25mm wide
- Clear space: height of the tallest letter on all sides
- Never below minimum — use abbreviated version instead

---

## CSS Variables Template

```css
:root {
  /* Brand Colours */
  --color-primary: #[hex];
  --color-secondary: #[hex];
  --color-accent: #[hex];

  /* Surfaces */
  --color-bg: #[hex];
  --color-surface-1: #[hex];
  --color-surface-2: #[hex];
  --color-border: #[hex];

  /* Text */
  --color-text-primary: #[hex];
  --color-text-muted: rgba([r],[g],[b],0.55);
  --color-text-faint: rgba([r],[g],[b],0.3);

  /* Typography */
  --font-display: '[Display Font]', sans-serif;
  --font-body: '[Body Font]', sans-serif;
  --font-mono: '[Mono Font]', monospace;

  /* Spacing (base: 8px) */
  --space-2xs: 0.25rem;  /* 4px */
  --space-xs:  0.5rem;   /* 8px */
  --space-sm:  0.75rem;  /* 12px */
  --space-md:  1rem;     /* 16px */
  --space-lg:  1.5rem;   /* 24px */
  --space-xl:  2rem;     /* 32px */
  --space-2xl: 3rem;     /* 48px */
  --space-3xl: 4rem;     /* 64px */
  --space-4xl: 6rem;     /* 96px */

  /* Border Radius */
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-xl: 20px;
  --radius-full: 9999px;

  /* Shadows */
  --shadow-sm: 0 1px 2px rgba(0,0,0,0.05);
  --shadow-md: 0 4px 6px rgba(0,0,0,0.07), 0 2px 4px rgba(0,0,0,0.05);
  --shadow-lg: 0 10px 15px rgba(0,0,0,0.1), 0 4px 6px rgba(0,0,0,0.05);
  --shadow-glow: 0 0 20px rgba([accent-r],[accent-g],[accent-b],0.3);

  /* Transitions */
  --transition-fast: 150ms ease;
  --transition-base: 250ms ease;
  --transition-slow: 400ms ease;
}
```

---

## Anti-Patterns to Avoid

**Colour anti-patterns:**
- Purple/violet gradient as default (massively overused in AI/SaaS 2023-2025)
- Rainbow gradients on hero backgrounds
- Low-contrast text on coloured backgrounds (WCAG AA minimum: 4.5:1)
- Too many accent colours (max 2 in a restrained palette, 3 in an expressive one)

**Typography anti-patterns:**
- Mixing more than 3 typefaces
- Using serif body + serif display (muddy hierarchy)
- All-caps body text beyond 3 words
- Font size below 14px for body (legibility)
- Line-height below 1.5 for body text

**Layout anti-patterns:**
- Centring everything (kills reading flow)
- Equal spacing between all elements (destroys hierarchy)
- 3-column feature grids with icons in coloured circles
- Generic "hero image of person smiling at laptop"
- Zero-radius cards that feel like rectangles vs. over-radiused cards that feel bubbly
