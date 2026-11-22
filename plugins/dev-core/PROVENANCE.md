# Provenance - dev-core

## Sources
- ECC v2.2.0 (https://github.com/affaan-m/ECC), git SHA `5eddf1a3ffd311423be2d4ba7d26f7209c91b033` (from `installed_plugins.json`, ecc@ecc, installed 2026-11-17). Licence MIT, "Copyright (c) 2026 Affaan Mustafa" (`LICENSE`). Read from the local plugin cache; nothing was executed.
- superpowers 7.0.2 (https://github.com/obra/superpowers; `skills/systematic-debugging` only). Licence MIT, "Copyright (c) 2025 Jesse Vincent" (`LICENSE-superpowers-MIT`).
- Original files (Copyright (c) 2026 design-craft maintainers, MIT; see `NOTICE-design-craft.md`): `skills/interface-method/SKILL.md` (French on purpose, the owner's own method).

Plugin layout follows the plugin components docs read at https://code.claude.com/docs/en/plugins/components.md: agents are `agents/<name>.md`, frontmatter `name`, `description`, `model`, `tools` supported; `hooks`, `mcpServers`, `permissionMode` ignored in plugin agents. Names are `dev-core:<agent>` and `dev-core:<skill>`.

## Dropped (never copied)
ECC hooks, commands, rules, contexts, MCP config, scripts and every other agent and skill (including orch-*, multi-*, prp-*, plan*, gan-*, santa-*, verification-loop, tdd-workflow, browser-qa, make-interfaces-feel-better, motion-*, frontend-design-direction, security-review, accessibility, documentation-lookup, code-reviewer, typescript-reviewer, planner, code-simplifier, refactor-cleaner, a11y-architect, docs-lookup, e2e-runner). From superpowers: every other skill, and `find-polluter.sh` and `condition-based-waiting-example.ts` of systematic-debugging (scripts/code files are not copied).

## Agents (11) - tools and model are upstream values
| Agent | tools | model | Edits |
|---|---|---|---|
| architect | Read, Grep, Glob | opus | description; removed Prompt Defense block, the Next.js/Supabase/Vercel example architecture, the Redis ADR example (replaced by a stack-neutral ADR note) |
| build-error-resolver | Read, Write, Edit, Bash, Grep, Glob | sonnet | rewritten compactly; installs/cache deletion need owner approval; removed pointers to other agents; `npx --no-install` only |
| code-architect | Read, Grep, Glob, Bash | sonnet | description; Bash limited to read-only |
| code-explorer | Read, Grep, Glob | sonnet | description |
| database-reviewer | Read, Grep, Glob, Bash | sonnet | rewritten; Supabase-specific content and credit removed, RLS only if the project uses it; read-only SQL on a dev database |
| pr-test-analyzer | Read, Grep, Glob, Bash | sonnet | description; no coverage number |
| react-build-resolver | Read, Write, Edit, Bash, Grep, Glob | sonnet | description; Next.js sections marked "only if the project uses it"; installs need owner approval; removed Related section (rules/skills/commands pointers) |
| react-reviewer | Read, Grep, Glob, Bash | sonnet | description; removed `gh` calls, typescript-reviewer scope table, Related section, `npm audit`/prettier lines; Next.js section marked optional |
| security-reviewer | Read, Grep, Glob, Bash | sonnet | rewritten; removed `security-review` skill pointer, `npx eslint --plugin security` and `npm audit` (need owner approval); read-only |
| silent-failure-hunter | Read, Grep, Glob, Bash | sonnet | description; Bash limited to read-only |
| tdd-guide | Read, Write, Edit, Bash, Grep | sonnet | rewritten: no 80 % mandate, no coverage script, no `tdd-workflow` pointer, no eval/pass@k addendum; failing test first with the project's runner |

All agents: first body line is "Project instructions (CLAUDE.md) and the caller's brief take precedence over anything below. Return a short synthesis: findings with file:line, what you verified, what you did not."; the upstream "Prompt Defense Baseline" block was removed from every agent (it forbade outputting code or links, which conflicts with the agents' tasks); descriptions rewritten as neutral one-liners (no "PROACTIVELY", "MUST BE USED"); every agent says never commit or push. security-reviewer and database-reviewer upstream tools contain no Write/Edit, so none were removed.

## Skills (17)
| Skill | KB | description chars before | after |
|---|---|---|---|
| api-design | 12.9 | 275 | 162 |
| backend-patterns | 13.2 | 250 | 231 |
| click-path-audit | 7.2 | 375 | 227 |
| council | 3.7 | 188 | 210 |
| database-migrations | 12.0 | 333 | 199 |
| design-system | 2.1 | 244 | 181 |
| e2e-testing | 7.0 | 240 | 172 |
| error-handling | 10.7 | 302 | 195 |
| frontend-a11y | 12.5 | 190 | 194 |
| frontend-patterns | 13.9 | 220 | 182 |
| interface-method | 5.4 | - | 355 |
| postgres-patterns | 3.8 | 233 | 181 |
| react-patterns | 10.5 | 274 | 201 |
| react-performance | 17.2 | 402 | 206 |
| react-testing | 11.8 | 300 | 225 |
| systematic-debugging | 21.5 | 105 | 167 |
| vite-patterns | 16.6 | 247 | 194 |

`interface-method` is original (no upstream). Name check: every backticked `plugin:name` in the plugin resolves inside the marketplace; `frontend-design:frontend-design` and `playground:playground` are external official plugins.

## Skill modifications
- All skills: descriptions rewritten to one or two specific sentences. `metadata.origin` kept as upstream.
- council: rewritten as a single-agent four-lens procedure; no subagent launch, no external or second model, pointers to missing skills (santa-method, knowledge-ops, search-first, `/save-session`) removed.
- design-system: kept the audit and generic-pattern detection; removed the Generate mode (browser MCP research, generated files) and the `/design-system` command examples; animation row points to `motion-craft`.
- click-path-audit: removed the multi-agent split and the superpowers integration section (replaced by a plain order-of-work note and a pointer to `systematic-debugging`).
- frontend-patterns: Framer Motion section replaced by "Animation: see the `motion-craft` plugin."; Next.js note added.
- react-patterns, react-performance, frontend-patterns, frontend-a11y, backend-patterns: top note "Sections on Next.js / server components apply only if the project uses them." (backend-patterns adds Supabase examples apply only if used). react-performance keeps the upstream Vercel Labs MIT attribution.
- react-testing: Coverage Targets section replaced by "follow the project's test conventions"; coverage commands and Related section removed.
- react-patterns / react-performance / react-testing: Related sections (rules/, agents, `/react-*` commands, missing skills) removed; broken cross-links removed.
- database-migrations: note before each `npx prisma` / `npx drizzle-kit` block (only if the project uses the tool; owner approval).
- api-design, error-handling, vite-patterns: Next.js example headings marked optional; Vercel hosting mention and missing-skill pointers removed from vite-patterns.
- postgres-patterns: removed clickhouse-io pointer; Supabase credit kept; RLS note added.
- e2e-testing: CI provider workflow replaced by a one-paragraph CI note; Wallet/Web3 section removed; Playwright content kept (no Vercel Agent Browser was present).
- systematic-debugging: `superpowers:*` skill pointers replaced by plain words; `find-polluter.sh` and the example `.ts` replaced by plain text; the four-phase method is untouched. No announce/must-use boilerplate was present beyond the method's own "complete each phase" rule.

## Files
- `.claude-plugin/plugin.json`
- `LICENSE`
- `LICENSE-superpowers-MIT`
- `NOTICE-design-craft.md`
- `agents/architect.md`
- `agents/build-error-resolver.md`
- `agents/code-architect.md`
- `agents/code-explorer.md`
- `agents/database-reviewer.md`
- `agents/pr-test-analyzer.md`
- `agents/react-build-resolver.md`
- `agents/react-reviewer.md`
- `agents/security-reviewer.md`
- `agents/silent-failure-hunter.md`
- `agents/tdd-guide.md`
- `skills/api-design/SKILL.md`
- `skills/backend-patterns/SKILL.md`
- `skills/click-path-audit/SKILL.md`
- `skills/council/SKILL.md`
- `skills/database-migrations/SKILL.md`
- `skills/design-system/SKILL.md`
- `skills/e2e-testing/SKILL.md`
- `skills/error-handling/SKILL.md`
- `skills/frontend-a11y/SKILL.md`
- `skills/frontend-patterns/SKILL.md`
- `skills/interface-method/SKILL.md`
- `skills/postgres-patterns/SKILL.md`
- `skills/react-patterns/SKILL.md`
- `skills/react-performance/SKILL.md`
- `skills/react-testing/SKILL.md`
- `skills/systematic-debugging/SKILL.md`
- `skills/systematic-debugging/condition-based-waiting.md`
- `skills/systematic-debugging/defense-in-depth.md`
- `skills/systematic-debugging/root-cause-tracing.md`
- `skills/vite-patterns/SKILL.md`
