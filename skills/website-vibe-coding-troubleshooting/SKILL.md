---
skill_name: website-vibe-coding-troubleshooting
description: Debug, optimize, and deploy websites built with website-vibe-coding skill. Fixes ESLint errors, animation performance, SSR issues, and handles production deployment.
version: 1.0.0
author: MaWoo Development
tags: [debugging, eslint, deployment, performance, nextjs, react, troubleshooting]
related_skills: [website-vibe-coding]
---

# Website Vibe Coding - Troubleshooting & Deployment

## Purpose

This skill handles debugging, optimization, and deployment for websites built using the `website-vibe-coding` skill. It fixes common production issues including ESLint errors, animation performance problems, SSR/client-side rendering conflicts, and manages the complete deployment workflow.

## When to Activate This Skill

Activate when:
- "Fix ESLint errors in the website"
- "Website animations are janky/laggy"
- "Getting 'window is not defined' errors"
- "Deploy the website to Vercel"
- "Build is failing with TypeScript/ESLint errors"
- "Layout is shifting when animations run"
- "Need to optimize website performance"

**Do NOT activate for**:
- Initial website development (use `website-vibe-coding`)
- Adding new features (use `website-vibe-coding`)
- Design changes without technical issues

## Activation Pattern

This skill should be invoked:
1. **After** building a website with `website-vibe-coding`
2. **Before** deploying to production
3. **When** encountering build/runtime errors
4. **When** performance issues are identified

---

## Phase 1: Code Quality & Linting

### Step 1.1: Run ESLint Check

Always start by identifying all linting issues:

```bash
npm run lint
```

### Step 1.2: Common ESLint Errors & Fixes

#### Error 1: React Hooks - setState in useEffect

**ESLint Error**:
```
React Hook useEffect has a missing dependency: 'setIsClient'.
Either include it or remove the dependency array.
```

**Problem Code** (❌ BAD - Causes cascading renders):
```typescript
const [isClient, setIsClient] = useState(false);

useEffect(() => {
  setIsClient(true);
}, []);
```

**Why It's Bad**:
- Creates unnecessary re-render cycle
- ESLint flags missing dependency
- Can cause hydration mismatches

**Solution** (✅ GOOD - Lazy initialization):
```typescript
// Option 1: Lazy initialization (preferred)
const [isClient] = useState(() => typeof window !== 'undefined');

// Option 2: useEffect with proper dependency (if needed)
const [isClient, setIsClient] = useState(false);

useEffect(() => {
  setIsClient(true);
}, []); // Disable ESLint for this specific case with comment
// eslint-disable-next-line react-hooks/exhaustive-deps
```

**Best Practice**: Use lazy initialization when initial value can be computed immediately.

#### Error 2: Unescaped Entities in JSX

**ESLint Error**:
```
`'` can be escaped with `&apos;`, `&lsquo;`, `&#39;`, `&rsquo;`.
```

**Problem Code** (❌ BAD):
```typescript
<p>Don't worry, we'll help you succeed!</p>
<h2>Here's what we offer</h2>
<p>"Premium" service with "guaranteed" results</p>
```

**Solution** (✅ GOOD):
```typescript
<p>Don&apos;t worry, we&apos;ll help you succeed!</p>
<h2>Here&apos;s what we offer</h2>
<p>&ldquo;Premium&rdquo; service with &ldquo;guaranteed&rdquo; results</p>

// Or use HTML entities reference:
// &apos;  → '  (apostrophe)
// &ldquo; → "  (left double quote)
// &rdquo; → "  (right double quote)
// &lsquo; → '  (left single quote)
// &rsquo; → '  (right single quote)
// &mdash; → —  (em dash)
// &ndash; → –  (en dash)
```

**Quick Reference Table**:
| Character | Entity | Example |
|-----------|--------|---------|
| ' | `&apos;` | Don&apos;t |
| " | `&ldquo;` `&rdquo;` | &ldquo;Quote&rdquo; |
| — | `&mdash;` | Best&mdash;ever |
| – | `&ndash;` | Pages 1&ndash;10 |

#### Error 3: TypeScript `any` Types

**ESLint Error**:
```
Unexpected any. Specify a different type.
```

**Problem Code** (❌ BAD):
```typescript
const handleDragEnd = (event: any, info: any) => {
  console.log(info.velocity.x);
};

