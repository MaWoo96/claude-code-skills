# Brand Kit & Color Palette Generator

## Activation

This skill activates when users need to:
- Generate color palettes from images or descriptions
- Create complete brand color systems
- Validate accessibility compliance (WCAG)
- Export design tokens for Tailwind, CSS, or design tools
- Develop full brand kits with semantic naming

**Trigger phrases**: "create a color palette", "brand kit", "extract colors from", "generate brand colors", "design tokens", "accessibility check", "WCAG compliance"

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

## Phase 4: Accessibility Validation

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
