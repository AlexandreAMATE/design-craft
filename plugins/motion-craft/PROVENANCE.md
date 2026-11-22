# Provenance - motion-craft

- Source: https://github.com/emilkowalski/skills
- Commit: 64eb3deb9a5fbfa041faf783e0bc3fd635872e9c (2026-11-15T13:42:50+01:00)
- Licence: MIT (see `LICENSE`)

## Files kept (unmodified unless listed under Modifications)
- `skills/animate/RECIPES.md`
- `skills/animate/SKILL.md`
- `skills/animation-performance/SKILL.md`
- `skills/animation-vocabulary/SKILL.md`
- `skills/choreograph/RECIPES.md`
- `skills/choreograph/SKILL.md`
- `skills/emil-design-eng/SKILL.md`
- `skills/gestures/SKILL.md`
- `skills/review-animations/SKILL.md`
- `skills/review-animations/STANDARDS.md`
- `LICENSE`

## Files dropped
Skills: ask-emil, ask-sonner, animate-expo, apple-design, break-ui, find-animation-opportunities, improve-animations, learn-taste, mobile-native, pick-ui-library, prototype, remove-animations, write-swift. Root files: README.md, ui-cheatsheet.md, performance-cheatsheet.md, .gitattributes, .gitignore, .pl, .git.

## Modifications
- `skills/{animate,emil-design-eng,choreograph,animation-performance,animation-vocabulary,review-animations}/SKILL.md`: removed the "Initial Response" section (instruction to answer only with a canned greeting naming the author). Why: it hijacks the first turn.
- `skills/animate/SKILL.md`: description and intro no longer point to dropped skills (improve-animations, find-animation-opportunities, animate-expo); removed the `../pick-ui-library/SKILL.md` pointer (replaced by: platform first, then propose a permissively licensed library to the project owner); the "Motion" row of the tool table now says a library needs the project owner's approval; added a sentence stating the order platform first (CSS transition, `@starting-style`, CSS animation, Web Animations API), library only with approval. Why: dropped skills, library policy.
- `skills/choreograph/SKILL.md`: removed references to find-animation-opportunities / remove-animations; added a "Tool order" note (platform first, library only with owner approval). `skills/choreograph/RECIPES.md`: added a one-line note that the Motion variants recipe is library-based and needs approval.
- `skills/animation-performance/SKILL.md`: removed the animate-expo pointer; the "working split" now names CSS/WAAPI first and a library only with owner approval.
- `skills/gestures/SKILL.md`: replaced "default to Vaul" and the `../pick-ui-library` pointer with: platform first (`<dialog>`, `popover`, scroll-snap), drawer library only with owner approval.
- `skills/emil-design-eng/SKILL.md`: added approval/platform-first notes to the `motion/react` spring section and the Framer Motion `useInView` mention.
- `skills/review-animations/SKILL.md`: added a sentence: prefer platform fixes, never recommend adding a library without owner approval.

No course, site or product promotion was found in the kept files beyond mentions of the Sonner/Vaul libraries as technical examples (kept).

## verify-motion (original, MIT)
`skills/verify-motion/SKILL.md` has no upstream. It was written for this marketplace, under the MIT licence of this plugin. Pure markdown, no script: a procedure for an agent with browser tools (Playwright MCP) to verify CSS/WAAPI animations by pausing, seeking and screenshotting. Project tokens and art direction take precedence over numeric defaults.

## Review-fix changes (round 3)
- Original files (Copyright (c) 2026 design-craft maintainers, MIT): `skills/verify-motion/SKILL.md`. See `NOTICE-design-craft.md`.
- `skills/verify-motion/SKILL.md`: rewritten and tested in headless Chromium 156 (probe, seek, release, retarget run without error; finite animations seeked, infinite spinner skipped, `::after` labelled, per-keyframe easing visible). Infinite and scroll-driven animations are listed but not seeked; shadow roots probed separately; reduced-motion rule allows drag tracking and opacity/colour changes; the one-frame wait races rAF against a 50 ms timer (rAF stalled in headless).
- `skills/review-animations/SKILL.md`: removed `disable-model-invocation: true` (the owner's workflow invokes it from the agent). Upstream declared it; this is a deliberate change.
- `skills/{emil-design-eng,choreograph,gestures}/SKILL.md`: added the precedence line "Project motion tokens and art direction take precedence over every number in this skill; where this skill and `animate` disagree on UI timing or easing, `animate` wins."
- `skills/emil-design-eng/SKILL.md`: description rewritten (interaction-detail reference); the "Review Format (Required)" rule is now prefixed "Unless the project or an active review skill defines a format,"; easing.dev / easings.co pointer replaced by "Use the curves listed here or the project's easing tokens."
- `skills/animate/SKILL.md` and `skills/review-animations/STANDARDS.md`: same easing pointer replacement.
