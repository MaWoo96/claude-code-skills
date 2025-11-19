# Claude Code Skills

A collection of production-tested Claude Code skills for web development workflows.

## Skills Included

### website-vibe-coding
**Purpose**: Build production-quality marketing/business websites from scratch with minimal iteration.

**When to use**:
- Starting a new marketing or business website
- Building landing pages, portfolios, or promotional sites
- Need comprehensive discovery-to-deployment workflow

**Key features**:
- 19-question discovery phase
- Technology stack selection (Next.js vs Vite)
- Design token configuration
- Shared component patterns (AnimatedSection, Container, SectionHeading)
- Mobile-first responsive design
- Quality assurance checklist

### website-vibe-coding-troubleshooting
**Purpose**: Debug, optimize, and deploy websites built with the website-vibe-coding skill.

**When to use**:
- ESLint errors blocking build
- Animation performance issues (layout shift, jank)
- SSR/hydration mismatches
- TypeScript compilation errors
- Deployment to Vercel

**Key features**:
- ESLint error patterns and fixes
- Animation performance optimization (CLS prevention)
- SSR/client-side rendering patterns
- Deployment workflow with troubleshooting
- Performance monitoring setup

## Tech Stack Covered

- **Frameworks**: Next.js 14+, Vite
- **UI Libraries**: React 19, Tailwind CSS 4, shadcn/ui, Radix UI
- **Animation**: Framer Motion / Motion library
- **State**: TanStack Query, React hooks
- **Database**: Supabase (PostgreSQL)
- **Deployment**: Vercel

## Installation

### Option 1: Clone entire repository
```bash
# Clone to your .claude-plugin directory
git clone https://github.com/MaWoo96/claude-code-skills.git ~/.claude-plugin/skills-repo

# Symlink skills you want
ln -s ~/.claude-plugin/skills-repo/skills/website-vibe-coding ~/.claude-plugin/skills/website-vibe-coding
ln -s ~/.claude-plugin/skills-repo/skills/website-vibe-coding-troubleshooting ~/.claude-plugin/skills/website-vibe-coding-troubleshooting
```

### Option 2: Copy individual skills
```bash
# Copy specific skill to your skills directory
cp -r skills/website-vibe-coding ~/.claude-plugin/skills/
cp -r skills/website-vibe-coding-troubleshooting ~/.claude-plugin/skills/
```

## Usage

The skills activate automatically based on context. You can also invoke them explicitly:

```
Use the website-vibe-coding skill to build a landing page for [project description]
```

```
Use the website-vibe-coding-troubleshooting skill to fix ESLint errors in my build
```

## Projects Built With These Skills

- **Endless Winning** - Sports performance coaching website
- **WTA (Winners Take All)** - Community platform
- **Freedom Path Wealth** - Financial services landing page

## Contributing

These skills are based on real production patterns from multiple website builds. Contributions welcome!

1. Fork the repository
2. Create a feature branch
3. Test your changes with real projects
4. Submit a pull request

## License

MIT License - Feel free to use, modify, and distribute.

## Author

Matt Wood ([@MaWoo96](https://github.com/MaWoo96))

---

Built with Claude Code
