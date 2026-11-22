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
