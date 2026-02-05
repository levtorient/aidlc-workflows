---
name: frontend-engineer
description: Create distinctive, production-grade frontend interfaces with high design quality. Use this skill when the user asks to build web components, pages, artifacts, posters, or applications (examples include websites, landing pages, dashboards, React components, HTML/CSS layouts, or when styling/beautifying any web UI). Generates creative, polished code and UI design that avoids generic AI aesthetics.
license: Complete terms in LICENSE.txt
---

This skill guides creation of distinctive, production-grade frontend interfaces that avoid generic "AI slop" aesthetics. Implement real working code with exceptional attention to aesthetic details and creative choices.

The user provides frontend requirements: a component, page, section, or interface to build. Always read `requirements.md` at the project root and the existing codebase before implementing — derive all structure, sections, and interactions from the actual requirements.

## Design Phase (Required Before Implementation)

**MANDATORY**: Before writing any code, create a `page_design.md` file in the project root (or appropriate design folder) that documents the wireframe and design decisions.

### Step 1: Design Thinking

Understand the context and commit to a BOLD aesthetic direction:
- **Purpose**: What problem does this interface solve? Who uses it?
- **Tone**: Pick an extreme: brutally minimal, maximalist chaos, retro-futuristic, organic/natural, luxury/refined, playful/toy-like, editorial/magazine, brutalist/raw, art deco/geometric, soft/pastel, industrial/utilitarian, etc. There are so many flavors to choose from. Use these for inspiration but design one that is true to the aesthetic direction.
- **Constraints**: Technical requirements (framework, performance, accessibility).
- **Differentiation**: What makes this UNFORGETTABLE? What's the one thing someone will remember?

**CRITICAL**: Choose a clear conceptual direction and execute it with precision. Bold maximalism and refined minimalism both work — the key is intentionality, not intensity.

### Step 2: Create `page_design.md` Wireframe

The design document MUST include:

```markdown
# [Page/Component Name] Design

## Overview
- Purpose: [What this page/component does]
- Target Users: [Who will use it]
- Aesthetic Direction: [Chosen tone/style]

## Wireframe (ASCII)
┌─────────────────────────────────────────┐
│  Header / Navigation                    │
├─────────────────────────────────────────┤
│                                         │
│  [Section layout with approximate       │
│   positioning of elements]              │
│                                         │
├─────────────────────────────────────────┤
│  Footer                                 │
└─────────────────────────────────────────┘

## Component Hierarchy
- Page Container
  - Header
    - Logo
    - Navigation
  - Main Content
    - [List components and nesting]
  - Footer

## Design Tokens (Consistency System)
[See UI/UX Consistency section below]

## Responsive Breakpoints
- Desktop (1200px+): [layout description]
- Tablet (768px-1199px): [layout description]
- Mobile (<768px): [layout description]

## Interactions & Animations
- [List key interactions and their behaviors]
```

### Step 3: Implement Code

Only after the design document is approved/created, implement working code (HTML/CSS/JS, React, Vue, etc.) that is:
- Production-grade and functional
- Visually striking and memorable
- Cohesive with a clear aesthetic point-of-view
- Meticulously refined in every detail

## UI/UX Consistency Guidelines

**CRITICAL**: Maintain strict visual consistency across all components. Define these in the `page_design.md` and enforce throughout implementation.

### Design Token System

Create and use CSS variables for all design decisions:

```css
:root {
  /* Page & Layout Backgrounds */
  --bg-page: #...;           /* Main page background */
  --bg-page-alt: #...;       /* Alternate sections */

  /* Component Backgrounds */
  --bg-card: #...;           /* Cards, panels */
  --bg-card-hover: #...;     /* Interactive state */
  --bg-input: #...;          /* Form inputs */
  --bg-button-primary: #...;
  --bg-button-secondary: #...;

  /* Text Colors */
  --text-primary: #...;      /* Main body text */
  --text-secondary: #...;    /* Subdued text */
  --text-muted: #...;        /* Hints, placeholders */
  --text-inverse: #...;      /* Text on dark backgrounds */
  --text-accent: #...;       /* Links, highlights */
  --text-error: #...;
  --text-success: #...;

  /* Alignment & Spacing */
  --spacing-unit: 8px;       /* Base unit */
  --spacing-xs: 4px;
  --spacing-sm: 8px;
  --spacing-md: 16px;
  --spacing-lg: 24px;
  --spacing-xl: 32px;
  --spacing-2xl: 48px;

  /* Container & Content Alignment */
  --content-max-width: 1200px;
  --content-padding: var(--spacing-lg);
  --section-gap: var(--spacing-2xl);
}
```

