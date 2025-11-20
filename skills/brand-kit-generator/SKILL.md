---
skill_name: brand-kit-generator
description: Generate complete brand color systems with accessibility validation and design token exports. Use when creating color palettes from images or descriptions, building brand kits with semantic naming, validating WCAG compliance, or exporting design tokens (Tailwind, CSS, JSON). Includes 11-shade scale generation, dark mode support, and color theory principles.
version: 1.0.0
author: MaWoo Development
tags: [design, colors, brand, accessibility, wcag, tailwind, design-tokens]
---

# Brand Kit & Color Palette Generator

## Activation

This skill activates when users need to:
- Generate color palettes from images or descriptions
- Create complete brand color systems
- Validate accessibility compliance (WCAG)
- Export design tokens for Tailwind, CSS, or design tools
- Develop full brand kits with semantic naming

**Trigger phrases**: "create a color palette", "brand kit", "extract colors from", "generate brand colors", "design tokens", "accessibility check", "WCAG compliance", "dark mode colors"

---

## Quick Start vs Comprehensive

### Quick Start Mode
For fast palette generation when user wants speed over strategy:
```
User: "Quick palette for a fitness app"
→ Skip detailed discovery
→ Apply industry defaults (fitness = energy, motivation)
→ Generate 5 colors with scales
→ Validate accessibility
→ Export ready-to-use tokens
```

### Comprehensive Mode
For full brand development (default when user asks for "brand kit"):
```
User: "Create a complete brand kit for my startup"
→ Full discovery questionnaire
→ Competitor analysis
→ Multiple palette options
→ Light + dark mode
→ Complete documentation
```

---

## Phase 1: Discovery & Strategy

Before generating any colors, gather context:

### Required Questions
1. **Brand/Business**: What is the business name and what do they do?
2. **Industry**: What sector? (tech, healthcare, finance, creative, etc.)
3. **Target Audience**: Who are the primary users/customers?
4. **Emotional Goals**: What feelings should the brand evoke? (trust, energy, calm, innovation)
5. **Existing Assets**: Any current brand colors, logos, or constraints?
6. **Use Cases**: Where will colors be used? (website, app, print, marketing)
7. **Competitors**: Any brands to differentiate from?

### Optional Context
- Color preferences or dislikes
- Cultural considerations for global brands
- Light mode, dark mode, or both
- Specific accessibility requirements beyond WCAG AA

### Competitor Analysis
Before finalizing palette, briefly check:
```
1. Identify 2-3 direct competitors
2. Note their primary brand colors
3. Ensure differentiation (different hue family or saturation level)
4. Document why your palette stands out
```

---

## Phase 2: Palette Generation

### From Image Analysis
When user uploads an image:
```
1. Extract 5-8 dominant colors
2. Identify roles: primary, secondary, accent, neutral
3. Provide for each color:
   - Hex code (uppercase): #3A4D7E
   - Descriptive name: "Ocean Depth Blue"
   - Role in palette
   - Emotional association
4. Create visual artifact with swatches
```

### From Text Description
Apply color theory principles:

**Color Psychology Reference**:
- Blue: Trust, stability, professionalism
- Green: Growth, health, sustainability
- Red: Energy, urgency, passion
- Orange: Creativity, enthusiasm, warmth
- Purple: Luxury, creativity, wisdom
- Yellow: Optimism, clarity, warmth
- Neutral: Sophistication, balance, timelessness

**Color Harmony Methods**:
- Complementary: High contrast, vibrant
- Analogous: Harmonious, cohesive
- Triadic: Balanced, dynamic
- Split-complementary: Contrast with less tension
- Monochromatic: Elegant, unified

### Initial Palette Structure
Generate 5-8 core colors:
```
Primary:     Main brand color (60% usage)
Secondary:   Supporting color (30% usage)
Accent:      Call-to-action, highlights (10% usage)
Neutral-Light: Backgrounds, cards
Neutral-Dark:  Text, borders
Success:     #10B981 (green family)
Warning:     #F59E0B (amber family)
Error:       #EF4444 (red family)
```