const handleClick = (e: any) => {
  e.preventDefault();
};
```

**Solution** (✅ GOOD):
```typescript
// Use specific types
const handleDragEnd = (
  _event: unknown,
  info: { velocity: { x: number }; offset: { x: number } }
) => {
  console.log(info.velocity.x);
};

// For events, use React's built-in types
const handleClick = (e: React.MouseEvent<HTMLButtonElement>) => {
  e.preventDefault();
};

// If you truly don't need the parameter, prefix with underscore
const handleScroll = (_e: Event) => {
  // Indicates intentionally unused
};
```

**Common Event Types**:
```typescript
React.MouseEvent<HTMLButtonElement>    // Button clicks
React.FormEvent<HTMLFormElement>       // Form submissions
React.ChangeEvent<HTMLInputElement>    // Input changes
React.KeyboardEvent<HTMLInputElement>  // Keyboard events
React.FocusEvent<HTMLInputElement>     // Focus events
```

#### Error 4: Missing Dependencies in useEffect

**ESLint Error**:
```
React Hook useEffect has missing dependencies: 'isMobile' and 'setCurrentSlide'.
Either include them or remove the dependency array.
```

**Problem Code** (❌ BAD):
```typescript
useEffect(() => {
  const interval = setInterval(() => {
    if (!isMobile) {
      setCurrentSlide((prev) => (prev + 1) % testimonials.length);
    }
  }, 5000);

  return () => clearInterval(interval);
}, []); // Missing dependencies!
```

**Solution Options**:

**Option 1** (✅ Add dependencies):
```typescript
useEffect(() => {
  const interval = setInterval(() => {
    if (!isMobile) {
      setCurrentSlide((prev) => (prev + 1) % testimonials.length);
    }
  }, 5000);

  return () => clearInterval(interval);
}, [isMobile, testimonials.length]); // Dependencies included
```

**Option 2** (✅ Use callback form of setState):
```typescript
useEffect(() => {
  const interval = setInterval(() => {
    if (!isMobile) {
      // Callback form doesn't require setCurrentSlide in deps
      setCurrentSlide((prev) => (prev + 1) % testimonials.length);
    }
  }, 5000);

  return () => clearInterval(interval);
}, [isMobile, testimonials.length]);
```

**Option 3** (✅ Disable ESLint with justification):
```typescript
useEffect(() => {
  const interval = setInterval(() => {
    if (!isMobile) {
      setCurrentSlide((prev) => (prev + 1) % testimonials.length);
    }
  }, 5000);

  return () => clearInterval(interval);
  // Only runs on mount - we want the interval to use initial isMobile value
  // eslint-disable-next-line react-hooks/exhaustive-deps
}, []);
```

**When to Disable ESLint**:
- Only when you're certain the dependency should NOT trigger re-runs
- Always add a comment explaining WHY
- Use sparingly - usually adding the dependency is correct

### Step 1.3: Fix All Linting Errors

**Process**:
1. Run `npm run lint` to see all errors
2. Fix errors one by one using patterns above
3. Re-run `npm run lint` to verify fixes
4. Repeat until no errors remain

**DO NOT** deploy with linting errors - they often indicate real bugs.

---

## Phase 2: Animation Performance & Layout Optimization

### Step 2.1: Identify Animation Issues

**Common Symptoms**:
- Page content "jumps" when animations start
- Cumulative Layout Shift (CLS) warnings in Lighthouse
- Animations feel janky or stuttery
- Content height changes during transitions

### Step 2.2: Fix Layout Shift in Animations

**Problem**: Content changing size during animation causes page jitter

#### Issue: Testimonials Carousel Layout Shift

**Problem Code** (❌ BAD - Causes layout shift):
```typescript
<AnimatePresence mode="wait">
  <motion.div key={currentSlide} className="relative">
    <div className="bg-white p-8 rounded-lg">
      {/* Variable height content - causes jitter */}
      <p className="text-gray-600 mb-6">{testimonials[currentSlide].text}</p>
      <div className="flex items-center gap-4">
        {/* Author info */}
      </div>
    </div>
  </motion.div>