### Consistency Rules

| Element | Rule | Example |
|---------|------|---------|
| **Page Background** | Single consistent color/gradient per page type | All dashboard pages use `--bg-page` |
| **Section Background** | Alternate between `--bg-page` and `--bg-page-alt` | Zebra striping for visual rhythm |
| **Card Background** | All cards use same `--bg-card` | Never mix card styles on same page |
| **Text on Light BG** | Always `--text-primary` | Never use random grays |
| **Text on Dark BG** | Always `--text-inverse` | Ensure WCAG AA contrast |
| **Horizontal Alignment** | Content aligned to grid | Use `--content-max-width` and `--content-padding` |
| **Vertical Spacing** | Consistent gaps between sections | Use `--section-gap` |
| **Component Spacing** | Internal padding from spacing scale | Never use arbitrary pixel values |

### Alignment Checklist

Before implementation, verify:
- [ ] All text aligns to the same grid baseline
- [ ] Section headings have consistent left alignment
- [ ] Cards in a row have identical heights (use flexbox/grid)
- [ ] Form labels align with their inputs
- [ ] Buttons align with input fields in forms
- [ ] Images align with text content
- [ ] Icons align with text baseline (use `vertical-align` or flexbox)

### Visual Hierarchy Rules

1. **Z-Index Layers** (define consistently):
   - `--z-base: 0` - Content
   - `--z-dropdown: 100` - Dropdowns, tooltips
   - `--z-sticky: 200` - Sticky headers
   - `--z-modal: 300` - Modals, dialogs
   - `--z-toast: 400` - Notifications

2. **Shadow System** (consistent depth):
   - `--shadow-sm` - Subtle lift (cards)
   - `--shadow-md` - Moderate lift (dropdowns)
   - `--shadow-lg` - Strong lift (modals)

3. **Border Radius** (consistent curves):
   - `--radius-sm: 4px` - Buttons, inputs
   - `--radius-md: 8px` - Cards
   - `--radius-lg: 16px` - Modals, large panels
   - `--radius-full: 9999px` - Pills, avatars

## Frontend Aesthetics Guidelines

Focus on:
- **Typography**: Choose fonts that are beautiful, unique, and interesting. Avoid generic fonts like Arial and Inter; opt instead for distinctive choices that elevate the frontend's aesthetics; unexpected, characterful font choices. Pair a distinctive display font with a refined body font. Ensure readability for Vietnamese diacritics. Use a responsive type scale (mobile → desktop) with line-height 1.5–1.8 for body text. **Define all font sizes in design tokens.**
- **Color & Theme**: Commit to a cohesive aesthetic. **Use the Design Token System (CSS variables) defined in `page_design.md`** for a consistent design system. Dominant colors with sharp accents outperform timid, evenly-distributed palettes. Ensure WCAG AA contrast ratios for accessibility. **Never use hardcoded color values — always reference tokens.**
- **Motion**: Use animations for effects and micro-interactions. Prioritize CSS-only solutions for HTML. Use Motion library for React when available. Focus on high-impact moments: one well-orchestrated page load with staggered reveals creates more delight than scattered micro-interactions. Use scroll-triggering and hover states that surprise.
- **Spatial Composition**: Unexpected layouts. Asymmetry. Overlap. Diagonal flow. Grid-breaking elements. Generous negative space OR controlled density. **Use the spacing scale from design tokens (8px base unit) — never arbitrary pixel values.** Maintain clear visual hierarchy with consistent alignment.
- **Backgrounds & Visual Details**: Create atmosphere and depth rather than defaulting to solid colors. **Use `--bg-page`, `--bg-card`, and other background tokens consistently.** Add contextual effects and textures that match the overall aesthetic. Apply creative forms like gradient meshes, noise textures, geometric patterns, layered transparencies, dramatic shadows, decorative borders, custom cursors, and grain overlays.
- **Alignment & Layout Consistency**: **All components on a page must follow the same alignment rules.** Use CSS Grid or Flexbox for consistent item alignment. Define `--content-max-width` and ensure all sections respect it. Vertical rhythm should use consistent `--section-gap` values.

