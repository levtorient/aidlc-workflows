---
name: frontend-design
description: Create distinctive, production-grade frontend interfaces with high design quality. Use this skill when the user asks to build web components, pages, artifacts, posters, or applications (examples include websites, landing pages, dashboards, React components, HTML/CSS layouts, or when styling/beautifying any web UI). Generates creative, polished code and UI design that avoids generic AI aesthetics.
license: Complete terms in LICENSE.txt
---

This skill guides creation of distinctive, production-grade frontend interfaces that avoid generic "AI slop" aesthetics. Implement real working code with exceptional attention to aesthetic details and creative choices.

The user provides frontend requirements: a component, page, section, or interface to build. Always read `requirements.md` at the project root and the existing codebase before implementing — derive all structure, sections, and interactions from the actual requirements.

## Design Thinking

Before coding, understand the context and commit to a BOLD aesthetic direction:
- **Purpose**: What problem does this interface solve? Who uses it?
- **Tone**: Pick an extreme: brutally minimal, maximalist chaos, retro-futuristic, organic/natural, luxury/refined, playful/toy-like, editorial/magazine, brutalist/raw, art deco/geometric, soft/pastel, industrial/utilitarian, etc. There are so many flavors to choose from. Use these for inspiration but design one that is true to the aesthetic direction.
- **Constraints**: Technical requirements (framework, performance, accessibility).
- **Differentiation**: What makes this UNFORGETTABLE? What's the one thing someone will remember?

**CRITICAL**: Choose a clear conceptual direction and execute it with precision. Bold maximalism and refined minimalism both work — the key is intentionality, not intensity.

Then implement working code (HTML/CSS/JS, React, Vue, etc.) that is:
- Production-grade and functional
- Visually striking and memorable
- Cohesive with a clear aesthetic point-of-view
- Meticulously refined in every detail

## Frontend Aesthetics Guidelines

Focus on:
- **Typography**: Choose fonts that are beautiful, unique, and interesting. Avoid generic fonts like Arial and Inter; opt instead for distinctive choices that elevate the frontend's aesthetics; unexpected, characterful font choices. Pair a distinctive display font with a refined body font. Ensure readability for Vietnamese diacritics. Use a responsive type scale (mobile → desktop) with line-height 1.5–1.8 for body text.
- **Color & Theme**: Commit to a cohesive aesthetic. Use CSS variables for a consistent design system. Dominant colors with sharp accents outperform timid, evenly-distributed palettes. Ensure WCAG AA contrast ratios for accessibility.
- **Motion**: Use animations for effects and micro-interactions. Prioritize CSS-only solutions for HTML. Use Motion library for React when available. Focus on high-impact moments: one well-orchestrated page load with staggered reveals creates more delight than scattered micro-interactions. Use scroll-triggering and hover states that surprise.
- **Spatial Composition**: Unexpected layouts. Asymmetry. Overlap. Diagonal flow. Grid-breaking elements. Generous negative space OR controlled density. Use a consistent spacing system (e.g., 8px base unit) with clear visual hierarchy.
- **Backgrounds & Visual Details**: Create atmosphere and depth rather than defaulting to solid colors. Add contextual effects and textures that match the overall aesthetic. Apply creative forms like gradient meshes, noise textures, geometric patterns, layered transparencies, dramatic shadows, decorative borders, custom cursors, and grain overlays.

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