---

## Phase 3: Scale Development

Generate 11-shade scales using perceptually uniform steps (Lab/LCH color space):

### Shade Scale Template
```
50:  Lightest - subtle backgrounds
100: Light backgrounds
200: Hover states on light
300: Borders, dividers
400: Placeholder text
500: Base color (starting point)
600: Hover on base
700: Active states
800: Text on light backgrounds
900: Headings, emphasis
950: Darkest - near black variant
```

### Scale Generation Rules
- Use Lab color space for perceptual uniformity
- Maintain consistent hue (±5°) across scale
- Decrease saturation slightly at extremes
- 50-200: Background-safe (light enough for text)
- 600-950: Text-safe (dark enough for contrast)

### Example Scale Output
```css
--color-primary-50: #EFF6FF;
--color-primary-100: #DBEAFE;
--color-primary-200: #BFDBFE;
--color-primary-300: #93C5FD;
--color-primary-400: #60A5FA;
--color-primary-500: #3B82F6;  /* Base */
--color-primary-600: #2563EB;
--color-primary-700: #1D4ED8;
--color-primary-800: #1E40AF;
--color-primary-900: #1E3A8A;
--color-primary-950: #172554;
```

---

## Phase 4: Dark Mode Support

When generating for both light and dark modes:

### Dark Mode Strategy
```
Option 1: Inverted Scales (Recommended)
- Light mode: 50-200 backgrounds, 700-950 text
- Dark mode: 800-950 backgrounds, 50-300 text
- Same scales, different semantic mappings

Option 2: Adjusted Saturation
- Dark backgrounds need lower saturation colors
- Reduce saturation 10-20% for dark mode variants
- Maintain hue consistency
```

### Semantic Token Mapping
```css
/* Light Mode */
:root {
  --color-bg-primary: var(--color-neutral-50);
  --color-bg-secondary: var(--color-neutral-100);
  --color-text-primary: var(--color-neutral-900);
  --color-text-secondary: var(--color-neutral-600);
  --color-border: var(--color-neutral-200);
}

/* Dark Mode */
:root.dark {
  --color-bg-primary: var(--color-neutral-900);
  --color-bg-secondary: var(--color-neutral-800);
  --color-text-primary: var(--color-neutral-50);
  --color-text-secondary: var(--color-neutral-400);
  --color-border: var(--color-neutral-700);
}
```

### Dark Mode Accessibility
- Re-validate all contrast ratios for dark backgrounds
- Primary colors often need lightening for dark mode
- Test both modes independently

---

## Phase 5: Accessibility Validation

### WCAG Contrast Requirements
| Text Type | AA Minimum | AAA Enhanced |
|-----------|------------|--------------|
| Normal text (< 18pt) | 4.5:1 | 7:1 |
| Large text (≥ 18pt / 14pt bold) | 3:1 | 4.5:1 |
| UI components, graphics | 3:1 | 3:1 |

### Required Tests
```
✓ Primary text on all backgrounds
✓ Secondary text on all backgrounds
✓ Button text on button backgrounds
✓ Link colors on backgrounds
✓ Border/icon contrast
✓ Hover and focus states
```

### Validation Output Format
```
Text: Primary-900 on Neutral-50
Contrast: 12.4:1
Status: ✓ Passes WCAG AAA

Text: Primary-500 on Neutral-100
Contrast: 3.2:1
Status: ✗ Fails AA for normal text
Fix: Use Primary-700 (5.1:1) or Primary-800 (7.3:1)
```

### When Accessibility Fails
1. Never just report failure—provide specific fix
2. Suggest exact shade from scale that works
3. Show before/after contrast improvement
4. Explain impact in plain language

---

## Phase 5: Design System Export

