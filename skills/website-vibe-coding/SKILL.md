---
skill_name: website-vibe-coding
description: Build production-quality websites with minimal iteration by gathering requirements through a structured discovery phase, then implementing using proven patterns from production sites.
version: 1.0.0
author: MaWoo Development
tags: [web-development, nextjs, react, tailwind, responsive-design, frontend]
---

# Website Vibe Coding Skill

## Purpose

This skill enables near-one-time-use website generation with minimal back-and-forth by systematically gathering all requirements upfront, then implementing using battle-tested patterns from production websites. It ensures both desktop AND mobile layouts work correctly without critical errors.

## When to Activate This Skill

Activate when the user requests:
- "Build me a website for..."
- "Create a landing page for..."
- "I need a portfolio site"
- "Build a marketing site"
- "Create a business website"
- Any request to build a complete website from scratch

**Do NOT activate for**:
- Bug fixes in existing sites
- Small component additions
- Styling tweaks
- Debugging existing code

## Core Philosophy

1. **Discovery First**: Gather ALL requirements before writing code
2. **Mobile-First**: Design for mobile (375px), expand to desktop
3. **Proven Patterns**: Use only battle-tested code from production sites
4. **Quality Checkpoints**: Verify functionality at key stages
5. **Minimal Iteration**: Get it right the first time

---

## Phase 1: Discovery

### Step 1.1: Gather Business Context

Ask these questions BEFORE suggesting any technology or writing code:

**Project Classification**:
1. What type of website? (marketing site, portfolio, web app, e-commerce, content platform)
2. Approximate size? (< 10 pages, 10-50 pages, 50+ pages)
3. Primary goal? (lead generation, sales, information, engagement, bookings)

**Target Audience**:
4. Who is your target audience? (age range, tech-savviness, typical device)
5. What's the main action visitors should take? (contact, purchase, sign up, read, book)

**Content Status**:
6. Is content ready or do you need placeholder text?
7. Do you have images/media ready or need stock photos?
8. Any existing brand guidelines? (logo, colors, fonts)

### Step 1.2: Design Vibe Questionnaire

**Aesthetic Preference**:
9. What aesthetic describes your brand best?
   - [ ] Minimal (clean, spacious, simple)
   - [ ] Bold (vibrant, eye-catching, energetic)
   - [ ] Professional (trustworthy, corporate, polished)
   - [ ] Playful (fun, creative, colorful)
   - [ ] Elegant (sophisticated, refined, luxurious)
   - [ ] Modern (cutting-edge, tech-forward, sleek)

**Color Scheme**:
10. Primary brand color (hex code or description)?
11. Secondary/accent color (if any)?
12. Background preference (light, dark, or both)?

**Personality Traits** (select 3-5):
13. What words describe your brand?
    - [ ] Trustworthy
    - [ ] Innovative
    - [ ] Friendly
    - [ ] Professional
    - [ ] Creative
    - [ ] Reliable
    - [ ] Energetic
    - [ ] Calm
    - [ ] Bold
    - [ ] Approachable

**Inspiration**:
14. Any websites you admire? (provide URLs for reference)

### Step 1.3: Technical Requirements

**Features Needed**:
15. Which sections/features do you need?
    - [ ] Hero section with headline/CTA
    - [ ] About/Story section
    - [ ] Services/Features showcase
    - [ ] Testimonials/Reviews
    - [ ] Portfolio/Gallery
    - [ ] Pricing tables
    - [ ] FAQ accordion
    - [ ] Blog/News feed
    - [ ] Contact form
    - [ ] Email signup
    - [ ] Booking/Calendar
    - [ ] Live chat
    - [ ] Other (specify)

**Additional Requirements**:
16. Need SEO optimization? (affects framework choice)
17. Need user authentication/accounts? (requires backend)
18. Expected traffic volume? (affects hosting decisions)
19. Integration needs? (CRM, email marketing, analytics, etc.)

### Step 1.4: Discovery Summary

After gathering responses, provide a summary:

```markdown
## Project Summary

**Type**: [marketing-site/web-app/e-commerce/content-platform]
**Size**: [small/medium/large]
**Goal**: [primary objective]
**Audience**: [description]
**Vibe**: [aesthetic + 3-5 personality traits]

**Color Scheme**:
- Primary: #[hex]
- Secondary: #[hex]
- Background: [light/dark]

**Required Sections**:
1. [Section 1]
2. [Section 2]
...

**Special Features**:
- [Feature 1]
- [Feature 2]
...

**Technical Stack** (based on requirements):
- Framework: [Next.js 16/Vite + React]
- Styling: Tailwind CSS 4
- Animations: Motion library
- Components: Radix UI + custom
- Backend: [Supabase/None]
```

**Ask for confirmation**: "Does this summary accurately capture your vision? Any adjustments needed before I start building?"

---

## Phase 2: Architecture Setup

### Step 2.1: Technology Selection

Based on discovery responses, select stack:

**For Marketing Sites** (SEO-critical, content-heavy):
```typescript
const stack = {
  framework: 'Next.js 16',
  features: ['App Router', 'React Server Components', 'Image Optimization'],
  why: 'Best for SEO, static generation, and content sites',
};
```

**For Web Applications** (complex interactions, separate backend):
```typescript
const stack = {
  framework: 'Vite + React 18',
  features: ['Fast HMR', 'Manual chunking', 'Better SPA control'],
  why: 'Best for data-heavy apps with real-time features',
};
```

**Consistent Across All**:
- Styling: Tailwind CSS 4 with `@theme inline`
- Components: Radix UI primitives
- Animations: Motion library + useInView
- Icons: Lucide React
- Utilities: clsx, tailwind-merge, class-variance-authority

### Step 2.2: Project Initialization

**For Next.js Marketing Site**:
```bash
npx create-next-app@latest [project-name] --typescript --tailwind --app
cd [project-name]
npm install motion react-intersection-observer
npm install class-variance-authority clsx tailwind-merge
npm install lucide-react
npm install -D @tailwindcss/typography
```

**For Vite React App**:
```bash
npm create vite@latest [project-name] -- --template react-ts
cd [project-name]
npm install
npm install @tanstack/react-query
npm install @radix-ui/react-dialog @radix-ui/react-dropdown-menu
npm install class-variance-authority clsx tailwind-merge
npm install motion
npm install lucide-react
npx tailwindcss init -p
```

### Step 2.3: Configure Design Tokens

Create `src/app/globals.css` (Next.js) or `src/index.css` (Vite):

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@theme inline {
  /* User's Brand Colors */
  --color-primary: #[USER_PRIMARY];
  --color-secondary: #[USER_SECONDARY];
  --color-accent: #[USER_ACCENT];

  /* Neutral Palette */
  --color-background: #FFFFFF;
  --color-foreground: #1A1A1A;
  --color-muted: #F5F5F5;
  --color-border: #E5E5E5;

  /* Typography */
  --font-sans: [USER_FONT], system-ui, sans-serif;
  --font-heading: [USER_HEADING_FONT], var(--font-sans);
}

@layer components {
  /* Button Styles */
  .btn-primary {
    @apply inline-flex items-center justify-center gap-2
           px-6 sm:px-8 py-3 sm:py-4
           text-sm sm:text-base font-semibold text-white
           rounded-full transition-all duration-300
           hover:scale-105 active:scale-95
           focus-visible:outline-none focus-visible:ring-2
           focus-visible:ring-primary focus-visible:ring-offset-2;
    background: linear-gradient(135deg,
      var(--color-primary) 0%,
      var(--color-secondary) 50%,
      var(--color-accent) 100%);
  }

  .btn-secondary {
    @apply inline-flex items-center justify-center gap-2
           px-6 sm:px-8 py-3 sm:py-4
           text-sm sm:text-base font-semibold
           border-2 border-primary text-primary
           rounded-full transition-all duration-300
           hover:bg-primary hover:text-white
           focus-visible:outline-none focus-visible:ring-2;
  }

  /* Container */
  .section-container {
    @apply max-w-7xl mx-auto
           px-4 sm:px-6 lg:px-8
           py-12 sm:py-16 md:py-20 lg:py-24;
  }

  /* Typography */
  .heading-1 {
    @apply text-4xl sm:text-5xl md:text-6xl lg:text-7xl
           font-bold leading-tight font-heading;
  }

  .heading-2 {
    @apply text-3xl sm:text-4xl md:text-5xl lg:text-6xl
           font-bold leading-tight font-heading;
  }

  .heading-3 {
    @apply text-2xl sm:text-3xl md:text-4xl
           font-semibold leading-snug font-heading;
  }

  .body-large {
    @apply text-lg sm:text-xl md:text-2xl leading-relaxed;
  }

  .body {
    @apply text-base sm:text-lg leading-relaxed;
  }
}
```

### Step 2.4: Create Project Structure

**Directory Structure** (Next.js):
```
src/
├── app/
│   ├── layout.tsx
│   ├── page.tsx
│   ├── globals.css
│   └── api/
│       └── contact/
│           └── route.ts
├── components/
│   ├── layout/
│   │   ├── Header.tsx
│   │   ├── Footer.tsx
│   │   └── MobileNav.tsx
│   ├── sections/
│   │   ├── Hero.tsx
│   │   ├── [other sections]
│   │   └── Contact.tsx
│   ├── ui/
│   │   ├── Button.tsx
│   │   ├── Card.tsx
│   │   └── Input.tsx
│   └── shared/
│       ├── AnimatedSection.tsx
│       ├── Container.tsx
│       └── SectionHeading.tsx
├── lib/
│   ├── utils.ts
│   └── constants.ts
└── types/
    └── index.ts