</AnimatePresence>
```

**Why It Fails**:
- No fixed height container
- Content size varies between testimonials
- Causes Cumulative Layout Shift (CLS)
- Page "bounces" during transitions

**Solution** (✅ GOOD - Fixed height, no shift):
```typescript
<div className="relative w-full max-w-[800px] mx-auto min-h-[500px] sm:min-h-[450px]">
  <AnimatePresence mode="wait">
    <motion.div
      key={currentSlide}
      initial={{ opacity: 0, x: 100 }}
      animate={{ opacity: 1, x: 0 }}
      exit={{ opacity: 0, x: -100 }}
      transition={{ duration: 0.5, ease: 'easeInOut' }}
      className="w-full absolute inset-0"  // Absolute positioning is KEY
    >
      <div className="bg-white h-full flex flex-col items-center justify-center p-8 rounded-lg shadow-lg">
        {/* Content centered, fixed height container */}
        <p className="text-gray-600 text-center mb-6">
          {testimonials[currentSlide].text}
        </p>
        <div className="flex items-center gap-4">
          {/* Author info */}
        </div>
      </div>
    </motion.div>
  </AnimatePresence>
</div>
```

**Key Principles for Smooth Animations**:

1. **Fixed Height Container**:
   ```css
   min-h-[500px] sm:min-h-[450px]
   ```
   - Prevents container from collapsing
   - Provides predictable dimensions
   - Adjust based on longest content

2. **Absolute Positioning**:
   ```css
   absolute inset-0
   ```
   - Takes animated content out of normal flow
   - Prevents layout reflow
   - Essential for preventing CLS

3. **Flexbox Centering**:
   ```css
   flex flex-col items-center justify-center
   ```
   - Centers content vertically and horizontally
   - Works with variable content heights
   - Maintains visual stability

4. **Full Height Child**:
   ```css
   h-full
   ```
   - Ensures child fills container
   - Maintains consistent height
   - Prevents collapse

**Before/After Comparison**:

| Aspect | Before (Bad) | After (Good) |
|--------|-------------|--------------|
| CLS Score | 0.25+ (Poor) | 0.00 (Excellent) |
| Layout Shift | Visible jitter | Smooth transition |
| Container Height | Variable | Fixed (min-h) |
| Positioning | Relative (in-flow) | Absolute (out-of-flow) |
| User Experience | Jarring | Professional |

### Step 2.3: GPU Acceleration for Smooth Animations

**Problem**: Animations running on CPU cause jank

**Solution** (✅ Use GPU-accelerated properties):
```typescript
<motion.div
  animate={{
    opacity: 1,           // ✅ GPU accelerated
    transform: 'translateY(0)',  // ✅ GPU accelerated
    x: 0,                 // ✅ GPU accelerated (Motion shorthand)
    y: 0,                 // ✅ GPU accelerated (Motion shorthand)
  }}
  style={{
    willChange: isInView ? 'auto' : 'transform, opacity',
    transform: 'translateZ(0)',  // Force GPU layer
  }}
