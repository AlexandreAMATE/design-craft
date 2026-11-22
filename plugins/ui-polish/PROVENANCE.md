# Provenance - ui-polish

- Source: https://github.com/jakubkrehel/skills
- Commit: 672ae44ace6aaed65b86cbb1e2fd6fbea0e79578 (2026-11-18T23:11:30-05:00, verified on disk)
- Licence: MIT (`LICENSE`, copied from upstream)

## Files kept
- `skills/better-interface/SKILL.md`
- `skills/better-interface/review-format.md`
- `skills/better-layout/SKILL.md`
- `skills/better-layout/grouping-and-alignment.md`
- `skills/better-layout/reporting.md`
- `skills/better-layout/spacing-and-adaptivity.md`
- `skills/better-typography/SKILL.md`
- `skills/better-typography/choosing-fonts.md`
- `skills/better-typography/css-cheat-sheet.md`
- `skills/better-typography/details-and-accessibility.md`
- `skills/better-typography/reporting.md`
- `skills/better-typography/spacing-and-sizing.md`
- `skills/better-typography/variable-fonts-and-opentype.md`
- `skills/better-typography/wrapping-and-punctuation.md`
- `skills/better-ui/SKILL.md`
- `skills/better-ui/icons.md`
- `skills/better-ui/reporting.md`
- `skills/better-ui/surfaces.md`
- `skills/interface-review/SKILL.md`
- `skills/interface-review/removed-signals.md`
- `skills/interface-review/scope-resolution.md`
- `LICENSE`

## Files dropped
Skills: better-motion, better-accessibility, better-colors, better-writing, afk, upskill, explain-interface, build-design, break, variant, state-machine. Every `agents/openai.yaml` sidecar (also in the kept skills), `opencode.json`, `AGENTS.md`, `CLAUDE.md`, `README.md`, `.claude-plugin/*` and `.gitattributes` of the upstream.

## Modifications
- All five kept skills: every pointer to `better-accessibility`, `better-colors`, `better-writing` replaced by "not covered by this pack"; every pointer to `better-motion` replaced by the `motion-craft` plugin (`animate`, `review-animations`). Files: better-layout/SKILL.md, better-layout/spacing-and-adaptivity.md, better-typography/SKILL.md, better-ui/SKILL.md, better-ui/icons.md, interface-review/SKILL.md, interface-review/scope-resolution.md, interface-review/removed-signals.md (owner column), better-interface/SKILL.md. Why: those skills are not in this marketplace.
- `better-interface/SKILL.md`: description, intro and the ordered "domain skills" list now cover layout, typography, UI and (if installed) motion via `review-animations`; accessibility, color and writing are reported as `Not reviewed: not covered by this pack`; added a sentence on escalation triggers belonging to uncovered domains. `better-interface/review-format.md`: same requirement in the coverage table.
- `interface-review/SKILL.md`: description rewritten to the covered domains; "better-* skills in this pack". Frontmatter `disable-model-invocation: true` is kept as declared upstream, so the skill is manual-only (user invoked).
- Motion numbers replaced by "see motion-craft; project motion tokens take precedence": `better-ui/surfaces.md` (150ms ease-out in the card example, now `var(--motion-duration)` / `var(--motion-ease)` plus a comment), `better-typography/details-and-accessibility.md` (200ms ease-out underline transition, same treatment), `better-ui/icons.md` (pointer to motion values).
- Remaining behaviour to know: `interface-review` instructs the agent to run read-only `git diff` / `gh pr view` commands on the user's project; kept unchanged.