```

### Step 2.5: Create Utility Functions

`src/lib/utils.ts`:
```typescript
import { type ClassValue, clsx } from 'clsx';
import { twMerge } from 'tailwind-merge';

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

---

## Phase 3: Implementation

### Step 3.1: Shared Components (Build These First)

#### AnimatedSection Component

`src/components/shared/AnimatedSection.tsx`:
```typescript
'use client';

import { motion } from 'motion/react';
import { useInView } from 'react-intersection-observer';
import { useRef } from 'react';

interface AnimatedSectionProps {
  children: React.ReactNode;
  className?: string;
  delay?: number;
  direction?: 'up' | 'down' | 'left' | 'right' | 'none';
}

export const AnimatedSection: React.FC<AnimatedSectionProps> = ({
  children,
  className = '',
  delay = 0,
  direction = 'up',
}) => {
  const ref = useRef(null);
  const isInView = useInView(ref, { once: true, threshold: 0.1 });

  const directionOffset = {
    up: { x: 0, y: 30 },
    down: { x: 0, y: -30 },
    left: { x: 30, y: 0 },
    right: { x: -30, y: 0 },
    none: { x: 0, y: 0 },
  };

  return (
    <motion.div
      ref={ref}
      initial={{ opacity: 0, ...directionOffset[direction] }}
      animate={isInView ? { opacity: 1, x: 0, y: 0 } : {}}
      transition={{ duration: 0.6, delay, ease: 'easeOut' }}
      style={{ willChange: isInView ? 'auto' : 'transform, opacity' }}
      className={className}
    >
      {children}
    </motion.div>
  );
};
```

#### Container Component

`src/components/shared/Container.tsx`:
```typescript
import { cn } from '@/lib/utils';

interface ContainerProps {
  children: React.ReactNode;
  className?: string;
  size?: 'sm' | 'md' | 'lg' | 'xl' | 'full';
}

const sizeClasses = {
  sm: 'max-w-3xl',
  md: 'max-w-5xl',
  lg: 'max-w-7xl',
  xl: 'max-w-[1400px]',
  full: 'max-w-full',
};

export const Container: React.FC<ContainerProps> = ({
  children,
  className,
  size = 'lg',
}) => {
  return (
    <div className={cn('mx-auto px-4 sm:px-6 lg:px-8', sizeClasses[size], className)}>
      {children}
    </div>
  );
};
```

#### SectionHeading Component

`src/components/shared/SectionHeading.tsx`:
```typescript
import { cn } from '@/lib/utils';
import { AnimatedSection } from './AnimatedSection';

interface SectionHeadingProps {
  title: string;
  subtitle?: string;
  align?: 'left' | 'center' | 'right';
  className?: string;
}

export const SectionHeading: React.FC<SectionHeadingProps> = ({
  title,
  subtitle,
  align = 'center',
  className,
}) => {
  const alignClasses = {
    left: 'text-left',
    center: 'text-center',
    right: 'text-right',
  };

  return (
    <AnimatedSection className={cn('mb-12 sm:mb-16', alignClasses[align], className)}>
      <h2 className="heading-2 mb-4">{title}</h2>
      {subtitle && (
        <p className="body-large text-gray-600 max-w-3xl mx-auto">
          {subtitle}
        </p>
      )}
    </AnimatedSection>
  );
};
```

### Step 3.2: Layout Components

#### Header Component

`src/components/layout/Header.tsx`:
```typescript
'use client';

import { useState, useEffect } from 'react';
import Link from 'next/link';
import { motion, AnimatePresence } from 'motion/react';
import { Menu, X } from 'lucide-react';
import { cn } from '@/lib/utils';

const navigation = [
  { name: 'Home', href: '#home' },
  { name: 'About', href: '#about' },
  { name: 'Services', href: '#services' },
  { name: 'Testimonials', href: '#testimonials' },
  { name: 'Contact', href: '#contact' },
];

export const Header: React.FC = () => {
  const [isScrolled, setIsScrolled] = useState(false);
  const [isMobileMenuOpen, setIsMobileMenuOpen] = useState(false);

  useEffect(() => {
    const handleScroll = () => {
      setIsScrolled(window.scrollY > 50);
    };

    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  return (
    <>
      <header
        className={cn(
          'fixed top-0 left-0 right-0 z-50 transition-all duration-300',
          isScrolled
            ? 'bg-white/95 backdrop-blur-md shadow-lg py-4'
            : 'bg-transparent py-6'
        )}
      >
        <div className="section-container py-0">
          <div className="flex items-center justify-between">
            <Link href="/" className="text-2xl font-bold text-primary">
              Logo
            </Link>

            <nav className="hidden md:flex items-center gap-8">
              {navigation.map((item) => (
                <a
                  key={item.name}
                  href={item.href}
                  className="text-foreground hover:text-primary transition-colors font-medium"
                >
                  {item.name}
                </a>
              ))}
              <button className="btn-primary">Get Started</button>
            </nav>

            <button
              onClick={() => setIsMobileMenuOpen(true)}
              className="md:hidden p-2"
              aria-label="Open menu"
            >
              <Menu className="w-6 h-6" />
            </button>
          </div>
        </div>
      </header>

      <AnimatePresence>
        {isMobileMenuOpen && (
          <>
            <motion.div
              initial={{ opacity: 0 }}
              animate={{ opacity: 1 }}
              exit={{ opacity: 0 }}
              className="fixed inset-0 bg-black/60 backdrop-blur-sm z-50"
              onClick={() => setIsMobileMenuOpen(false)}
            />
            <motion.div
              initial={{ x: '100%' }}
              animate={{ x: 0 }}
              exit={{ x: '100%' }}
              transition={{ type: 'spring', damping: 25, stiffness: 200 }}
              className="fixed inset-y-0 right-0 z-50 w-full sm:w-80 bg-white shadow-2xl"
            >
              <div className="flex items-center justify-between p-6 border-b">
                <span className="text-xl font-bold text-primary">Menu</span>
                <button
                  onClick={() => setIsMobileMenuOpen(false)}
                  aria-label="Close menu"
                >
                  <X className="w-6 h-6" />
                </button>
              </div>

              <nav className="flex flex-col gap-6 p-8">
                {navigation.map((item, index) => (
                  <motion.a
                    key={item.name}
                    href={item.href}
                    initial={{ opacity: 0, x: 20 }}
                    animate={{ opacity: 1, x: 0 }}
                    transition={{ delay: index * 0.1 }}
                    className="text-xl font-semibold hover:text-primary transition-colors"
                    onClick={() => setIsMobileMenuOpen(false)}
                  >
                    {item.name}
                  </motion.a>
                ))}
                <motion.button
                  initial={{ opacity: 0, x: 20 }}
                  animate={{ opacity: 1, x: 0 }}
                  transition={{ delay: navigation.length * 0.1 }}
                  className="btn-primary w-full"
                >
                  Get Started
                </motion.button>
              </nav>
            </motion.div>
          </>
        )}
      </AnimatePresence>
    </>
  );
};
```

#### Footer Component