>
```

**GPU-Accelerated Properties** (USE THESE):
- ✅ `transform` (translate, rotate, scale)
- ✅ `opacity`
- ✅ Motion library's `x`, `y`, `scale`, `rotate`

**CPU-Heavy Properties** (AVOID ANIMATING):
- ❌ `width`, `height`
- ❌ `top`, `left`, `right`, `bottom`
- ❌ `margin`, `padding`
- ❌ `font-size`

**Performance Tip**: Use `transform: scale()` instead of animating width/height:
```typescript
// ❌ BAD - CPU heavy
animate={{ width: 200, height: 300 }}

// ✅ GOOD - GPU accelerated
animate={{ scale: 1.2 }}
```

---

## Phase 3: SSR & Client-Side Rendering Issues

### Step 3.1: Common SSR Errors

#### Error: "window is not defined"

**Problem**: Accessing browser APIs during server-side rendering

**Problem Code** (❌ BAD):
```typescript
export default function Component() {
  const [isMobile, setIsMobile] = useState(window.innerWidth < 768); // ❌ Crashes on SSR

  return <div>...</div>;
}
```

**Solution Pattern 1** (✅ Lazy Initialization):
```typescript
'use client';

export default function Component() {
  // ✅ Lazy initialization - runs only once on mount
  const [isClient] = useState(() => typeof window !== 'undefined');
  const [isMobile, setIsMobile] = useState(() => {
    if (typeof window !== 'undefined') {
      return window.innerWidth < 768;
    }
    return false; // Default value for SSR
  });

  return (
    <>
      {isClient && isMobile && <MobileOnlyContent />}
      {isClient && !isMobile && <DesktopOnlyContent />}
    </>
  );
}
```

**Solution Pattern 2** (✅ Separate useEffect):
```typescript
'use client';

export default function Component() {
  const [isClient, setIsClient] = useState(false);
  const [isMobile, setIsMobile] = useState(false);

  // ✅ Runs only on client after hydration
  useEffect(() => {
    setIsClient(true);
    setIsMobile(window.innerWidth < 768);
  }, []);

  // ✅ Separate effect for window listeners
  useEffect(() => {
    if (!isClient) return;

    const handleResize = () => {
      setIsMobile(window.innerWidth < 768);
    };

    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  }, [isClient]);

  return (
    <>
      {isClient && isMobile && <MobileOnlyContent />}
      {isClient && !isMobile && <DesktopOnlyContent />}
    </>
  );
}
```

**Solution Pattern 3** (✅ Dynamic Import):
```typescript
import dynamic from 'next/dynamic';

// ✅ Only loads on client side
const ClientOnlyComponent = dynamic(() => import('./ClientOnlyComponent'), {
  ssr: false,
  loading: () => <div>Loading...</div>,
});

export default function Page() {
  return <ClientOnlyComponent />;
}
```

### Step 3.2: Hydration Mismatch Errors

**Problem**: Server HTML doesn't match client HTML

**Error Message**:
```
Warning: Text content did not match. Server: "..." Client: "..."
```

**Common Causes**:
1. Using `Date.now()` or random values during render
2. Browser-specific APIs in JSX
3. Conditional rendering based on `window`

**Solution Pattern**:
```typescript
'use client';

export default function Component() {
  const [mounted, setMounted] = useState(false);

  useEffect(() => {
    setMounted(true);
  }, []);

  // ✅ Return same content during SSR and initial client render
  if (!mounted) {
    return <div>Loading...</div>; // Matches SSR output
  }

  // ✅ Now safe to use client-only features
  return (
    <div>
      Current time: {new Date().toLocaleTimeString()}
    </div>
  );
}
```

---

## Phase 4: TypeScript & Build Errors

### Step 4.1: Run TypeScript Check

```bash
npm run typecheck
# or
npx tsc --noEmit
```

### Step 4.2: Common TypeScript Fixes

#### Error: Property does not exist on type

**Problem Code** (❌ BAD):
```typescript
const testimonials = [...];
<p>{testimonials[currentSlide].text}</p> // Error: 'text' doesn't exist
```

**Solution** (✅ Define interface):
```typescript
interface Testimonial {
  id: number;
  text: string;
  author: string;
  role: string;
  image?: string;
}