NEVER use generic AI-generated aesthetics like overused font families (Inter, Roboto, Arial, system fonts), cliched color schemes (particularly purple gradients on white backgrounds), predictable layouts and component patterns, and cookie-cutter design that lacks context-specific character.

Interpret creatively and make unexpected choices that feel genuinely designed for the context. No design should be the same. Vary between light and dark themes, different fonts, different aesthetics. NEVER converge on common choices (Space Grotesk, for example) across generations.

## Animation & Interaction Principles

Follow these timing rules strictly:
- **Fast (150–250ms)**: Hover effects, button state changes, color transitions
- **Medium (300–500ms)**: Tab switching, accordion expand/collapse, slide transitions
- **Slow (600–1000ms)**: Page load fade-ins, complex reveals, parallax shifts

### Easing
- Use easing functions (`ease-in-out`, `cubic-bezier`) — never linear (except progress bars)
- Prefer natural, physics-based motion curves

### Motion Sensitivity
- Respect `prefers-reduced-motion` — provide a way to disable animations
- Animations must serve a purpose: guide attention, provide feedback, or create delight
- Never run multiple heavy animations simultaneously

## Responsive Design

- **Desktop**: Full multi-column layouts, hover interactions, parallax effects
- **Tablet**: 2-column grids, collapsed menus, touch-optimized targets
- **Mobile**: Single column, hamburger menu, large touch targets (min 44px), swipe gestures
- All breakpoints must be tested and functional

## Performance

- Lazy-load images and below-fold content
- Use WebP format for images
- Minify CSS/JS in production
- Target page load < 3 seconds
- Use skeleton screens for content sections during load

**IMPORTANT**: Match implementation complexity to the aesthetic vision. Maximalist designs need elaborate code with extensive animations and effects. Minimalist or refined designs need restraint, precision, and careful attention to spacing, typography, and subtle details. Elegance comes from executing the vision well.

Remember: Claude is capable of extraordinary creative work. Don't hold back, show what can truly be created when thinking outside the box and committing fully to a distinctive vision.

## Implementation Workflow

**ALWAYS follow this order:**

```
1. READ requirements.md and existing codebase
       ↓
2. CREATE page_design.md (wireframe + design tokens)
       ↓
3. DEFINE CSS variables (design token system)
       ↓
4. IMPLEMENT structure (HTML/JSX)
       ↓
5. APPLY styles (using ONLY design tokens)
       ↓
6. ADD interactions & animations
       ↓
7. VERIFY consistency checklist
```

## Pre-Implementation Consistency Checklist

Before writing code, confirm these are defined in `page_design.md`:

- [ ] Page background color/gradient defined (`--bg-page`)
- [ ] Component backgrounds defined (`--bg-card`, `--bg-input`, etc.)
- [ ] Text color hierarchy defined (`--text-primary`, `--text-secondary`, `--text-muted`)
- [ ] Spacing scale defined (8px base unit)
- [ ] Content max-width and padding defined
- [ ] Section gaps defined
- [ ] Border radius scale defined
- [ ] Shadow system defined
- [ ] Z-index layers defined

## Post-Implementation Consistency Audit

After coding, verify:

- [ ] No hardcoded colors — all use CSS variables
- [ ] No hardcoded spacing — all use spacing tokens
- [ ] All cards on same page have identical styling
- [ ] Text colors match the defined hierarchy
- [ ] Backgrounds are consistent across similar elements
- [ ] Horizontal alignment is consistent (same max-width, padding)
- [ ] Vertical spacing uses consistent gap values
- [ ] Interactive states (hover, focus, active) are consistent
- [ ] Responsive breakpoints maintain alignment consistency