`src/components/layout/Footer.tsx`:
```typescript
import Link from 'next/link';
import { Facebook, Twitter, Instagram, Linkedin } from 'lucide-react';

export const Footer: React.FC = () => {
  return (
    <footer className="bg-gray-900 text-white">
      <div className="section-container">
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8 lg:gap-12">
          <div>
            <h3 className="text-xl font-bold mb-4">Company Name</h3>
            <p className="text-gray-400 mb-4">
              Brief description of your company and what you do.
            </p>
            <div className="flex gap-4">
              <a href="#" className="hover:text-primary transition-colors" aria-label="Facebook">
                <Facebook className="w-5 h-5" />
              </a>
              <a href="#" className="hover:text-primary transition-colors" aria-label="Twitter">
                <Twitter className="w-5 h-5" />
              </a>
              <a href="#" className="hover:text-primary transition-colors" aria-label="Instagram">
                <Instagram className="w-5 h-5" />
              </a>
              <a href="#" className="hover:text-primary transition-colors" aria-label="LinkedIn">
                <Linkedin className="w-5 h-5" />
              </a>
            </div>
          </div>

          <div>
            <h3 className="text-lg font-semibold mb-4">Quick Links</h3>
            <ul className="space-y-2">
              <li>
                <a href="#about" className="text-gray-400 hover:text-white transition-colors">
                  About Us
                </a>
              </li>
              <li>
                <a href="#services" className="text-gray-400 hover:text-white transition-colors">
                  Services
                </a>
              </li>
              <li>
                <a href="#contact" className="text-gray-400 hover:text-white transition-colors">
                  Contact
                </a>
              </li>
            </ul>
          </div>

          <div>
            <h3 className="text-lg font-semibold mb-4">Services</h3>
            <ul className="space-y-2">
              <li className="text-gray-400">Service 1</li>
              <li className="text-gray-400">Service 2</li>
              <li className="text-gray-400">Service 3</li>
            </ul>
          </div>

          <div>
            <h3 className="text-lg font-semibold mb-4">Contact</h3>
            <ul className="space-y-2 text-gray-400">
              <li>123 Street Name</li>
              <li>City, State 12345</li>
              <li>
                <a href="tel:+1234567890" className="hover:text-white transition-colors">
                  (123) 456-7890
                </a>
              </li>
              <li>
                <a href="mailto:info@company.com" className="hover:text-white transition-colors">
                  info@company.com
                </a>
              </li>
            </ul>
          </div>
        </div>

        <div className="border-t border-gray-800 mt-12 pt-8 text-center text-gray-400 text-sm">
          <p>&copy; {new Date().getFullYear()} Company Name. All rights reserved.</p>
        </div>
      </div>
    </footer>
  );
};
```

### Step 3.3: Section Components

Build sections based on user's requirements. Each section follows this pattern:

```typescript
import { AnimatedSection } from '@/components/shared/AnimatedSection';
import { Container } from '@/components/shared/Container';
import { SectionHeading } from '@/components/shared/SectionHeading';

export const [SectionName]: React.FC = () => {
  return (
    <section id="section-id" className="py-12 sm:py-16 md:py-20 lg:py-24 bg-[BACKGROUND_COLOR]">
      <Container>
        <SectionHeading
          title="Section Title"
          subtitle="Optional subtitle describing this section"
        />

        <AnimatedSection delay={0.2}>
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 lg:gap-8">
            {/* Section content */}
          </div>
        </AnimatedSection>
      </Container>
    </section>
  );
};
```

### Step 3.4: Mobile-First Responsive Patterns

**Always follow this progression**:

1. **Mobile Base** (< 640px):
   ```css
   .card {
     @apply p-4 text-base;
   }
   ```

2. **Tablet** (≥ 640px):
   ```css
   @screen sm {
     .card {
       @apply p-6 text-lg;
     }
   }
   ```

3. **Desktop** (≥ 1024px):
   ```css
   @screen lg {
     .card {
       @apply p-8 text-xl;
     }
   }
   ```

**Critical Mobile Patterns**:
- Touch targets minimum 44x44px
- Font sizes: 16px → 18px → 20px
- Padding: 16px → 24px → 32px
- Use `hidden md:block` for desktop-only elements
- Use `block md:hidden` for mobile-only elements

### Step 3.5: Build Order

Follow this exact order to avoid rework:

1. ✅ Shared components (AnimatedSection, Container, SectionHeading)
2. ✅ Layout components (Header, Footer)
3. ✅ Hero section (most important, sets the tone)
4. ✅ Remaining sections in priority order
5. ✅ Contact form/CTA sections (conversion-critical)
6. ✅ Polish animations and transitions
7. ✅ Optimize images and assets

---

## Phase 4: Quality Assurance

### Step 4.1: Responsive Testing Checklist

Test at these exact widths:

- [ ] **375px** - iPhone SE (smallest common mobile)
- [ ] **414px** - iPhone Pro Max
- [ ] **768px** - iPad/Tablet
- [ ] **1024px** - Laptop
- [ ] **1920px** - Desktop

**What to verify at each breakpoint**:
- [ ] All text is readable (not too small)
- [ ] Buttons are clickable (minimum 44x44px)
- [ ] Images don't overflow or break layout
- [ ] Navigation works properly
- [ ] Forms are usable
- [ ] No horizontal scrollbars

### Step 4.2: Functionality Testing