const testimonials: Testimonial[] = [
  { id: 1, text: "Great service!", author: "John Doe", role: "CEO" },
  // ...
];
```

#### Error: Type 'string | undefined' not assignable

**Problem Code** (❌ BAD):
```typescript
const name: string = formData.name; // Error: could be undefined
```

**Solution Options**:
```typescript
// Option 1: Optional chaining with fallback
const name: string = formData.name ?? '';

// Option 2: Type narrowing
const name: string = formData.name || 'Anonymous';

// Option 3: Non-null assertion (only if you're certain)
const name: string = formData.name!;
```

---

## Phase 5: Performance Optimization

### Step 5.1: Run Production Build

```bash
npm run build
```

**Analyze output**:
```
Route (app)                              Size     First Load JS
┌ ○ /                                    15.2 kB        105 kB
├ ○ /_not-found                          0 B             0 B
└ ○ /api/contact                         0 B             0 B

First Load JS shared by all:             89.8 kB
  ├ chunks/framework-abc123.js           45.2 kB
  ├ chunks/main-def456.js               31.5 kB
  └ other shared chunks                 13.1 kB
```

**Performance Targets**:
- ✅ First Load JS: < 200KB (Excellent)
- ⚠️ First Load JS: 200-300KB (Acceptable)
- ❌ First Load JS: > 300KB (Needs optimization)

### Step 5.2: Optimize Bundle Size

**If bundle is too large**:

1. **Add dynamic imports** for heavy components:
   ```typescript
   const HeavyComponent = dynamic(() => import('./HeavyComponent'), {
     loading: () => <Skeleton />,
   });
   ```

2. **Check for duplicate dependencies**:
   ```bash
   npx webpack-bundle-analyzer
   ```

3. **Use Next.js Image component**:
   ```typescript
   import Image from 'next/image';

   <Image
     src="/hero.jpg"
     width={1920}
     height={1080}
     quality={85}
     priority  // For LCP
   />
   ```

### Step 5.3: Lighthouse Audit

```bash
npm run build
npm run start
# In another terminal:
npx lighthouse http://localhost:3000 --view
```

**Target Scores**:
- Performance: > 90
- Accessibility: > 95
- Best Practices: > 90
- SEO: > 90

**Common Issues & Fixes**:

| Issue | Fix |
|-------|-----|
| Low Performance | Add lazy loading, optimize images |
| Low Accessibility | Add alt text, ARIA labels, focus indicators |
| Low Best Practices | Fix console errors, use HTTPS |
| Low SEO | Add meta tags, semantic HTML |

---

## Phase 6: Deployment Workflow

### Step 6.1: Pre-Deployment Checklist

**CRITICAL**: Run ALL of these before deploying:

```bash
# 1. Fix all linting errors
npm run lint

# 2. Fix all TypeScript errors
npm run typecheck

# 3. Verify production build succeeds
npm run build

# 4. Test production build locally
npm run start
# Visit http://localhost:3000 and test all pages

# 5. Check for console errors in browser DevTools
```

**DO NOT PROCEED** if any of these fail.

### Step 6.2: Git Workflow

**Commit all changes** with descriptive message:

```bash
# Check what's changed
git status

# Review changes
git diff

# Add all changes
git add .

# Commit with clear message
git commit -m "feat: implement [feature name] with responsive design

- Added mobile-first responsive layouts
- Fixed ESLint errors (React hooks, unescaped entities)
- Optimized animations to prevent layout shift
- Added accessibility improvements (alt text, ARIA labels)
- Verified TypeScript compilation and production build"

# Push to GitHub
git push origin main
```

**Commit Message Format**:
```
<type>: <subject>

<body>

