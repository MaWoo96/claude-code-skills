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

## References

Patterns in this skill are derived from:
- Endless Winning (Next.js 16 marketing site)
- WTA (Vite React enterprise application)
- Freedom Path Wealth (Next.js 16 financial advisor site)

All code templates are battle-tested in production environments.