- [ ] All internal links work (# anchors scroll smoothly)
- [ ] All external links open in new tab
- [ ] Forms validate inputs
- [ ] Forms submit successfully
- [ ] Error messages display correctly
- [ ] Success states show properly
- [ ] Loading states don't cause layout shift
- [ ] Mobile menu opens/closes smoothly
- [ ] Animations don't cause jank (60fps)

### Step 4.3: Accessibility Verification

- [ ] All images have alt text
- [ ] Buttons have aria-labels where needed
- [ ] Focus indicators visible on all interactive elements
- [ ] Keyboard navigation works (Tab, Enter, Escape)
- [ ] Color contrast meets WCAG AA (4.5:1 for text)
- [ ] Headings follow proper hierarchy (h1 → h2 → h3)
- [ ] Forms have proper labels

### Step 4.4: Performance Check

Run these commands before deployment:

```bash
# TypeScript check
npm run typecheck

# Build optimization
npm run build

# Check bundle size (should be < 200KB initial)
npm run build && ls -lh dist/assets/*.js

# Lighthouse audit (aim for 90+ score)
npx lighthouse https://your-site.com --view
```

**Performance Targets**:
- Initial load: < 200KB
- Largest Contentful Paint: < 2.5s
- First Input Delay: < 100ms
- Cumulative Layout Shift: < 0.1
- Lighthouse Performance Score: > 90

### Step 4.5: Content Review

- [ ] No placeholder text (no "Lorem ipsum")
- [ ] All company/contact info is correct
- [ ] Social media links point to correct profiles
- [ ] Email addresses are correct
- [ ] Phone numbers are properly formatted
- [ ] Copyright year is current
- [ ] All images have proper licensing

### Step 4.6: Pre-Launch Final Check

Run through this complete list before calling it done:

```typescript
interface PreLaunchChecklist {
  responsive: {
    mobile_375px: boolean;
    mobile_414px: boolean;
    tablet_768px: boolean;
    desktop_1024px: boolean;
    desktop_1920px: boolean;
  };
  functionality: {
    navigation_works: boolean;
    forms_submit: boolean;
    animations_smooth: boolean;
    links_valid: boolean;
  };
  accessibility: {
    keyboard_navigation: boolean;
    alt_text_present: boolean;
    color_contrast_wcag: boolean;
    aria_labels: boolean;
  };
  performance: {
    lighthouse_score: number; // > 90
    bundle_size_kb: number;   // < 200
    images_optimized: boolean;
  };
  content: {
    no_placeholders: boolean;
    contact_info_correct: boolean;
    social_links_work: boolean;
  };
}
```

---

## Critical Error Prevention

### Common Mistakes to AVOID

1. **Don't skip the discovery phase** - Gather ALL requirements first
2. **Don't hardcode content** - Use variables and constants
3. **Don't ignore mobile** - Design mobile-first, always
4. **Don't use index keys** - Use stable IDs for list items
5. **Don't inline styles** - Use Tailwind classes
6. **Don't forget loading states** - Add skeletons/spinners
7. **Don't skip error boundaries** - Catch errors gracefully
8. **Don't forget alt text** - Every image needs description
9. **Don't use !important** - Fix specificity issues properly
10. **Don't deploy without testing** - Run full QA checklist

### Mobile Layout Failures (Critical)

These cause the most mobile issues - avoid at all costs:

**Problem**: Fixed widths on mobile
```css
/* ❌ BAD */
.container {
  width: 1200px;
}

/* ✅ GOOD */
.container {
  @apply w-full max-w-7xl mx-auto px-4;
}
```

**Problem**: Tiny text on mobile
```css
/* ❌ BAD */
.heading {
  font-size: 12px; /* Same on all devices */
}

/* ✅ GOOD */
.heading {
  @apply text-2xl sm:text-3xl md:text-4xl lg:text-5xl;
}
```

**Problem**: Horizontal scroll
```css
/* ❌ BAD */
.grid {
  display: grid;
  grid-template-columns: repeat(4, 300px); /* Overflows on mobile */
}

/* ✅ GOOD */
.grid {
  @apply grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6;
}
```

---

## Example Usage

### Example Conversation Flow

**User**: "Build me a website for my consulting business"

**Assistant**: "I'd be happy to help build a consulting website! Let me gather some information first to ensure we build exactly what you need.

**Project Classification:**
1. This is a marketing site, correct?
2. How many pages approximately? (< 10, 10-50, or 50+)
3. What's the primary goal? Lead generation, bookings, information, or something else?

**Target Audience:**
4. Who are your ideal clients? (industry, seniority level, tech-savviness)
5. What's the main action you want visitors to take? (contact you, book a call, download something)

**Content:**
6. Do you have all your content ready (text, images, testimonials)?
7. Do you have brand guidelines? (logo, colors, fonts)

**Design Vibe:**
8. Which aesthetic fits your brand best? (minimal, professional, bold, elegant, modern)
9. What's your primary brand color?
10. Any secondary/accent colors?

**Features Needed:**
Which of these sections do you need?
- [ ] Hero with headline/CTA
- [ ] About/Story
- [ ] Services showcase
- [ ] Testimonials
- [ ] Portfolio/Case studies
- [ ] Pricing
- [ ] FAQ
- [ ] Blog
- [ ] Contact form
- [ ] Booking calendar
- [ ] Other?

**Technical:**
11. Need SEO optimization?
12. Expected traffic volume?
13. Any integrations needed? (CRM, email marketing, calendar)"

**User provides answers**

**Assistant**: "Perfect! Here's what I'm going to build:

## Project Summary
**Type**: Professional consulting marketing site
**Goal**: Lead generation through contact form and booking
**Vibe**: Professional + Trustworthy
**Colors**: Navy (#1E3A8A), Gold (#D4AF37), White
**Sections**: Hero, Services, Testimonials, About, Contact

**Tech Stack:**
- Next.js 16 (for SEO optimization)
- Tailwind CSS 4
- Motion library for smooth animations
- Responsive design (mobile-first)

I'll build this in the following order:
1. Set up project with design tokens
2. Create shared components
3. Build Header & Footer
4. Build Hero section
5. Build Services section
6. Build Testimonials section
7. Build About section
8. Build Contact form
9. Test responsive design
10. Run quality checks

Let me start building..."

**Assistant then builds the complete site following the exact framework above**

---

## Skill Maintenance

### When to Update This Skill

Update when:
- New versions of core libraries released (Next.js, React, Tailwind)
- New patterns emerge from production websites
- User feedback identifies missing features
- Accessibility standards change (WCAG updates)
- Performance best practices evolve

### Version History

- **v1.0.0** (2025-01-19): Initial release based on analysis of Endless Winning, WTA, and Freedom Path Wealth production websites

---

---

## Asset Resources & Quick Start Defaults (2025)

### Icon Libraries

**Recommended by Use Case:**

```typescript
const iconLibraries2025 = {
  // Primary choice - industry standard
  primary: {
    name: 'Lucide React',
    install: 'npm install lucide-react',
    url: 'https://lucide.dev',
    icons: '1000+',
    style: 'Consistent, minimal stroke',
    usage: `import { ArrowRight, CheckCircle } from 'lucide-react';`,
  },

  // Premium - used by Vercel, Shadcn
  premium: {
    name: 'Radix Icons',
    install: 'npm install @radix-ui/react-icons',
    url: 'https://icons.radix-ui.com',
    icons: '300+',
    style: 'Crisp 15x15 grid, perfect for UI',
    usage: `import { ArrowRightIcon } from '@radix-ui/react-icons';`,
  },

  // Versatile - 6 weights
  versatile: {
    name: 'Phosphor Icons',
    install: 'npm install @phosphor-icons/react',
    url: 'https://phosphoricons.com',
    icons: '1200+',
    style: '6 weights: thin, light, regular, bold, fill, duotone',
    usage: `import { Lightning } from '@phosphor-icons/react';`,
  },

  // Dashboard/Admin
  dashboard: {
    name: 'Tabler Icons',
    install: 'npm install @tabler/icons-react',
    url: 'https://tabler.io/icons',
    icons: '5000+',
    style: 'Comprehensive, dashboard-focused',
    usage: `import { IconDashboard } from '@tabler/icons-react';`,
  },

  // Brand/Social logos
  brands: {
    name: 'Simple Icons',
    install: 'npm install react-icons',
    url: 'https://simpleicons.org',
    usage: `import { SiFacebook, SiTwitter } from 'react-icons/si';`,
  },

  // Premium paid (2025 rising)
  paid: {
    name: 'Iconic',
    url: 'https://iconic.app',
    note: 'Premium animated + static, excellent for hero sections',
  },
};

// Size classes for consistency
const iconSizes = {
  xs: 'w-3 h-3',
  sm: 'w-4 h-4',
  md: 'w-5 h-5',
  lg: 'w-6 h-6',
  xl: 'w-8 h-8',
  '2xl': 'w-12 h-12',
};
```

### Stock Photography & Illustrations

**Free Stock Photo Sources:**

```typescript
const stockPhotoSources = {
  // Tier 1 - Best quality
  unsplash: {
    url: 'https://unsplash.com',
    api: 'https://api.unsplash.com', // 50 requests/hour free
    best_for: 'Hero backgrounds, lifestyle, nature',
    license: 'Free for commercial use',
  },

  pexels: {
    url: 'https://pexels.com',
    api: 'https://api.pexels.com',
    best_for: 'Business, people, technology',
    license: 'Free for commercial use',
  },

  // Tier 2 - Alternatives
  reshot: {
    url: 'https://www.reshot.com',
    best_for: 'Unique, less overused images',
    license: 'Free for commercial use',
  },

  // Premium (subscription)
  death_to_stock: {
    url: 'https://deathtothestockphoto.com',
    best_for: 'Authentic, non-stocky photos',
    license: 'Subscription based',
  },
};
```

**Avatar & People Solutions (2025):**

```typescript
const avatarSources = {
  // AI-generated faces - REPLACES UI Faces (deprecated)
  ai_faces: {
    name: 'Generated Photos',
    url: 'https://generated.photos',
    best_for: 'Realistic AI-generated faces',
    license: 'Free tier available',
  },

  // Random face API
  random_face: {
    url: 'https://thispersondoesnotexist.com',
    best_for: 'Quick placeholders',
    note: 'Refresh for new face',
  },

  // Code-based avatars
  dicebear: {
    name: 'Dicebear Avatars',
    install: 'npm install @dicebear/core @dicebear/collection',
    url: 'https://www.dicebear.com',
    best_for: 'Consistent placeholders, multiple styles',
    usage: `
import { createAvatar } from '@dicebear/core';
import { avataaars } from '@dicebear/collection';

const avatar = createAvatar(avataaars, {
  seed: 'John Doe',
});`,
  },

  // Illustrated people
  humaaans: {
    url: 'https://www.humaaans.com',
    best_for: 'Customizable illustrated people',
    license: 'Free for personal + commercial',
  },

  blush: {
    url: 'https://blush.design',
    best_for: 'Illustrated people, integrates with Figma',
  },

  // Simple letter avatars
  ui_avatars: {
    url: (name: string) => `https://ui-avatars.com/api/?name=${encodeURIComponent(name)}&background=random&size=200`,
    best_for: 'Quick text-based avatars',
  },
};
```

**Illustration Libraries:**

```typescript
const illustrationSources = {
  undraw: {
    url: 'https://undraw.co/illustrations',
    best_for: 'SVG illustrations, customizable colors',
    license: 'Free, open source',
  },

  storyset: {
    url: 'https://storyset.com',
    best_for: 'Animated illustrations',
    license: 'Free with attribution',
  },

  heropatterns: {
    url: 'https://heropatterns.com',
    best_for: 'SVG background patterns',
  },

  haikei: {
    url: 'https://haikei.app',
    best_for: 'SVG background generators (blobs, waves)',
  },
};
```

### Font Pairing Recommendations (2025 Meta)

**Premium Pairings - The 2025 Standard:**

```css
/* SaaS / Tech Startup - THE 2025 META */
/* Satoshi (heading) + Inter (body) */
/* Source: https://www.fontshare.com/fonts/satoshi */
@font-face {
  font-family: 'Satoshi';
  src: url('/fonts/Satoshi-Variable.woff2') format('woff2');
  font-weight: 400 900;
  font-display: swap;
}
/* Satoshi is free from Fontshare - download and self-host */

