---
name: ux-reviewer
description: Review and audit web interfaces for UX quality, accessibility compliance, responsive design, and performance. Use this skill when the user wants to verify WCAG compliance, test responsive layouts, audit interaction patterns, or optimize the user experience. Returns actionable findings with severity levels.
---

This skill performs structured UX and accessibility audits. Read `requirements.md` and the actual codebase to understand what was built and what the expected behavior is. Audit against the requirements and web standards — not against a fixed checklist.

## Approach

1. **Read requirements** — understand what the expected behavior and UX criteria are
2. **Read the code** — inspect the actual implementation to find gaps
3. **Audit by pillar** — work through the five pillars below in order
4. **Report findings** — use the severity format at the bottom, with actionable fixes

## Audit Pillars

### 1. Accessibility (WCAG AA)

- **Contrast**: 4.5:1 for normal text, 3:1 for large text. Color never sole information carrier.
- **Keyboard**: All interactive elements reachable via Tab. Logical focus order. No keyboard traps. Escape closes overlays. Arrow keys for grouped controls.
- **Screen readers**: Meaningful `alt` text (decorative = `alt=""`). ARIA labels where needed. ARIA live regions for dynamic updates. Proper heading hierarchy. Labels on form inputs.
- **Motion**: Respects `prefers-reduced-motion`. Auto-playing content has pause controls. No information conveyed solely through animation.
- **Text**: Body text uses relative units (rem/em). Line height 1.5–1.8. Line width under ~75 characters. All chosen fonts render diacritics correctly.

### 2. Responsive Design

Test at real device widths, not just breakpoints:
- **Mobile** (320–414px): Touch targets min 44px, no horizontal scroll, mobile keyboard usability, swipe gestures where expected
- **Tablet** (768–1024px): Multi-column layouts correct, menus collapse appropriately, images scale properly
- **Desktop** (1280–1920px): Full layouts render without gaps, hover states present, parallax/effects smooth

### 3. Interaction Quality

- **Navigation**: Smooth scroll, active states, sticky behavior per requirements
- **Animation timing**: Fast (150–250ms) for hovers, medium (300–500ms) for transitions, slow (600–1000ms) for reveals. Proper easing, no jank.
- **Components**: Verify every interactive component works as specified in requirements — carousels, accordions, modals, tabs, forms, timers, etc.
- **States**: Every interactive element needs default, hover, active, focus, disabled, loading, error, and success states where applicable

### 4. Performance

- **Loading**: Above-fold renders first. Images lazy-load below fold. Skeleton screens during load. No layout shifts (CLS < 0.1).
- **Assets**: WebP with fallbacks. Correctly sized images per viewport. Minified CSS/JS. Fonts use `font-display: swap`.
- **Runtime**: 60fps scroll. No layout thrashing from animations. Throttled/debounced event listeners. No memory leaks from intervals or listeners.

### 5. Conversion & Engagement

- **Trust**: Testimonials feel authentic. Credentials verifiable. Guarantees visible.
- **Purchase/Action flow**: Pricing clear. Differences easy to compare. Button states for full lifecycle (default → loading → success/error). Error recovery is obvious.
- **Engagement features**: Verify any engagement hooks specified in requirements work correctly (popups, newsletters, sharing, progress indicators, etc.)

## Report Format

Organize findings as:

```
## [Area] Audit

### Critical (Must Fix)
- [Issue]: [Description] → [Fix]

### Warning (Should Fix)
- [Issue]: [Description] → [Fix]

### Info (Nice to Have)
- [Issue]: [Description] → [Suggestion]

### Passed
- [What was checked and passed]
```

- **Critical**: Blocks users, breaks functionality, or violates WCAG A/AA
- **Warning**: Degrades experience significantly but doesn't block
- **Info**: Polish and enhancement opportunities
