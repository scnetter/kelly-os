---
name: design-development-philosophy
description: >
  Applies Kelly's pragmatic, evidence-driven design and development philosophy
  to software, automation, AI systems, and agentic workflows. Use when designing
  architecture, evaluating implementation approaches, deciding where to use
  deterministic logic versus AI, defining automation authority, planning
  experiments, or reviewing whether complexity is justified.
version: 0.2
---

# Design & Development Philosophy

Build systems that are understandable, testable, observable, evidence-driven,
appropriately simple, safe to evolve, and respectful of human attention and
authority.

This is a posture, not an architecture, stack, or lifecycle.

Do not generalize from what sounds right. Generalize from what survives contact
with reality.

---

## Core Principles

### 1. Start with the problem, not the technology

Before choosing a tool, name: the actual problem, who has it, the current
workflow, known failure modes, constraints, and what evidence would show
improvement. Do not introduce AI, agents, orchestration, or infrastructure
because they are available.

### 2. Prefer inspectable systems over magic

Explicit rules before inferred rules. Deterministic checks before probabilistic
judgment. Structured data before free-form interpretation. Use an LLM only for
the parts that genuinely need language understanding, interpretation, or
ambiguity resolution, never merely because it can do the task.

### 3. Complexity must earn its place

Prefer: simple mechanism → validated behavior → observed limitation → justified
capability. Avoid: anticipated requirements → generalized architecture → large
build → eventual validation.

Before adding any component, answer:

1. What problem does it solve?
2. Have we actually observed that problem?
3. Can an existing component solve it?
4. How will we know it improved the system?
5. What new failure modes or operating costs does it bring?

### 4. Validate the riskiest uncertainty early

Find the assumption that would invalidate the design (Does the API expose the
data? Is the identifier stable? Can the two systems be correlated? Is the
history available?) and test it before building on it. A feasibility
experiment must produce evidence, not merely code.

### 5. Separate evidence, extraction, judgment, policy, and action

raw evidence → extraction → derived features → assessment → confidence →
policy → permitted action

These need not be separate services, but they must stay conceptually
distinguishable so each can be inspected, tested, and replaced. Do not hide
deterministic logic inside prompts.

### 6. Separate judgment from authority

A component that evaluates something does not thereby gain permission to act on
it. Represent separately what the evidence is, what it is believed to mean, how
confident the system is, what policy permits, and what is authorized. Greater
model capability does not justify greater authority. Authority is granted
deliberately.

### 7. Treat uncertainty as data

Distinguish known facts, derived facts, assumptions, probabilistic assessments,
missing evidence, and conflicting evidence. Confidence drives policy:

- high significance + low confidence → ask or investigate
- not: high significance → act

When uncertainty is decision-relevant, expose it rather than hiding it behind a
definitive answer. Never ask an LLM to invent certainty the evidence lacks.

### 8. Earn automation authority

observe → recommend → ask → act

Move up only when the current level has proven reliable for the intended use.
The acceptable level depends on consequence of error, reversibility,
confidence, track record, observability, and safeguards. Higher consequence
demands more evidence. This is a principle for controlling authority, not a
mandatory project lifecycle.

### 9. Compare against a simpler baseline

A sophisticated system must beat the simpler alternative: the current human
workflow, deterministic rules, recency or urgency ordering, a simple heuristic,
or direct LLM judgment without extra architecture. If the gain doesn't justify
the cost, prefer the simpler system. A negative result is useful.

### 10. Build the smallest experiment that could disprove the idea

Ask: what is the cheapest credible test that could show this does not work?
Prefer tests that distinguish approaches (baseline vs deterministic vs LLM-only
vs hybrid). Define the success criterion before looking at results. Do not
build the production architecture to find out whether the idea has merit.

### 11. Preserve reversibility

When evidence is weak, avoid committing to complex schemas, generalized
abstractions, distributed services, vendor lock-in, learned models, or
autonomous behavior. Irreversible or expensive decisions need stronger evidence
than reversible ones.

### 12. Build for observability and explanation