/* Alternative SaaS pairing */
/* General Sans + Inter */
/* Source: https://www.fontshare.com/fonts/general-sans */

/* Premium / Luxury / Finance */
/* Clash Display (heading) + Neue Montreal (body) */
/* Both from: https://www.fontshare.com */

/* Creative / Agency */
/* Cabinet Grotesk + Switzer */
/* Source: https://www.fontshare.com */
```

**Free Google Fonts Alternatives:**

```css
/* If you can't self-host, use these Google Font alternatives */

/* Modern Tech (Satoshi alternative) */
@import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap');
/* Plus Jakarta Sans - closest to Satoshi on Google Fonts */

/* Professional / Corporate */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Source+Serif+4:wght@400;600&display=swap');
/* Source Serif 4 (heading) + Inter (body) */

/* Friendly / Approachable */
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&display=swap');
/* DM Sans - versatile, works for both heading and body */

/* Bold / Energetic */
@import url('https://fonts.googleapis.com/css2?family=Outfit:wght@400;500;600;700;800&display=swap');
/* Outfit - modern, geometric, great for fitness/energy */

/* Minimal / Clean */
@import url('https://fonts.googleapis.com/css2?family=Geist:wght@400;500;600;700&display=swap');
/* Geist - Vercel's font, very 2025 */
```

**Free Premium Alternatives (Self-hosted):**

```typescript
const fontSources2025 = {
  // Best free fonts source
  fontshare: {
    url: 'https://www.fontshare.com',
    recommended: ['Satoshi', 'General Sans', 'Clash Display', 'Switzer', 'Cabinet Grotesk'],
    license: 'Free for personal + commercial',
  },

  // GitHub-hosted alternatives
  mona_sans: {
    url: 'https://github.com/github/mona-sans',
    best_for: 'Neue Montreal alternative (free)',
  },

  hubot_sans: {
    url: 'https://github.com/github/hubot-sans',
    best_for: 'Technical/developer sites',
  },
};
```

**Font Configuration in Tailwind CSS 4:**

```css
@theme inline {
  /* 2025 SaaS Standard */
  --font-heading: 'Satoshi', 'Plus Jakarta Sans', system-ui, sans-serif;
  --font-sans: 'Inter', system-ui, sans-serif;

  /* Or for luxury/finance */
  --font-heading: 'Clash Display', Georgia, serif;
  --font-sans: 'Neue Montreal', 'Mona Sans', system-ui, sans-serif;
}
```

### Logo Placeholder Solutions

**Logo APIs (2025):**

```typescript
const logoAPIs = {
  // Generate SVG logos on the fly
  logo_dev: {
    url: 'https://logo.dev/api/',
    best_for: 'Generate company logos from domain',
    usage: 'https://img.logo.dev/google.com?token=YOUR_TOKEN',
    note: 'Free tier available',
  },

  // Fetch existing company logos
  clearbit: {
    url: 'https://logo.clearbit.com/',
    usage: 'https://logo.clearbit.com/stripe.com',
    best_for: 'Fetching known company logos',
    note: 'No API key needed',
  },

  // Brand icons
  simple_icons: {
    install: 'npm install simple-icons',
    url: 'https://simpleicons.org',
    best_for: 'Brand/tech company logos as SVGs',
  },
};
```

**Custom Logo Components:**

1. **Text-Based Logo** (Recommended for MVP):
```typescript
export const TextLogo: React.FC<{ name: string; className?: string }> = ({
  name,
  className
}) => (
  <span className={cn(
    'font-heading font-bold text-2xl bg-gradient-to-r from-primary to-secondary bg-clip-text text-transparent',
    className
  )}>
    {name}
  </span>
);
```

2. **Icon + Text Logo**:
```typescript
import { Zap, Crown, Rocket, Sparkles } from 'lucide-react';

export const IconLogo: React.FC<{ name: string; icon?: string }> = ({
  name,
  icon = 'sparkles'
}) => {
  const icons = { zap: Zap, crown: Crown, rocket: Rocket, sparkles: Sparkles };
  const Icon = icons[icon as keyof typeof icons] || Sparkles;

  return (
    <div className="flex items-center gap-2">
      <div className="w-8 h-8 rounded-lg bg-gradient-to-br from-primary to-secondary flex items-center justify-center">
        <Icon className="w-5 h-5 text-white" />
      </div>
      <span className="font-heading font-bold text-xl">{name}</span>
    </div>
  );
};
```

3. **Monogram Logo**:
```typescript
export const MonogramLogo: React.FC<{ initials: string }> = ({ initials }) => (
  <div className="w-10 h-10 rounded-full bg-gradient-to-br from-primary to-secondary flex items-center justify-center">
    <span className="text-white font-bold text-lg">{initials}</span>
  </div>
);
```

4. **AI Logo Generation** (if user wants actual logo):
```typescript
const logoGenerators = {
  free: [
    'https://hatchful.shopify.com',     // Shopify's free logo maker
    'https://www.canva.com/create/logos/', // Free tier
  ],
  paid: [
    'https://looka.com',      // AI-generated, ~$20
    'https://brandmark.io',   // AI-generated, ~$25
  ],
};
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

### UI Component Libraries & Boilerplates

**Tailwind Component Libraries (2025):**

```typescript
const componentLibraries = {
  // Premium - hot new library
  magic_ui: {
    url: 'https://magicui.design',
    best_for: 'Animated components, landing pages',
    note: 'React + Tailwind + Framer Motion',
  },

  // Free - marketing focused
  hyper_ui: {
    url: 'https://www.hyperui.dev',
    best_for: 'Marketing components, e-commerce',
    license: 'Free, open source',
  },

  // Free - very complete
  preline: {
    url: 'https://preline.co',
    best_for: 'Full UI kit, dashboards',
    license: 'Free + pro options',
  },

  // Premium - industry standard
  tailwind_ui: {
    url: 'https://tailwindui.com',
    best_for: 'Official Tailwind templates',
    license: 'Paid ($299 one-time)',
  },
};
```

**GitHub Boilerplates (2025):**

```typescript
const boilerplates = [
  {
    name: 'Next.js Boilerplate',
    url: 'https://github.com/ixartz/Next-js-Boilerplate',
    stars: '8k+',
    includes: 'TypeScript, Tailwind, ESLint, testing',
  },
  {
    name: 'Taxonomy',
    url: 'https://github.com/shadcn/taxonomy',
    stars: '18k+',
    includes: 'Shadcn reference implementation',
  },
  {
    name: 'HyperUI',
    url: 'https://github.com/markmead/hyperui',
    includes: 'Marketing component collection',
  },
  {
    name: 'Lovable Components',
    url: 'https://github.com/michael-andreuzza/lovable-components',
    note: '2025 rising star, beautiful defaults',
  },
  {
    name: 'Create T3 App',
    url: 'https://create.t3.gg',
    includes: 'Full-stack TypeScript starter',
  },
];
```

### Placeholder Content Sources

```typescript
const contentSources = {
  // Lorem ipsum alternatives
  hipsum: 'https://hipsum.co',              // Hipster ipsum
  bacon: 'https://baconipsum.com',          // Meat-themed
  office: 'https://officeipsum.com',        // Office jargon

  // Realistic fake data
  faker: {
    install: 'npm install @faker-js/faker',
    usage: `
import { faker } from '@faker-js/faker';

const testimonial = {
  name: faker.person.fullName(),
  company: faker.company.name(),
  quote: faker.lorem.paragraph(),
};`,
  },

  // JSON placeholder API
  jsonplaceholder: {
    url: 'https://jsonplaceholder.typicode.com',
    best_for: 'Fake REST API for prototyping',
  },
};
```