Examples:
- feat: add contact form with validation
- fix: resolve layout shift in testimonials carousel
- perf: optimize image loading with Next.js Image
- style: improve mobile navigation animations
- docs: update README with deployment instructions
```

### Step 6.3: Vercel Deployment

#### Automatic Deployment (Recommended)

**Setup** (one-time):
1. Go to [vercel.com](https://vercel.com)
2. Click "Add New Project"
3. Import your GitHub repository
4. Configure:
   - Framework Preset: Next.js (auto-detected)
   - Root Directory: `./` (or specify if nested)
   - Build Command: `npm run build`
   - Output Directory: `.next` (default)
5. Click "Deploy"

**Subsequent Deployments**:
- Vercel auto-deploys when you push to GitHub
- Check deployment status at `https://vercel.com/[username]/[project]`
- Production URL: `https://[project-name].vercel.app`

#### Manual Deployment (Fallback)

If auto-deploy fails or isn't configured:

```bash
# Install Vercel CLI if not installed
npm i -g vercel

# Login to Vercel
vercel login

# Deploy to production
vercel --prod

# Follow prompts to configure project
```

### Step 6.4: Deployment Troubleshooting

#### Issue 1: Deployment Not Triggering

**Symptoms**: Pushed to GitHub but no Vercel deployment starts

**Diagnosis**:
1. Check Vercel dashboard → Settings → Git
2. Verify repository is connected
3. Check branch is set to `main` (or your default branch)

**Solution**:
```bash
# Option 1: Trigger manual deployment from Vercel dashboard
# Click "Deployments" → "Redeploy" → "Use existing Build Cache"

# Option 2: Use Vercel CLI
vercel --prod

# Option 3: Re-connect Git integration
# Vercel dashboard → Settings → Git → Disconnect → Reconnect
```

#### Issue 2: Build Fails on Vercel (But Works Locally)

**Symptoms**: Local `npm run build` succeeds, Vercel build fails

**Common Causes**:

**A) Node.js Version Mismatch**

Check Vercel build logs for Node version, then:

```json
// package.json
{
  "engines": {
    "node": ">=18.0.0"
  }
}
```

Or set in Vercel dashboard → Settings → Environment Variables:
```
NODE_VERSION=18
```

**B) Missing Environment Variables**

If your app uses environment variables:

1. Go to Vercel dashboard → Settings → Environment Variables
2. Add all required variables (e.g., `NEXT_PUBLIC_API_URL`)
3. Redeploy

**C) Dependencies in Wrong Section**

```json
// ❌ BAD - Build will fail
{
  "devDependencies": {
    "@types/react": "^18.0.0",  // Needed for build!
    "tailwindcss": "^4.0.0"     // Needed for build!
  }
}

// ✅ GOOD - Move to dependencies
{
  "dependencies": {
    "@types/react": "^18.0.0",
    "tailwindcss": "^4.0.0",
    "react": "^19.0.0",
    "next": "^16.0.0"
  },
  "devDependencies": {
    "eslint": "^8.0.0"  // Only dev tools here
  }
}
```

**D) ESLint/TypeScript Errors**

Vercel treats warnings as errors by default.

**Quick fix** (not recommended for production):
```json
// next.config.js
module.exports = {
  eslint: {
    ignoreDuringBuilds: true,  // ⚠️ Only use temporarily
  },
  typescript: {
    ignoreBuildErrors: true,   // ⚠️ Only use temporarily
  },
}
```

**Proper fix**: Fix all ESLint and TypeScript errors locally first.

#### Issue 3: SSL Certificate Pending

**Symptoms**: Site deployed but shows SSL error

**Solution**:
- Wait 5-10 minutes for SSL provisioning
- Verify domain DNS settings are correct
- Check Vercel dashboard → Domains → SSL status

#### Issue 4: 404 on Custom Routes

**Symptoms**: Homepage works but `/about` returns 404

**Cause**: Client-side routing not configured

