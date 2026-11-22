---
name: council
description: "Structured four-lens (architect, skeptic, pragmatist, critic) analysis of an ambiguous decision with a verdict that keeps the dissent visible. Use for tradeoffs and go/no-go calls with several credible options."
metadata:
  origin: ECC
---

# Council

Work through an ambiguous decision from four lenses, written by you in sequence, so disagreement is visible before the verdict. This skill launches no other agent and uses no external or second model.

This is for **decision-making under ambiguity**, not code review, implementation planning, or architecture design.

## When to Use

- a decision has multiple credible paths and no obvious winner
- you need explicit tradeoff surfacing, or the user asks for dissent or several perspectives
- conversational anchoring is a real risk
- a go / no-go call would benefit from adversarial challenge

Examples: monorepo vs polyrepo; ship now vs hold for polish; feature flag vs full rollout.

## When NOT to Use

| Instead of council | Use |
| --- | --- |
| Designing system architecture | the `architect` agent |
| Reviewing code for bugs or security | the review agents of this plugin |
| Straight factual questions | just answer directly |
| Obvious execution tasks | just do the task |

## Lenses

| Voice | Lens |
| --- | --- |
| Architect | correctness, maintainability, long-term implications |
| Skeptic | premise challenge, simplification, assumption breaking |
| Pragmatist | shipping speed, user impact, operational reality |
| Critic | edge cases, downside risk, failure modes |

## Workflow

1. **Extract the real question.** What are we deciding, which constraints matter, what counts as success? If the question is vague, ask one clarifying question first.
2. **Gather only the necessary context** (relevant files, snippets, metrics). Skip repo snippets for strategic questions.
3. **Write your Architect position first**: initial position, the three strongest reasons, the main risk. Do this before the other lenses so the synthesis does not just mirror them.
4. **Write the other three lenses one at a time**, each as if you knew only the question and the compact context: Position (1-2 sentences), Reasoning (3 bullets), Risk, and one Surprise the others may miss. Skeptic challenges the framing and proposes the simplest credible alternative; Pragmatist optimises for speed and real-world execution; Critic surfaces downside risk and reasons the plan could fail. Be direct, under 150 words each.
5. **Synthesize with bias guardrails.** Do not dismiss a lens without explaining why; say explicitly if a lens changed your recommendation; always include the strongest dissent; if two lenses align against your initial position, treat that as a real signal; keep the raw positions visible before the verdict.
6. **Present a compact verdict.**

```markdown
## Council: [short decision title]

**Architect:** [1-2 sentence position] / [1 line on why]
**Skeptic:** [1-2 sentence position] / [1 line on why]
**Pragmatist:** [1-2 sentence position] / [1 line on why]
**Critic:** [1-2 sentence position] / [1 line on why]

### Verdict
- **Consensus:** [where they align]
- **Strongest dissent:** [most important disagreement]
- **Premise check:** [did the Skeptic challenge the question itself?]
- **Recommendation:** [the synthesized path]
```

Do not write notes to files from this skill; record a decision only where the project keeps its decisions (for example its ADRs), and only if it changes something real.

## Anti-Patterns

- using council for code review or plain implementation work
- hiding disagreement in the final verdict
- persisting every decision regardless of importance

The value is not unanimity. The value is making the disagreement legible before choosing.