---

## Industry-Specific Defaults

### Quick-Start Configurations

When user says "build me a website for my [industry]", apply these defaults:

```typescript
const industryDefaults = {
  tech_startup: {
    aesthetic: 'modern',
    primaryColor: '#6366F1', // Indigo
    secondaryColor: '#8B5CF6', // Violet
    accentColor: '#06B6D4', // Cyan
    fonts: {
      heading: 'Satoshi',        // 2025 meta - or Plus Jakarta Sans (Google)
      body: 'Inter',
    },
    traits: ['innovative', 'bold', 'cutting-edge'],
    sections: ['hero', 'features', 'how-it-works', 'pricing', 'faq', 'cta'],
    cta: 'Start Free Trial',
    images: 'technology, abstract, gradients',
  },

  consulting: {
    aesthetic: 'professional',
    primaryColor: '#1E3A8A', // Navy
    secondaryColor: '#3B82F6', // Blue
    accentColor: '#D4AF37', // Gold
    fonts: {
      heading: 'Source Serif 4',
      body: 'Inter',
    },
    traits: ['trustworthy', 'professional', 'reliable'],
    sections: ['hero', 'services', 'about', 'testimonials', 'case-studies', 'contact'],
    cta: 'Schedule Consultation',
    images: 'business, office, professionals',
  },

  fitness_coaching: {
    aesthetic: 'bold',
    primaryColor: '#DC2626', // Red
    secondaryColor: '#F97316', // Orange
    accentColor: '#FBBF24', // Yellow
    fonts: {
      heading: 'Outfit',         // 2025 - modern, geometric
      body: 'Inter',
    },
    traits: ['energetic', 'motivating', 'bold'],
    sections: ['hero', 'programs', 'transformation', 'testimonials', 'about', 'pricing', 'contact'],
    cta: 'Start Your Transformation',
    images: 'fitness, athletes, gym',
  },

  healthcare: {
    aesthetic: 'minimal',
    primaryColor: '#0D9488', // Teal
    secondaryColor: '#06B6D4', // Cyan
    accentColor: '#10B981', // Emerald
    fonts: {
      heading: 'DM Sans',
      body: 'DM Sans',
    },
    traits: ['trustworthy', 'calm', 'professional'],
    sections: ['hero', 'services', 'team', 'testimonials', 'faq', 'contact'],
    cta: 'Book Appointment',
    images: 'healthcare, wellness, nature',
  },

  creative_agency: {
    aesthetic: 'playful',
    primaryColor: '#EC4899', // Pink
    secondaryColor: '#8B5CF6', // Violet
    accentColor: '#FBBF24', // Yellow
    fonts: {
      heading: 'Cabinet Grotesk', // 2025 - or General Sans
      body: 'Switzer',            // 2025 - or Inter
    },
    traits: ['creative', 'bold', 'innovative'],
    sections: ['hero', 'portfolio', 'services', 'process', 'team', 'contact'],
    cta: 'Start a Project',
    images: 'creative, art, design',
  },

  financial_services: {
    aesthetic: 'elegant',
    primaryColor: '#1E3A8A', // Navy
    secondaryColor: '#059669', // Green
    accentColor: '#D4AF37', // Gold
    fonts: {
      heading: 'Clash Display',  // 2025 - premium/luxury
      body: 'Mona Sans',         // 2025 - or Neue Montreal
    },
    traits: ['trustworthy', 'professional', 'reliable'],
    sections: ['hero', 'services', 'why-us', 'testimonials', 'team', 'contact'],
    cta: 'Get Free Assessment',
    images: 'finance, success, professional',
  },

  ecommerce: {
    aesthetic: 'modern',
    primaryColor: '#000000', // Black
    secondaryColor: '#6B7280', // Gray
    accentColor: '#F59E0B', // Amber
    fonts: {
      heading: 'Satoshi',        // 2025 - clean, modern
      body: 'Inter',
    },
    traits: ['clean', 'modern', 'trustworthy'],
    sections: ['hero', 'featured-products', 'categories', 'testimonials', 'newsletter'],
    cta: 'Shop Now',
    images: 'products, lifestyle, minimal',
  },

  restaurant: {
    aesthetic: 'elegant',
    primaryColor: '#B91C1C', // Deep Red
    secondaryColor: '#78350F', // Brown
    accentColor: '#D4AF37', // Gold
    fonts: {
      heading: 'Clash Display',  // 2025 - elegant display
      body: 'DM Sans',
    },
    traits: ['warm', 'inviting', 'sophisticated'],
    sections: ['hero', 'menu-highlights', 'about', 'gallery', 'reservations', 'contact'],
    cta: 'Make Reservation',
    images: 'food, restaurant, ambiance',
  },
};
```

**Usage in Discovery:**
```typescript
// When user mentions their industry
if (userIndustry) {
  const defaults = industryDefaults[userIndustry];
  // Pre-fill discovery form with these defaults
  // Ask: "I'll use these as a starting point - [show defaults]. Want to adjust anything?"
}
```

---

## Complete Section Templates

### Hero Section (with placeholder content)

```typescript
'use client';

import { motion } from 'motion/react';
import { ArrowRight, Play } from 'lucide-react';
import { AnimatedSection } from '@/components/shared/AnimatedSection';

interface HeroProps {
  headline?: string;
  subheadline?: string;
  primaryCta?: string;
  secondaryCta?: string;
  backgroundImage?: string;
}

export const Hero: React.FC<HeroProps> = ({
  headline = "Transform Your Business with Expert Solutions",
  subheadline = "We help ambitious companies achieve extraordinary results through proven strategies and dedicated partnership.",
  primaryCta = "Get Started",
  secondaryCta = "Watch Demo",
  backgroundImage,
}) => {
  return (
    <section id="home" className="relative min-h-screen flex items-center overflow-hidden">
      {/* Background */}
      <div className="absolute inset-0 bg-gradient-to-br from-primary/5 via-background to-secondary/5" />

      {/* Optional background image */}
      {backgroundImage && (
        <div
          className="absolute inset-0 opacity-10"
          style={{
            backgroundImage: `url(${backgroundImage})`,
            backgroundSize: 'cover',
            backgroundPosition: 'center',
          }}
        />
      )}

      <div className="relative section-container">
        <div className="grid lg:grid-cols-2 gap-12 lg:gap-16 items-center">
          {/* Content */}
          <AnimatedSection className="text-center lg:text-left">
            <motion.span
              initial={{ opacity: 0, y: 20 }}
              animate={{ opacity: 1, y: 0 }}
              className="inline-block px-4 py-2 bg-primary/10 text-primary rounded-full text-sm font-semibold mb-6"
            >
              Welcome to [Company Name]
            </motion.span>

            <h1 className="heading-1 mb-6">
              {headline.split(' ').map((word, i) => (
                <motion.span
                  key={i}
                  initial={{ opacity: 0, y: 20 }}
                  animate={{ opacity: 1, y: 0 }}
                  transition={{ delay: i * 0.1 }}
                  className={i === Math.floor(headline.split(' ').length / 2) ? 'text-primary' : ''}
                >
                  {word}{' '}
                </motion.span>
              ))}
            </h1>

            <motion.p
              initial={{ opacity: 0, y: 20 }}
              animate={{ opacity: 1, y: 0 }}
              transition={{ delay: 0.4 }}
              className="body-large text-gray-600 mb-8 max-w-xl mx-auto lg:mx-0"
            >
              {subheadline}
            </motion.p>

            <motion.div
              initial={{ opacity: 0, y: 20 }}
              animate={{ opacity: 1, y: 0 }}
              transition={{ delay: 0.5 }}
              className="flex flex-col sm:flex-row gap-4 justify-center lg:justify-start"
            >
              <button className="btn-primary">
                {primaryCta}
                <ArrowRight className="w-5 h-5" />
              </button>
              <button className="btn-secondary">
                <Play className="w-5 h-5" />
                {secondaryCta}
              </button>
            </motion.div>

            {/* Trust indicators */}
            <motion.div
              initial={{ opacity: 0 }}
              animate={{ opacity: 1 }}
              transition={{ delay: 0.7 }}
              className="mt-12 pt-8 border-t border-gray-200"
            >
              <p className="text-sm text-gray-500 mb-4">Trusted by leading companies</p>
              <div className="flex flex-wrap items-center justify-center lg:justify-start gap-8 opacity-50">
                {/* Replace with actual logos */}
                {['Company 1', 'Company 2', 'Company 3', 'Company 4'].map((company) => (
                  <span key={company} className="font-bold text-gray-400">{company}</span>
                ))}
              </div>
            </motion.div>
          </AnimatedSection>

          {/* Visual */}
          <AnimatedSection delay={0.3} direction="right" className="hidden lg:block">
            <div className="relative">
              <div className="absolute -inset-4 bg-gradient-to-r from-primary/20 to-secondary/20 rounded-3xl blur-2xl" />
              <img
                src="https://images.unsplash.com/photo-1551434678-e076c223a692?w=800&h=600&fit=crop"
                alt="Hero visual"
                className="relative rounded-2xl shadow-2xl w-full"
              />
            </div>
          </AnimatedSection>
        </div>
      </div>
    </section>
  );
};
```