**Solution**: Vercel handles Next.js routing automatically. If using static export:
```javascript
// next.config.js
module.exports = {
  output: 'export',  // Only for static hosting
  trailingSlash: true,
}
```

### Step 6.5: Post-Deployment Verification

After successful deployment:

**1. Visit Production URL**
```
https://[project-name].vercel.app
```

**2. Test Critical Paths**:
- [ ] Homepage loads
- [ ] Mobile menu works
- [ ] Contact form submits
- [ ] All images load
- [ ] Animations are smooth
- [ ] No console errors (check DevTools)

**3. Test Responsive Breakpoints**:
- [ ] 375px (iPhone SE)
- [ ] 768px (Tablet)
- [ ] 1024px (Desktop)

**4. Run Lighthouse Audit on Production**:
```bash
npx lighthouse https://[project-name].vercel.app --view
```

**5. Check Analytics** (if configured):
- Vercel Analytics
- Google Analytics
- Vercel Speed Insights

---

## Phase 7: Common Production Issues

### Issue 1: Fonts Not Loading

**Symptoms**: Fonts show as fallback on production

**Solution** (Next.js Font Optimization):
```typescript
// app/layout.tsx
import { Inter, Playfair_Display } from 'next/font/google';

const inter = Inter({
  subsets: ['latin'],
  variable: '--font-sans',
});

const playfair = Playfair_Display({
  subsets: ['latin'],
  variable: '--font-serif',
});

export default function RootLayout({ children }) {
  return (
    <html lang="en" className={`${inter.variable} ${playfair.variable}`}>
      <body>{children}</body>
    </html>
  );
}
```

### Issue 2: Images Not Optimized

**Symptoms**: Slow page load, large Lighthouse warnings

**Solution**:
```typescript
// ❌ BAD
<img src="/hero.jpg" alt="Hero" />

// ✅ GOOD - Next.js Image component
import Image from 'next/image';

<Image
  src="/hero.jpg"
  alt="Hero image"
  width={1920}
  height={1080}
  priority  // For above-fold images (LCP)
  quality={85}
  placeholder="blur"
  blurDataURL="data:image/jpeg;base64,..."
/>

// For below-fold images
<Image
  src="/feature.jpg"
  alt="Feature"
  width={800}
  height={600}
  loading="lazy"  // Default behavior
  quality={75}
/>
```

### Issue 3: Environment Variables Not Working

**Symptoms**: API calls fail, features don't work in production

**Solution**:

**Client-side variables** (must start with `NEXT_PUBLIC_`):
```bash
# .env.local
NEXT_PUBLIC_API_URL=https://api.example.com
NEXT_PUBLIC_GA_ID=G-XXXXXXXXXX
```

**Server-side variables** (no prefix needed):
```bash
# .env.local
DATABASE_URL=postgresql://...
API_SECRET=secret_key_here
```

**Vercel Configuration**:
1. Dashboard → Settings → Environment Variables
2. Add each variable
3. Select environments (Production, Preview, Development)
4. Redeploy for changes to take effect

### Issue 4: 500 Internal Server Error

**Symptoms**: API routes return 500 errors

**Diagnosis**:
```bash
# Check Vercel function logs
vercel logs [deployment-url]

# Or view in dashboard:
# Deployments → [Latest] → Functions → [function-name] → Logs
```

**Common Causes**:
- Missing environment variables
- Database connection errors
- Unhandled exceptions in API routes
- Timeout (10s limit on Hobby plan, 60s on Pro)

**Solution Pattern**:
```typescript
// app/api/contact/route.ts
export async function POST(request: Request) {
  try {
    const body = await request.json();

    // Validate input
    if (!body.email || !body.name) {
      return Response.json(
        { error: 'Missing required fields' },
        { status: 400 }
      );
    }

    // Process request
    // ...

    return Response.json({ success: true });

  } catch (error) {
    console.error('Contact form error:', error);
    return Response.json(
      { error: 'Internal server error' },
      { status: 500 }
    );
  }
}
```

