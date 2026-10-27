---
name: design-development-philosophy
description: >
  Applies a pragmatic, evidence-driven design and development philosophy to
  software, automation, AI systems, and agentic workflows. Use when designing
  architecture, evaluating implementation approaches, deciding where to use
  deterministic logic versus AI, defining automation authority, planning
  experiments, or reviewing whether complexity is justified.
---

# Design & Development Philosophy

## Purpose

Use this philosophy when designing software, automation, AI-assisted systems,
agents, workflows, or technical experiments.

The goal is not to prescribe a particular architecture, technology stack, or
development methodology.

The goal is to build systems that are:

- understandable
- testable
- observable
- evidence-driven
- appropriately simple
- safe to evolve
- respectful of human attention and authority

Do not generalize from what merely sounds right. Generalize from what survives
contact with reality.

---

## 1. Start With the Problem, Not the Technology

Understand what needs to improve before selecting an architecture or tool.

Identify:

- the actual problem
- who experiences it
- the current workflow
- known failure modes
- desired outcomes
- important constraints
- what evidence would demonstrate improvement

Do not introduce AI, agents, orchestration, automation, databases, or other
infrastructure merely because they are available.

Technology should solve a demonstrated problem.

---

## 2. Prefer Inspectable Systems Over Magic

Start with the simplest mechanism whose behavior can be understood, tested,
observed, and explained.

Prefer:

- explicit rules before inferred rules
- deterministic checks before probabilistic judgment
- structured data before free-form interpretation where practical
- observable intermediate states
- explainable decisions
- measurable inputs and outputs

Introduce probabilistic or learned behavior where it provides value that
simpler mechanisms cannot adequately provide.

Do not use an LLM merely because an LLM can perform the task.

When an LLM is appropriate, constrain its responsibility to the parts of the
problem that genuinely benefit from language understanding, interpretation,
reasoning, or ambiguity resolution.

---

## 3. Complexity Must Earn Its Place

Do not design the final sophisticated system before proving the simpler system
works.

Add complexity when evidence identifies a need for it.

Prefer progression such as:

simple mechanism
→ validated behavior
→ identified limitation
→ justified additional capability

over:

anticipated future requirements
→ generalized architecture
→ large implementation
→ eventual validation

Before adding a component, ask:

1. What problem does this component solve?
2. Have we observed that problem?
3. Can an existing component solve it?
4. How will we know the new component improved the system?
5. What new failure modes or operational costs does it introduce?

Avoid speculative architecture whose primary justification is that it may be
useful later.

---

## 4. Validate Uncertainty Early

Identify assumptions that could invalidate the proposed design and test them
before investing heavily in implementation.

Examples include:

- Does the required API expose the needed data?
- Is the identifier stable and unique?
- Can two systems be reliably correlated?
- Is required historical data available?
- Can the event source trigger the intended workflow?
- Can the required evidence actually be retrieved?
- Is the intended decision measurable?

Prefer small feasibility experiments that answer specific questions.

A feasibility experiment should produce evidence, not merely code.

Record:

- hypothesis or question
- test performed
- evidence observed
- result
- limitations
- resulting decision

---

## 5. Separate Evidence, Extraction, Judgment, Policy, and Action

Avoid architectures where one opaque component performs the entire workflow.

Conceptually prefer:

raw evidence
→ extraction / normalization
→ derived features
→ assessment
→ confidence
→ policy
→ permitted action

These responsibilities may not require separate services or software
components, but they should remain conceptually distinguishable.

This allows each stage to be inspected, tested, replaced, and governed
independently.

Do not hide deterministic logic inside prompts when it can be represented
explicitly and tested directly.

---

## 6. Separate Judgment From Authority

A component that evaluates something should not automatically receive
permission to act on that evaluation.

Represent separately:

- what evidence exists
- what the system believes the evidence means
- how confident the system is
- what policy permits
- what action is authorized

A system may correctly determine that an action is desirable without being
authorized to perform it.

Likewise, greater model capability does not automatically justify greater
automation authority.

Authority must be intentionally granted.

---

## 7. Treat Uncertainty as Data

Do not force uncertain observations into false certainty.

Preserve uncertainty where it exists.

Distinguish, where practical:

- known facts
- derived facts
- assumptions
- probabilistic assessments
- missing evidence
- conflicting evidence

Confidence should influence policy.

For example:

high significance + low confidence
may justify asking or investigating

rather than:

high significance
therefore act

When uncertainty is decision-relevant, expose it rather than hiding it behind
a definitive answer.

---

## 8. Earn Automation Authority

Increase automation authority only after the preceding level demonstrates
sufficient reliability for the intended use.

A useful conceptual progression is:

observe
→ recommend
→ ask
→ act

Possible implementations may include:

- passive observation
- shadow evaluation
- recommendations to a human
- human-approved actions
- narrowly scoped automatic actions
- broader governed automation

Do not interpret this progression as a mandatory project lifecycle. It is a
principle for controlling authority.

The acceptable level of automation should depend on:

- consequence of error
- reversibility
- confidence
- historical performance
- observability
- available safeguards

Actions with substantial consequences should earn a higher evidence threshold.

---

## 9. Design the Feedback Loop Before Learning From It

Where a system makes judgments or recommendations, determine how those
judgments can eventually be evaluated.

Possible feedback signals include:

- accepted recommendation
- rejected recommendation
- corrected assessment
- successful action
- failed action
- analyst/user override
- dismissed notification
- explicit usefulness feedback
- 