### Testimonials Section (with placeholder content)

```typescript
'use client';

import { Star, Quote } from 'lucide-react';
import { AnimatedSection } from '@/components/shared/AnimatedSection';
import { Container } from '@/components/shared/Container';
import { SectionHeading } from '@/components/shared/SectionHeading';

interface Testimonial {
  id: string;
  name: string;
  role: string;
  company: string;
  content: string;
  rating: number;
  avatar: string;
}

const defaultTestimonials: Testimonial[] = [
  {
    id: '1',
    name: 'Sarah Johnson',
    role: 'CEO',
    company: 'TechStart Inc',
    content: 'Working with this team transformed our business. We saw a 300% increase in leads within the first quarter. Their strategic approach and attention to detail is unmatched.',
    rating: 5,
    avatar: 'https://randomuser.me/api/portraits/women/44.jpg',
  },
  {
    id: '2',
    name: 'Michael Chen',
    role: 'Founder',
    company: 'Growth Labs',
    content: 'The results speak for themselves. Professional, responsive, and truly invested in our success. I recommend them to everyone looking to scale their business.',
    rating: 5,
    avatar: 'https://randomuser.me/api/portraits/men/32.jpg',
  },
  {
    id: '3',
    name: 'Emily Rodriguez',
    role: 'Marketing Director',
    company: 'Innovate Co',
    content: 'From strategy to execution, everything was flawless. They understood our vision immediately and delivered beyond our expectations. A true partner in growth.',
    rating: 5,
    avatar: 'https://randomuser.me/api/portraits/women/68.jpg',
  },
];

interface TestimonialsProps {
  testimonials?: Testimonial[];
  title?: string;
  subtitle?: string;
}

export const Testimonials: React.FC<TestimonialsProps> = ({
  testimonials = defaultTestimonials,
  title = "What Our Clients Say",
  subtitle = "Don't just take our word for it. Here's what our clients have to say about working with us.",
}) => {
  return (
    <section id="testimonials" className="py-12 sm:py-16 md:py-20 lg:py-24 bg-muted">
      <Container>
        <SectionHeading title={title} subtitle={subtitle} />

        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 lg:gap-8">
          {testimonials.map((testimonial, index) => (
            <AnimatedSection key={testimonial.id} delay={index * 0.1}>
              <div className="bg-white rounded-2xl p-6 sm:p-8 shadow-lg h-full flex flex-col">
                {/* Rating */}
                <div className="flex gap-1 mb-4">
                  {[...Array(testimonial.rating)].map((_, i) => (
                    <Star key={i} className="w-5 h-5 fill-yellow-400 text-yellow-400" />
                  ))}
                </div>

                {/* Quote */}
                <div className="relative flex-1 mb-6">
                  <Quote className="absolute -top-2 -left-2 w-8 h-8 text-primary/20" />
                  <p className="text-gray-600 leading-relaxed pl-6">
                    {testimonial.content}
                  </p>
                </div>

                {/* Author */}
                <div className="flex items-center gap-4 pt-6 border-t border-gray-100">
                  <img
                    src={testimonial.avatar}
                    alt={testimonial.name}
                    className="w-12 h-12 rounded-full object-cover"
                  />
                  <div>
                    <p className="font-semibold text-foreground">{testimonial.name}</p>
                    <p className="text-sm text-gray-500">
                      {testimonial.role}, {testimonial.company}
                    </p>
                  </div>
                </div>
              </div>
            </AnimatedSection>
          ))}
        </div>
      </Container>
    </section>
  );
};
```

### Services/Features Section (with placeholder content)

```typescript
'use client';

import {
  Rocket, Target, Zap, Shield,
  TrendingUp, Users, CheckCircle, ArrowRight
} from 'lucide-react';
import { AnimatedSection } from '@/components/shared/AnimatedSection';
import { Container } from '@/components/shared/Container';
import { SectionHeading } from '@/components/shared/SectionHeading';

interface Service {
  id: string;
  icon: React.ElementType;
  title: string;
  description: string;
  features: string[];
}

const defaultServices: Service[] = [
  {
    id: '1',
    icon: Rocket,
    title: 'Growth Strategy',
    description: 'Accelerate your business growth with data-driven strategies tailored to your unique goals.',
    features: ['Market Analysis', 'Competitive Research', 'Growth Roadmap'],
  },
  {
    id: '2',
    icon: Target,
    title: 'Digital Marketing',
    description: 'Reach your ideal customers with targeted campaigns that deliver measurable results.',
    features: ['SEO Optimization', 'Paid Advertising', 'Content Strategy'],
  },
  {
    id: '3',
    icon: Zap,
    title: 'Brand Development',
    description: 'Build a memorable brand that resonates with your audience and stands out from competition.',
    features: ['Visual Identity', 'Brand Messaging', 'Style Guidelines'],
  },
  {
    id: '4',
    icon: Shield,
    title: 'Technology Solutions',
    description: 'Leverage cutting-edge technology to streamline operations and enhance customer experience.',
    features: ['Web Development', 'App Development', 'System Integration'],
  },
  {
    id: '5',
    icon: TrendingUp,
    title: 'Analytics & Insights',
    description: 'Make informed decisions with comprehensive analytics and actionable insights.',
    features: ['Performance Tracking', 'User Behavior', 'ROI Analysis'],
  },
  {
    id: '6',
    icon: Users,
    title: 'Team Training',
    description: 'Empower your team with the skills and knowledge to drive sustainable growth.',
    features: ['Workshops', 'Ongoing Support', 'Best Practices'],
  },
];

interface ServicesProps {
  services?: Service[];
  title?: string;
  subtitle?: string;
}

export const Services: React.FC<ServicesProps> = ({
  services = defaultServices,
  title = "Our Services",
  subtitle = "Comprehensive solutions designed to help your business thrive in today's competitive landscape.",
}) => {
  return (
    <section id="services" className="py-12 sm:py-16 md:py-20 lg:py-24">
      <Container>
        <SectionHeading title={title} subtitle={subtitle} />

        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 lg:gap-8">
          {services.map((service, index) => {
            const Icon = service.icon;
            return (
              <AnimatedSection key={service.id} delay={index * 0.1}>
                <div className="group bg-white rounded-2xl p-6 sm:p-8 shadow-lg hover:shadow-xl transition-all duration-300 h-full flex flex-col border border-transparent hover:border-primary/20">
                  {/* Icon */}
                  <div className="w-14 h-14 rounded-xl bg-gradient-to-br from-primary to-secondary flex items-center justify-center mb-6 group-hover:scale-110 transition-transform">
                    <Icon className="w-7 h-7 text-white" />
                  </div>

                  {/* Content */}
                  <h3 className="text-xl font-bold mb-3">{service.title}</h3>
                  <p className="text-gray-600 mb-6 flex-1">{service.description}</p>

                  {/* Features */}
                  <ul className="space-y-2 mb-6">
                    {service.features.map((feature) => (
                      <li key={feature} className="flex items-center gap-2 text-sm text-gray-600">
                        <CheckCircle className="w-4 h-4 text-green-500 flex-shrink-0" />
                        {feature}
                      </li>
                    ))}
                  </ul>

                  {/* CTA */}
                  <a
                    href="#contact"
                    className="inline-flex items-center gap-2 text-primary font-semibold group-hover:gap-3 transition-all"
                  >
                    Learn More
                    <ArrowRight className="w-4 h-4" />
                  </a>
                </div>
              </AnimatedSection>
            );
          })}
        </div>
      </Container>
    </section>
  );
};
```