Keep intermediate outputs so failures can be localized: what came in, what was
extracted, which rules applied, what was retrieved, what the model produced,
what confidence was assigned, what policy decided, what happened, and what
feedback followed. For consequential decisions, explanations must come from
those recorded inputs, not from a convincing narrative written afterwards.

### 13. Treat human attention as finite

Every alert, notification, recommendation, escalation, and confirmation request
has a cost. Optimize for useful signal, not maximum relevant items. Evaluate
both "Was it correct?" and "Was it worth putting in front of a human, now?"

Significance (how much this matters in context) is not attention priority (is
this worth interrupting someone for right now). Attention priority also depends
on opportunity to act, time sensitivity, confidence, interruption cost, and
whether it was already surfaced or resolved. A correct notification at the
wrong time is still a poor decision.

### 14. Account for resolution and decay

Importance is not permanent. Track whether an item was resolved, superseded,
acknowledged, acted on, or made irrelevant, and let its priority fall
accordingly. A completed commitment should stop competing for attention. New
evidence can also raise significance.

### 15. Distinguish stated values from revealed behavior

Observed behavior is not ground truth about what someone values. Keep stated
priorities, observed behavior, and inferred preferences separate. The gap is
itself information. Never silently overwrite an explicit value because behavior
differs; avoid paternalism, explain recommendations, and allow override.

### 16. Record decisions and their evidence

When the reasoning would otherwise be lost, record: decision, context,
alternatives, evidence, reason, trade-offs, and what would justify revisiting
it. Document to preserve knowledge someone will need, not for its own sake.

### 17. Resist premature generalization

Patterns become reusable when they repeatedly survive practice. Before
generalizing, separate what was hypothesized, what was tested, what worked,
what failed, what was project-specific, and what looks reusable. Frameworks
emerge from evidence; don't force future work into abstractions built before
the evidence existed.

---

## Default Pattern for AI Systems

deterministic acquisition
→ structured extraction
→ probabilistic reasoning where useful
→ deterministic validation where possible
→ explicit policy
→ controlled action

Use deterministic software for exact transformations, stable identifiers,
equality and subset checks, schema validation, business rules, authorization,
safety boundaries, and calculations with defined answers. Use an LLM where
ambiguity, language, synthesis, classification, or contextual reasoning adds
real value.

---

## Decision Heuristics

Between competing designs, prefer the one that:

1. solves the demonstrated problem
2. tests the riskiest assumption early
3. adds the least unjustified complexity
4. preserves inspectability
5. separates deterministic and probabilistic responsibilities
6. exposes uncertainty
7. preserves human authority where consequences justify it
8. produces measurable evidence
9. keeps important decisions reversible
10. can evolve when evidence changes

When these conflict, name the trade-off explicitly instead of pretending one
design is universally correct.

---

## Working Style

1. Identify the immediate question.
2. Separate known facts from assumptions.
3. Name the highest-risk unknown.
4. Recommend the smallest useful test of it.
5. Expand scope only to solve an observed problem.
6. Park good future ideas without letting them derail current work.
7. Challenge complexity that hasn't earned its place.
8. Surface trade-offs directly.
9. Revisit earlier decisions when evidence changes the premise.

Optimize for learning what is true, not for the most sophisticated design.

---

## Supporting References (read when the trigger applies)

- **Before proposing that a model, agent, or automation takes an action, or
  when designing an AI or agentic pipeline,** read
  `references/ai-system-design.md`.
- **Before designing a feasibility spike, an evaluation, a feedback loop, a
  rollout from shadow to automated operation, or a decision record,** read
  `references/evaluation.md`.
- **If the work involves deciding what matters to a person in context (beyond
  urgency),** see `concepts/significance-engine/README.md` in the kelly-os
  repo. It is an untested concept, not established philosophy; do not treat
  it as doctrine.

---

## Scope

This skill is philosophy, not a delivery lifecycle. Sequences like discovery →
feasibility → walking skeleton → historical evaluation → shadow → assisted →
governed automation may help, but are not yet universal requirements. A
delivery framework will be extracted separately once practice shows which
patterns are durable.

---

## Core Principle

Build what the evidence justifies.
Understand it before making it clever.
Measure it before trusting it.
Let authority be earned.
