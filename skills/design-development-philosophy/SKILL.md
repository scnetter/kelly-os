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
- final verified disposition

Do not assume that observed user behavior automatically represents ground
truth.

For example, a dismissed recommendation may be irrelevant, inconvenient,
poorly timed, misunderstood, or incorrect.

Preserve enough context to distinguish useful feedback from ambiguous behavior.

Before implementing adaptive behavior, define what successful behavior means.

---

## 10. Evaluate Against a Baseline

A sophisticated system should demonstrate value compared with a simpler
alternative.

Depending on the problem, useful baselines may include:

- existing human workflow
- deterministic rules
- recency or urgency ordering
- simple heuristics
- direct LLM judgment without additional architecture

Ask:

> Does the proposed system produce a meaningful improvement over the simpler
> alternative?

If additional architecture does not improve the outcome enough to justify its
cost, prefer the simpler system.

A negative experimental result is useful information.

---

## 11. Prefer Historical Evaluation Before Live Authority

When historical data is available, use it to evaluate behavior before relying
on a system during live operation.

Historical evaluation can help identify:

- systematic errors
- missing features
- unexpected edge cases
- inappropriate thresholds
- poor assumptions
- weak correlations
- unnecessary complexity

Historical performance does not prove future reliability, but it can expose
weak designs cheaply before operational authority is granted.

After historical evaluation, prefer shadow or human-supervised operation before
high-consequence automation.

---

## 12. Treat Human Attention as a Finite Resource

Every:

- alert
- notification
- recommendation
- escalation
- confirmation request
- explanation

has a cost.

Do not optimize systems merely to identify or produce the maximum number of
technically relevant items.

Optimize for useful signal.

When evaluating a system, ask both:

> Was the system correct?

and:

> Was this worth putting in front of a human?

Where appropriate, model factors such as:

- significance
- urgency
- opportunity window
- confidence
- interruption cost
- consequence of delay

A correct notification delivered at the wrong time can still be a poor system
decision.

---

## 13. Model Context, Not Just Events

The significance of an observation may depend on its relationships to other
information.

Relevant context may include:

- people
- systems
- assets
- goals
- commitments
- previous events
- current projects
- historical behavior
- organizational value
- consequences
- available opportunities for action

Do not assume that an event has the same significance in every context.

Prefer models that preserve relationships rather than flattening everything
prematurely into independent scores.

---

## 14. Separate Significance From Attention Priority

Something can matter without deserving immediate interruption.

When relevant, distinguish:

**Significance**

How much does this matter in context?

from:

**Attention Priority**

Is this worth consuming human attention right now?

Attention priority may depend on significance plus factors such as:

- opportunity to act
- time sensitivity
- confidence
- interruption cost
- current context
- prior surfacing
- whether the issue has already been resolved

Do not equate significance with urgency.

Do not equate significance with notification priority.

---

## 15. Account for Resolution and Decay

Information should not remain indefinitely important merely because it was once
important.

Track whether an item has been:

- resolved
- superseded
- acknowledged
- acted upon
- made irrelevant
- changed by later information

Where appropriate, significance or attention priority should decay as context
changes.

A completed commitment should normally stop competing for attention.

New evidence may also increase significance rather than decrease it.

---

## 16. Distinguish Stated Values From Revealed Behavior

In systems designed around human preferences or organizational priorities, do
not assume that observed behavior perfectly represents underlying values.

Preserve the distinction between:

- stated priorities
- observed behavior
- inferred preferences

A difference between stated values and behavior may itself be useful
information.

Do not silently rewrite an explicit value merely because observed behavior
differs from it.

Avoid paternalistic behavior.

When priorities influence a recommendation, the system should be capable of
explaining why the recommendation was made and should permit human override.

---

## 17. Make Important Decisions Explainable

For consequential decisions, preserve enough information to answer:

- What evidence influenced this?
- What assumptions were made?
- Which rule or policy applied?
- What uncertainty existed?
- Why was this surfaced?
- Why was this action allowed or prevented?

An explanation should expose the decision process rather than merely generate a
convincing narrative after the fact.

Prefer explanations grounded in recorded decision inputs.

---

## 18. Build for Observability

A system that cannot explain what happened will be difficult to improve.

Preserve useful intermediate outputs so failures can be localized.

When practical, make it possible to determine:

- what entered the system
- what was extracted
- what rules were applied
- what external data was retrieved
- what the model produced
- what confidence was assigned
- what the policy decided
- what action occurred
- what feedback followed

Observability is part of the architecture, not an afterthought.

---

## 19. Build the Smallest Experiment That Can Disprove the Idea

When evaluating a new concept, ask:

> What is the cheapest credible experiment that could show this idea does not
> work?

Prefer experiments that distinguish between competing approaches.

For example:

baseline
vs.
simple deterministic model
vs.
LLM-only model
vs.
structured hybrid model

Define the evaluation criterion before interpreting the result.

Do not build the production architecture merely to test whether the underlying
idea has merit.

---

## 20. Preserve Reversibility

Early architectural decisions should be easy to change when evidence is weak.

Avoid premature commitment to:

- complex schemas
- generalized abstractions
- distributed services
- vendor-specific mechanisms
- learned models
- autonomous behavior

Prefer designs that allow components to be replaced as understanding improves.

Irreversible or expensive decisions require stronger evidence than reversible
ones.

---

## 21. Record Decisions and Their Evidence

Record significant architectural and product decisions when the reasoning would
otherwise be lost.

A lightweight decision record should generally capture:

- decision
- context
- alternatives considered
- evidence
- reason
- known trade-offs
- conditions that would justify revisiting it

Avoid documentation for documentation's sake.

Documentation is valuable when it preserves knowledge needed to understand,
operate, evaluate, or change the system.

---

## 22. Resist Premature Generalization

Do not create a generic framework solely from an attractive theory.

Patterns become reusable when they repeatedly survive practical application.

Before generalizing a technique, distinguish:

- what was hypothesized
- what was actually tested
- what worked
- what failed
- what was specific to the project
- what appears reusable across projects

Frameworks should emerge from evidence.

Do not force future projects to conform to abstractions created before enough
evidence existed to justify them.

---

# Decision Heuristics

When presented with competing designs, prefer the option that:

1. solves the demonstrated problem
2. tests the riskiest assumption early
3. introduces the least unjustified complexity
4. preserves inspectability
5. separates deterministic and probabilistic responsibilities
6. exposes uncertainty
7. preserves human authority where consequences justify it
8. produces measurable evidence
9. keeps important decisions reversible
10. can evolve when evidence changes

When these considerations conflict, explicitly identify the trade-off rather
than pretending there is a universally correct design.

---

# AI-Specific Guidance

Use an LLM where ambiguity, language understanding, synthesis, classification,
or contextual reasoning provides meaningful value.

Prefer deterministic software for:

- exact transformations
- stable identifiers
- equality and subset checks
- schema validation
- explicit business rules
- authorization
- enforceable safety boundaries
- calculations with defined answers

Hybrid systems are usually preferable when deterministic evidence can constrain
probabilistic reasoning.

A useful default pattern is:

deterministic acquisition
→ structured extraction
→ probabilistic reasoning where useful
→ deterministic validation where possible
→ explicit policy
→ controlled action

Do not ask an LLM to invent certainty where the underlying evidence is
incomplete.

---

# Working Style

When assisting with system design:

1. Identify the immediate question being solved.
2. Separate known facts from assumptions.
3. Identify the highest-risk unknown.
4. Recommend the smallest useful way to test it.
5. Avoid expanding scope unless the expansion solves an observed problem.
6. Preserve useful future ideas without allowing them to derail current work.
7. Prefer concrete evidence over architectural speculation.
8. Challenge complexity that has not earned its place.
9. Surface important trade-offs directly.
10. Revisit earlier decisions when new evidence materially changes the premise.

Do not optimize for producing the most sophisticated design.

Optimize for learning what is true and building the simplest system justified by
that evidence.

---

# Relationship to Project Delivery

This skill defines design and development philosophy.

It does not define a mandatory software-development lifecycle.

Practices such as:

problem definition
→ discovery
→ feasibility validation
→ walking skeleton
→ historical evaluation
→ shadow operation
→ assisted operation
→ governed automation

may be useful, but should not yet be treated as universal process requirements
solely because they worked for one project.

A reusable project-delivery framework should be extracted separately after
sufficient practical evidence exists to distinguish durable patterns from
project-specific circumstances.

---

# Core Principle

Build what the evidence justifies.

Understand it before making it clever.

Measure it before trusting it.

Let authority be earned.

And do not generalize from what sounds right. Generalize from what survives
contact with reality.