### Pricing Section (with placeholder content)

```typescript
'use client';

import { Check, X } from 'lucide-react';
import { AnimatedSection } from '@/components/shared/AnimatedSection';
import { Container } from '@/components/shared/Container';
import { SectionHeading } from '@/components/shared/SectionHeading';
import { cn } from '@/lib/utils';

interface PricingTier {
  id: string;
  name: string;
  description: string;
  price: string;
  period: string;
  features: { text: string; included: boolean }[];
  cta: string;
  popular?: boolean;
}

const defaultTiers: PricingTier[] = [
  {
    id: 'starter',
    name: 'Starter',
    description: 'Perfect for small businesses just getting started',
    price: '$49',
    period: '/month',
    features: [
      { text: 'Up to 5 team members', included: true },
      { text: 'Basic analytics', included: true },
      { text: 'Email support', included: true },
      { text: '1GB storage', included: true },
      { text: 'Advanced features', included: false },
      { text: 'Priority support', included: false },
    ],
    cta: 'Get Started',
  },
  {
    id: 'professional',
    name: 'Professional',
    description: 'Best for growing teams that need more power',
    price: '$99',
    period: '/month',
    features: [
      { text: 'Up to 20 team members', included: true },
      { text: 'Advanced analytics', included: true },
      { text: 'Priority email support', included: true },
      { text: '10GB storage', included: true },
      { text: 'Advanced features', included: true },
      { text: '24/7 phone support', included: false },
    ],
    cta: 'Get Started',
    popular: true,
  },
  {
    id: 'enterprise',
    name: 'Enterprise',
    description: 'For large organizations with custom needs',
    price: '$249',
    period: '/month',
    features: [
      { text: 'Unlimited team members', included: true },
      { text: 'Custom analytics', included: true },
      { text: '24/7 phone & email support', included: true },
      { text: 'Unlimited storage', included: true },
      { text: 'All advanced features', included: true },
      { text: 'Dedicated account manager', included: true },
    ],
    cta: 'Contact Sales',
  },
];

interface PricingProps {
  tiers?: PricingTier[];
  title?: string;
  subtitle?: string;
}

export const Pricing: React.FC<PricingProps> = ({
  tiers = defaultTiers,
  title = "Simple, Transparent Pricing",
  subtitle = "Choose the plan that best fits your needs. All plans include a 14-day free trial.",
}) => {
  return (
    <section id="pricing" className="py-12 sm:py-16 md:py-20 lg:py-24">
      <Container>
        <SectionHeading title={title} subtitle={subtitle} />

        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 lg:gap-8">
          {tiers.map((tier, index) => (
            <AnimatedSection key={tier.id} delay={index * 0.1}>
              <div className={cn(
                'relative bg-white rounded-2xl p-6 sm:p-8 shadow-lg h-full flex flex-col',
                tier.popular && 'ring-2 ring-primary'
              )}>
                {tier.popular && (
                  <span className="absolute -top-4 left-1/2 -translate-x-1/2 px-4 py-1 bg-primary text-white text-sm font-semibold rounded-full">
                    Most Popular
                  </span>
                )}

                {/* Header */}
                <div className="text-center mb-6">
                  <h3 className="text-xl font-bold mb-2">{tier.name}</h3>
                  <p className="text-gray-600 text-sm mb-4">{tier.description}</p>
                  <div className="flex items-baseline justify-center gap-1">
                    <span className="text-4xl font-bold">{tier.price}</span>
                    <span className="text-gray-500">{tier.period}</span>
                  </div>
                </div>

                {/* Features */}
                <ul className="space-y-3 mb-8 flex-1">
                  {tier.features.map((feature) => (
                    <li key={feature.text} className="flex items-center gap-3">
                      {feature.included ? (
                        <Check className="w-5 h-5 text-green-500 flex-shrink-0" />
                      ) : (
                        <X className="w-5 h-5 text-gray-300 flex-shrink-0" />
                      )}
                      <span className={cn(
                        'text-sm',
                        feature.included ? 'text-gray-600' : 'text-gray-400'
                      )}>
                        {feature.text}
                      </span>
                    </li>
                  ))}
                </ul>

                {/* CTA */}
                <button className={cn(
                  'w-full py-3 rounded-lg font-semibold transition-all',
                  tier.popular
                    ? 'bg-primary text-white hover:bg-primary/90'
                    : 'bg-gray-100 text-foreground hover:bg-gray-200'
                )}>
                  {tier.cta}
                </button>
              </div>
            </AnimatedSection>
          ))}
        </div>
      </Container>
    </section>
  );
};
```

### FAQ Section (with placeholder content)

```typescript
'use client';

import { useState } from 'react';
import { ChevronDown } from 'lucide-react';
import { motion, AnimatePresence } from 'motion/react';
import { AnimatedSection } from '@/components/shared/AnimatedSection';
import { Container } from '@/components/shared/Container';
import { SectionHeading } from '@/components/shared/SectionHeading';
import { cn } from '@/lib/utils';

interface FAQItem {
  id: string;
  question: string;
  answer: string;
}

const defaultFaqs: FAQItem[] = [
  {
    id: '1',
    question: 'How long does it take to see results?',
    answer: 'Most clients start seeing measurable results within the first 30-60 days. However, this can vary based on your specific goals, industry, and starting point. We provide regular progress reports so you can track improvements throughout our engagement.',
  },
  {
    id: '2',
    question: 'What makes your approach different?',
    answer: 'We combine data-driven strategies with creative solutions tailored specifically to your business. Unlike one-size-fits-all approaches, we take time to understand your unique challenges, goals, and target audience before developing a customized plan.',
  },
  {
    id: '3',
    question: 'Do you offer ongoing support?',
    answer: 'Yes! All our packages include ongoing support. We believe in building long-term partnerships with our clients. Whether you need help with implementation, have questions, or want to scale your strategy, we are here to help.',
  },
  {
    id: '4',
    question: 'What is your pricing model?',
    answer: 'We offer flexible pricing options including project-based, retainer, and hourly arrangements. During our initial consultation, we will discuss your needs and recommend the most cost-effective option for your situation.',
  },
  {
    id: '5',
    question: 'How do we get started?',
    answer: 'Getting started is easy! Simply click the "Get Started" button or contact us to schedule a free consultation. During this call, we will discuss your goals, answer any questions, and outline potential strategies for your business.',
  },
];

interface FAQProps {
  faqs?: FAQItem[];
  title?: string;
  subtitle?: string;
}

export const FAQ: React.FC<FAQProps> = ({
  faqs = defaultFaqs,
  title = "Frequently Asked Questions",
  subtitle = "Find answers to common questions about our services and approach.",
}) => {
  const [openId, setOpenId] = useState<string | null>(null);

  return (
    <section id="faq" className="py-12 sm:py-16 md:py-20 lg:py-24 bg-muted">
      <Container size="md">
        <SectionHeading title={title} subtitle={subtitle} />

        <div className="space-y-4">
          {faqs.map((faq, index) => (
            <AnimatedSection key={faq.id} delay={index * 0.1}>
              <div className="bg-white rounded-xl overflow-hidden shadow-sm">
                <button
                  onClick={() => setOpenId(openId === faq.id ? null : faq.id)}
                  className="w-full flex items-center justify-between p-6 text-left hover:bg-gray-50 transition-colors"
                >
                  <span className="font-semibold pr-8">{faq.question}</span>
                  <ChevronDown className={cn(
                    'w-5 h-5 text-primary flex-shrink-0 transition-transform',
                    openId === faq.id && 'rotate-180'
                  )} />
                </button>

                <AnimatePresence>
                  {openId === faq.id && (
                    <motion.div
                      initial={{ height: 0 }}
                      animate={{ height: 'auto' }}
                      exit={{ height: 0 }}
                      transition={{ duration: 0.3 }}
                      className="overflow-hidden"
                    >
                      <div className="px-6 pb-6 text-gray-600 leading-relaxed">
                        {faq.answer}
                      </div>
                    </motion.div>
                  )}
                </AnimatePresence>
              </div>
            </AnimatedSection>
          ))}
        </div>
      </Container>
    </section>
  );
};
```

---

## References

Patterns in this skill are derived from:
- Endless Winning (Next.js 16 marketing site)
- WTA (Vite React enterprise application)
- Freedom Path Wealth (Next.js 16 financial advisor site)

All code templates are battle-tested in production environments.