### CSS Custom Properties
```css
:root {
  /* Primitive Tokens */
  --color-blue-500: #3B82F6;
  --color-blue-600: #2563EB;

  /* Semantic Tokens */
  --color-primary: var(--color-blue-500);
  --color-primary-hover: var(--color-blue-600);
  --color-text-primary: var(--color-gray-900);
  --color-text-secondary: var(--color-gray-600);
  --color-bg-primary: var(--color-white);
  --color-bg-secondary: var(--color-gray-50);
  --color-border: var(--color-gray-200);
}
```

### Tailwind CSS Configuration
```css
@theme {
  --color-primary-50: #EFF6FF;
  --color-primary-100: #DBEAFE;
  --color-primary-200: #BFDBFE;
  --color-primary-300: #93C5FD;
  --color-primary-400: #60A5FA;
  --color-primary-500: #3B82F6;
  --color-primary-600: #2563EB;
  --color-primary-700: #1D4ED8;
  --color-primary-800: #1E40AF;
  --color-primary-900: #1E3A8A;
  --color-primary-950: #172554;

  --color-secondary-*: /* secondary scale */;
  --color-accent-*: /* accent scale */;
  --color-neutral-*: /* neutral scale */;
}
```

### Design Tokens JSON (Style Dictionary)
```json
{
  "color": {
    "primary": {
      "50": { "value": "#EFF6FF" },
      "500": { "value": "#3B82F6" },
      "900": { "value": "#1E3A8A" }
    },
    "semantic": {
      "text": {
        "primary": { "value": "{color.neutral.900}" },
        "secondary": { "value": "{color.neutral.600}" }
      },
      "background": {
        "primary": { "value": "{color.neutral.50}" }
      }
    }
  }
}
```

---

## Phase 6: Documentation

### Style Guide Structure
```markdown
# [Brand Name] Color System

## Brand Colors
[Visual swatches with hex codes]

## Color Scales
[Full 50-950 scales for each color]

## Accessibility Matrix
[Contrast ratios for all text/background pairs]

## Usage Guidelines
- Primary: CTAs, links, key UI elements
- Secondary: Supporting elements, tags
- Accent: Highlights, notifications
- Neutrals: Text, backgrounds, borders

## Code Implementation
[CSS variables, Tailwind config, tokens]
```

---

## Color Theory Principles

### Always Apply
1. **60-30-10 Rule**: Dominant (60%), Secondary (30%), Accent (10%)
2. **Perceptual Uniformity**: Use Lab/LCH for calculations
3. **Saturation Balance**: Vary saturation for depth
4. **Cultural Context**: Research color meanings globally
5. **Brand Differentiation**: Check competitor colors

