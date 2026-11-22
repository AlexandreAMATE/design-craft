---
name: design-system
description: "Inventory and audit an existing design system: tokens, house components, visual consistency."
metadata:
  origin: ECC
---

# Design System - Inventory and Audit

Audit an existing codebase for visual consistency. This skill reads code and, if a dev server is already running and browser tools are available, the rendered UI. It generates nothing with external tools or services.

## When to Use

- Auditing an existing codebase for visual consistency
- Before a redesign, to understand what exists
- When the UI looks "off" but you cannot pinpoint why

## Visual Audit

Start by listing existing tokens, house components and animations with their paths. Then scan CSS/Tailwind/styled-components for existing patterns first: colors, typography, spacing, border-radius, shadows, breakpoints. Then score the UI across 10 dimensions (0-10 each):

```
1. Color consistency - are you using your palette or random hex values?
2. Typography hierarchy - clear h1 > h2 > h3 > body > caption?
3. Spacing rhythm - consistent scale (4px/8px/16px) or arbitrary?
4. Component consistency - do similar elements look similar?
5. Responsive behavior - fluid or broken at breakpoints?
6. Dark mode - complete or half-done?
7. Animation - purposeful or gratuitous? (see the `motion-craft` plugin)
8. Accessibility - contrast ratios, focus states, touch targets
9. Information density - cluttered or clean?
10. Polish - hover states, transitions, loading states, empty states
```

Each dimension gets a score, specific examples, and a fix with exact file:line. Prefer the project's existing tokens over new values; if the project has a design-token file, treat it as the reference.

## Generic-pattern detection

Flag generic AI-generated design patterns:

```
- Gratuitous gradients on everything
- Purple-to-blue defaults
- "Glass morphism" cards with no purpose
- Rounded corners on things that shouldn't be rounded
- Excessive animations on scroll
- Generic hero with centered text over stock gradient
- Sans-serif font stack with no personality
```

Report only; do not rewrite the design unless asked.