---

## Phase 8: Performance Monitoring

### Step 8.1: Enable Vercel Analytics

```bash
npm install @vercel/analytics
```

```typescript
// app/layout.tsx
import { Analytics } from '@vercel/analytics/react';

export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        {children}
        <Analytics />
      </body>
    </html>
  );
}
```

### Step 8.2: Monitor Core Web Vitals

**Target Metrics**:
- **LCP** (Largest Contentful Paint): < 2.5s
- **FID** (First Input Delay): < 100ms
- **CLS** (Cumulative Layout Shift): < 0.1

**View in Vercel Dashboard**:
- Analytics → Core Web Vitals
- Speed Insights (if enabled)

### Step 8.3: Set Up Error Tracking

**Option 1: Vercel Error Tracking** (Built-in)
- Dashboard → Deployments → [Latest] → Functions → Errors

**Option 2: Sentry** (Recommended for production):
```bash
npm install @sentry/nextjs
npx @sentry/wizard@latest -i nextjs
```

---

## Troubleshooting Checklist

Before asking for help, verify:

**Build Issues**:
- [ ] `npm run lint` passes with no errors
- [ ] `npm run typecheck` passes with no errors
- [ ] `npm run build` completes successfully
- [ ] All dependencies are in correct section (dependencies vs devDependencies)
- [ ] Node.js version matches between local and Vercel

**Runtime Issues**:
- [ ] No `window is not defined` errors (check SSR patterns)
- [ ] No hydration mismatch warnings
- [ ] All environment variables set in Vercel dashboard
- [ ] API routes have proper error handling
- [ ] Images use Next.js Image component

**Performance Issues**:
- [ ] Animations use fixed-height containers
- [ ] Animated elements use `absolute` positioning
- [ ] Only animating `transform` and `opacity`
- [ ] Images are optimized (WebP/AVIF)
- [ ] Heavy components use dynamic imports

**Deployment Issues**:
- [ ] Git repository connected to Vercel
- [ ] Correct branch selected for auto-deploy
- [ ] Build logs checked for specific errors
- [ ] Environment variables configured
- [ ] SSL certificate provisioned (wait 5-10 min)

---

## Quick Reference

### ESLint Fixes
```typescript
// React hooks
const [state] = useState(() => initialValue);

// Unescaped entities
<p>Don&apos;t use raw apostrophes</p>

// TypeScript any
const handler = (e: React.MouseEvent<HTMLButtonElement>) => {}

// Dependencies
useEffect(() => {}, [dep1, dep2]); // Include all deps
```

### Animation Performance
```typescript
// Fixed container
<div className="min-h-[500px] relative">
  <motion.div className="absolute inset-0 flex justify-center items-center h-full">
    {content}
  </motion.div>
</div>
```

### SSR Safe Patterns
```typescript
// Lazy init
const [isClient] = useState(() => typeof window !== 'undefined');

// useEffect
useEffect(() => {
  setIsClient(true);
}, []);

// Dynamic import
const Component = dynamic(() => import('./Component'), { ssr: false });
```

### Deployment Commands
```bash
npm run lint && npm run typecheck && npm run build
git add . && git commit -m "feat: description" && git push
vercel --prod  # Manual deployment
```

---

## Integration with Main Skill

This skill should be used:
1. **After** completing website with `website-vibe-coding`
2. **Before** final deployment to production
3. **When** encountering any errors during development

**Typical Workflow**:
```
website-vibe-coding (build)
  ↓
website-vibe-coding-troubleshooting (debug & optimize)
  ↓
website-vibe-coding-troubleshooting (deploy)
  ↓
Production website ✅
```

---

## Version History

- **v1.0.0** (2025-01-19): Initial release
  - ESLint error patterns from Endless Winning fixes
  - Animation performance optimizations
  - SSR/hydration issue solutions
  - Complete deployment workflow
  - Production troubleshooting guide