### Avoid Common Pitfalls
- ❌ Pure black (#000000) or white (#FFFFFF)
- ❌ Uneven perceptual steps in scales
- ❌ Palettes without brand context
- ❌ Skipping accessibility validation
- ❌ Raw hex codes without semantic names

### Color Adjustments
When user requests changes like "more energetic":
```
Analyze: Current saturation/brightness levels
Explain: What creates the desired effect
Adjust: Specific values with before/after
Validate: Re-check accessibility
```

---

## Visual Artifacts

When creating color artifacts:

### Required Elements
- Clean, organized layout
- Hex codes visible and copyable
- Color names and roles labeled
- WCAG compliance indicators
- Usage context examples

### Artifact Types
- **React Component**: Interactive palette explorer
- **HTML**: Static style guide with copy buttons
- **SVG**: Color wheels, harmony diagrams
- **Contrast Matrix**: Text on background samples

### Example Swatch Component
```tsx
<div className="flex flex-col gap-2">
  <div
    className="h-16 rounded-lg flex items-end p-2"
    style={{ backgroundColor: '#3B82F6' }}
  >
    <span className="text-white text-sm font-mono">#3B82F6</span>
  </div>
  <div className="text-sm">
    <p className="font-medium">Primary Blue</p>
    <p className="text-gray-500">Main brand color, CTAs</p>
  </div>
</div>
```

---

## Iteration Support

### Version Tracking
- Label iterations: v1, v2, v3
- Show before/after comparisons
- Document reasoning for changes

### Refinement Approach
1. Make incremental adjustments (±10% saturation/lightness)
2. Provide 2-3 alternatives for uncertain choices
3. Ask specific questions: "Is the primary too bright?" not "Do you like it?"
4. Always explain the "why" behind changes

---

## Export Checklist

Before delivering final palette:

- [ ] All colors have descriptive names
- [ ] Full 11-shade scales generated
- [ ] WCAG AA compliance validated
- [ ] Semantic tokens defined
- [ ] CSS variables provided
- [ ] Tailwind config provided
- [ ] Usage guidelines documented
- [ ] Visual artifact created
- [ ] Accessibility matrix included

---

## Quick Reference

### Contrast Calculation
```
Contrast Ratio = (L1 + 0.05) / (L2 + 0.05)
Where L1 = lighter color luminance
      L2 = darker color luminance
```

### Safe Pairings
```
Text on light backgrounds: Use 700-950 shades
Text on dark backgrounds: Use 50-300 shades
Large text/UI: Can use 500-600 on light
```

### Semantic Color Defaults
```
Success: Green family (#10B981)
Warning: Amber family (#F59E0B)
Error: Red family (#EF4444)
Info: Blue family (#3B82F6)
```

---

## Tools & Libraries

### Recommended for Implementation
```
Color Manipulation:
- chroma-js: Color conversions, scales, contrast
- culori: OKLCH/Lab calculations, modern color spaces
- color: Simple color parsing and manipulation

Online Tools:
- Realtime Colors: Live preview on UI mockups
- Coolors: Palette generation and exploration
- Contrast Checker: WebAIM contrast validation
- OKLCH Color Picker: Perceptually uniform adjustments
```

### Code Example with chroma-js
```javascript
import chroma from 'chroma-js';

// Generate perceptually uniform scale
const generateScale = (baseColor, steps = 11) => {
  const base = chroma(baseColor);
  return chroma
    .scale(['#ffffff', base, '#000000'])
    .mode('lab')
    .colors(steps);
};

// Check contrast ratio
const contrast = chroma.contrast('#3B82F6', '#ffffff');
// Returns: 4.5 (passes AA for large text)
```

### Color Palette Resources (2025)

```typescript
const colorTools = {
  // Gradient generator
  hypercolor: {
    url: 'https://hypercolor.dev',
    best_for: 'Tailwind gradient presets',
    usage: 'Copy-paste gradient classes',
  },

  // OKLCH - 2025 standard for perceptual uniformity
  oklch_picker: {
    url: 'https://oklch.com',
    best_for: 'Perceptually uniform color scales',
    note: 'Modern color space, better than HSL',
  },

  // AI color generation
  huemint: {
    url: 'https://huemint.com',
    best_for: 'AI-generated palettes for brand identity',
  },

  khroma: {
    url: 'https://www.khroma.co',
    best_for: 'AI learns your color preferences',
  },

  // Accessibility
  contrast_checker: {
    url: 'https://webaim.org/resources/contrastchecker/',
    best_for: 'WCAG contrast validation',
  },

  // Realtime preview
  realtime_colors: {
    url: 'https://www.realtimecolors.com',
    best_for: 'Preview colors on actual UI',
  },
};
```

---

## Font Pairing Recommendations (2025 Meta)

### Typography Resources

**Tier 1 - The 2025 Standard:**

```typescript
const typographyResources = {
  // #1 Pick - 70-80% of hot 2025 landing pages use these
  fontshare: {
    url: 'https://www.fontshare.com',
    license: '100% free for commercial use, no attribution',
    run_by: 'Indian Type Foundry (ITF)',
    top_fonts: [
      'General Sans',      // The 2025 body font meta
      'Switzer',           // Satoshi alternative
      'Cabinet Grotesk',   // Premium display
      'Instrument Sans',   // Clean modern
      'Instrument Serif',  // Elegant headlines
      'Bricolage Grotesque', // Quirky display
      'Teneur',            // Luxury serif
      'Clash Grotesk',     // Tech headlines (free weights)
    ],
  },

  // Self-host any font with npm - fixes Google CDN speed + privacy
  fontsource: {
    url: 'https://fontsource.org',
    best_for: 'Self-hosting Google Fonts + others',
    note: 'Used in every serious Next.js + Tailwind project in 2025',
    install: 'npm install @fontsource-variable/general-sans',
  },

  // Google Fonts - still excellent for specific pairings
  google_fonts_2025_picks: [
    'Manrope',           // Clean geometric sans
    'Plus Jakarta Sans', // Perfect Neue Montreal replacement
    'Space Grotesk',     // Tech/futuristic headlines
    'Outfit',            // Friendlier Inter alternative
    'Syne',              // Quirky display for creative agencies
  ],

  // Paid with generous free tiers
  pangram_pangram: {
    url: 'https://pangrampangram.com',
    fonts: ['Neue Montreal', 'Clash Display', 'Satoshi', 'Mona Sans'],
    note: 'Free personal-use weights or lookalikes available',
  },

  collletttivo: {
    url: 'https://collletttivo.it',
    best_for: 'High-end fonts with generous free weights',
    fonts: ['Obviously', 'Teneur'],
  },
};
```

### The 2025 Copy-Paste Pairings

These instantly make your site look like a $10k+ template:

**Tech / SaaS:**
```css
font-family: "General Sans", sans-serif;      /* body - Fontshare */
font-family: "Switzer", sans-serif;           /* alternative body */
font-family: "Clash Grotesk", sans-serif;     /* headlines - free weights */
```

**Premium / Luxury:**
```css
font-family: "Teneur", serif;                 /* headlines - Fontshare */
font-family: "Cabinet Grotesk", sans-serif;   /* body - Fontshare */
```

**Modern Corporate:**
```css
font-family: "Manrope", sans-serif;           /* body - Google Fonts */
font-family: "Space Grotesk", sans-serif;     /* headlines */
```

**Friendly / Consumer:**
```css
font-family: "Obviously", sans-serif;         /* headlines - Collletttivo */
font-family: "Inter", sans-serif;             /* body */
```

**Playful / Creative:**
```css
font-family: "Syne", sans-serif;              /* headlines - Google Fonts */
font-family: "Instrument Sans", sans-serif;   /* body - Fontshare */
```

### Quick Setup with Fontsource

**Install the 2025 meta stack:**
```bash
npm install @fontsource-variable/general-sans @fontsource-variable/switzer @fontsource-variable/instrument-sans
```

**Import in your CSS:**
```css
@import "@fontsource-variable/general-sans";
@import "@fontsource-variable/switzer";
@import "@fontsource-variable/instrument-sans";
```

**Or for Google Fonts alternatives:**
```bash
npm install @fontsource-variable/manrope @fontsource-variable/space-grotesk @fontsource-variable/plus-jakarta-sans
```

### Font Configuration in Tailwind CSS 4

```css
@theme inline {
  /* Tech / SaaS (The 2025 Meta) */
  --font-heading: 'Clash Grotesk', 'Space Grotesk', system-ui, sans-serif;
  --font-sans: 'General Sans', 'Switzer', system-ui, sans-serif;

  /* Premium / Luxury */
  --font-heading: 'Teneur', Georgia, serif;
  --font-sans: 'Cabinet Grotesk', system-ui, sans-serif;

  /* Modern Corporate */
  --font-heading: 'Space Grotesk', system-ui, sans-serif;
  --font-sans: 'Manrope', system-ui, sans-serif;

  /* Playful / Creative */
  --font-heading: 'Syne', system-ui, sans-serif;
  --font-sans: 'Instrument Sans', system-ui, sans-serif;
}
```

### Industry Font Recommendations

| Industry | Heading Font | Body Font | Source |
|----------|-------------|-----------|--------|
| Tech / SaaS | Clash Grotesk | General Sans | Fontshare |
| Finance / Luxury | Teneur | Cabinet Grotesk | Fontshare |
| Modern Corporate | Space Grotesk | Manrope | Google Fonts |
| Consumer / Friendly | Obviously | Inter | Collletttivo / Google |
| Creative / Agency | Syne | Instrument Sans | Google / Fontshare |
| E-commerce | Plus Jakarta Sans | Outfit | Google Fonts |
| Developer | Space Grotesk | Inter | Google Fonts |

### Google Fonts Direct Links

```css
/* Tech / SaaS */
@import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Manrope:wght@400;500;600;700;800&display=swap');

/* Friendly / Consumer */
@import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&family=Outfit:wght@400;500;600;700&display=swap');

/* Playful / Creative */
@import url('https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&display=swap');
```

---

## Interactive Refinement

### Specific Adjustment Questions
Instead of "Do you like it?", ask:

**For Hue Issues:**
- "Should the primary lean more toward [warmer/cooler] tones?"
- "Is the green too yellow-ish or too blue-ish?"

**For Saturation Issues:**
- "Does the palette feel too vibrant/muted for your brand?"
- "Should the accent color pop more or blend in?"

**For Lightness Issues:**
- "Are the dark shades dark enough for good contrast?"
- "Do the light backgrounds feel too stark or too creamy?"

### Before/After Refinement Examples

**Request: "Make it more energetic"**
```
Before: Primary #4A6FA5 (muted blue, S: 45%, L: 47%)
After:  Primary #3B82F6 (vibrant blue, S: 90%, L: 60%)

Changes made:
- Increased saturation from 45% to 90%
- Increased lightness from 47% to 60%
- Shifted hue slightly warmer (more purple undertone)

Why: Higher saturation creates visual energy;
     increased lightness adds brightness/optimism
```

**Request: "Too corporate, needs to feel friendlier"**
```
Before: Primary #1E3A5F (dark navy)
After:  Primary #6366F1 (indigo-violet)

Changes made:
- Shifted hue from blue (220°) to violet (239°)
- Increased lightness significantly
- Added warmth to feel more approachable

Why: Purple/violet feels more creative and playful;
     lighter colors feel less formal and austere
```

**Request: "The accent doesn't stand out enough"**
```
Before: Accent #F59E0B on Primary #3B82F6 background
After:  Accent #FBBF24 on Primary #1E40AF background

Changes made:
- Lightened accent for better contrast
- Darkened primary background
- Maintained complementary relationship

Why: Increased value contrast between accent and background;
     complementary colors (blue/orange) already have hue contrast
```

---

## Export Formats

### Figma Import (ASE/JSON)
```json
{
  "name": "Brand Colors",
  "colors": [
    {
      "name": "Primary/500",
      "color": { "r": 0.231, "g": 0.510, "b": 0.965 }
    },
    {
      "name": "Primary/600",
      "color": { "r": 0.145, "g": 0.388, "b": 0.922 }
    }
  ]
}
```

### Adobe ASE Format
For Illustrator/Photoshop import:
```
Provide hex values in format:
Primary 500: #3B82F6
Primary 600: #2563EB
(User can import via Coolors or ASE converter)
```

### CSS-in-JS (styled-components/emotion)
```typescript
export const colors = {
  primary: {
    50: '#EFF6FF',
    500: '#3B82F6',
    900: '#1E3A8A',
  },
  semantic: {
    text: {
      primary: '#111827',
      secondary: '#4B5563',
    },
    background: {
      primary: '#FFFFFF',
      secondary: '#F9FAFB',
    },
  },
} as const;
```
