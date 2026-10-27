# 0001: Split design-development-philosophy into a kernel plus references

- **Status**: proposed (pending the comparison in
  `field-notes/2026-10-27-philosophy-skill-size.md`)
- **Date**: 2026-10-27

## Decision

Reshape the skill from one 22-principle file (v0.1) into:

- `SKILL.md`: a behavioral kernel of 17 principles, each keeping its checklist
  or contrast, plus the default AI pattern, heuristics, and working style.
- `references/ai-system-design.md` and `references/evaluation.md`: deeper
  guidance, loaded only when a concrete trigger applies.
- `concepts/significance-engine/README.md`: the developing concept, marked
  untested.

## Context

Kelly raised a concern about the file's size. Discussion (Copilot, Hark)
concluded that load cost is mostly not the issue, because skills are
progressively disclosed. The real issue is cohesion: v0.1 mixed core
philosophy, detailed AI-design and evaluation guidance, and material drifting
toward the Significance Engine concept.

Adopted convention: every line loaded when a skill activates should have a
good chance of changing the model's behavior.

## Alternatives considered

1. **Keep v0.1 as is.** Works; no observed misbehavior. Rejected only if the
   comparison shows v0.2 is at least as good, since the reshape is cheap and
   reversible.
2. **Copilot's 14 one-line principles.** Rejected: one-liners drop the
   checklists that change behavior, and moving attention, decay, and stated vs
   revealed values into the concept would downgrade general principles to
   hypotheses.
3. **Kernel + references with triggers (chosen).**

## Where each v0.1 principle went

| v0.1 | v0.2 |
|---|---|
| 1 Problem first | Core 1 |
| 2 Inspectable | Core 2 |
| 3 Complexity earns place | Core 3 (all five questions kept) |
| 4 Validate uncertainty | Core 4; record format → evaluation.md |
| 5 Evidence → action pipeline | Core 5; stage table → ai-system-design.md |
| 6 Judgment vs authority | Core 6; checklist → ai-system-design.md |
| 7 Uncertainty as data | Core 7 |
| 8 Earn authority | Core 8; level table → ai-system-design.md |
| 9 Feedback loops | evaluation.md (trigger in SKILL.md) |
| 10 Baseline | Core 9; detail → evaluation.md |
| 11 Historical evaluation | evaluation.md (trigger in SKILL.md) |
| 12 Attention finite | Core 13 |
| 13 Model context | ai-system-design.md; also concept |
| 14 Significance vs attention priority | Core 13 (merged, short); detail → concept |
| 15 Resolution and decay | Core 14 |
| 16 Stated vs revealed | Core 15 |
| 17 Explainable decisions | Core 12 (merged with observability) |
| 18 Observability | Core 12 |
| 19 Smallest disproving experiment | Core 10 |
| 20 Reversibility | Core 11 |
| 21 Record decisions | Core 16; ADR template → evaluation.md |
| 22 Resist generalization | Core 17 |

Nothing was dropped; three were relocated behind triggers (9, 11, 13).

## Evidence

- Observed: one author concern about size and cohesion. No observed
  misbehavior from v0.1.
- Pending: side-by-side comparison on real design prompts.

## Trade-offs

- Agents may not open reference files. Mitigated by concrete triggers; to be
  checked in the comparison.
- Three principles are no longer always in context.

## Revisit if

- The comparison shows v0.2 answers miss guidance that v0.1 applied.
- Agents repeatedly fail to load a reference when its trigger applied.
- A relocated principle turns out to matter in most design conversations.
