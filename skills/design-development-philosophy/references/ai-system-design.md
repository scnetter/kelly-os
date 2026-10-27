# AI System Design (reference)

Read this before proposing that a model, agent, or automation takes an action,
or when designing an AI or agentic pipeline. It expands principles 2, 5, 6, 7,
and 8 of the core skill.

---

## The pipeline, stage by stage

| Stage | Question it answers | Usually deterministic? | Test it by |
|---|---|---|---|
| Raw evidence | What actually happened / what do we have? | Yes | Fixtures, replay of real inputs |
| Extraction / normalization | What are the fields, entities, identifiers? | Mostly | Schema validation, golden files |
| Derived features | What facts follow from the evidence? | Yes where defined | Unit tests on known cases |
| Assessment | What do we believe it means? | Often probabilistic | Labeled set, baseline comparison |
| Confidence | How sure are we, and why? | Mixed | Calibration on history |
| Policy | Given belief + confidence, what is allowed? | Yes | Table-driven tests |
| Permitted action | What may be done, by whom? | Yes | Authorization tests |

Stages can live in one process. What matters is that each stage's output can be
inspected and each can be replaced without rewriting the rest.

Anti-patterns:

- One prompt that reads raw evidence and returns an action.
- Deterministic rules hidden inside a prompt ("if the sender domain is X,
  always...") instead of code with a test.
- A confidence number with no record of what it was based on.
- Policy that lives in the model's instructions rather than in code or config
  a human can review.

---

## Where the LLM belongs

Good fits: classifying ambiguous text, summarizing, extracting meaning from
unstructured input, resolving references, explaining a decision from recorded
inputs, proposing hypotheses for a human or a deterministic check to confirm.

Poor fits: identifiers, equality, arithmetic with a defined answer, schema
conformance, authorization, enforcing safety boundaries, anything where a
wrong answer must be impossible rather than unlikely.

Hybrid rule of thumb: let deterministic evidence constrain probabilistic
reasoning, then validate the model's output deterministically where possible
before policy sees it.

---

## Judgment versus authority checklist

Before a component is allowed to act, record:

1. **Evidence**: what inputs it used, retained for review.
2. **Belief**: what it concluded.
3. **Confidence**: how sure, and on what basis.
4. **Policy**: which rule permits the action at this confidence.
5. **Authorization**: who or what granted that rule, and when.
6. **Reversibility**: can the action be undone, and how fast?
7. **Blast radius**: what is the worst plausible outcome if it is wrong?

If any of 4 to 7 is unknown, the component may recommend or ask, not act.

---

## Authority levels

| Level | The system... | Typical evidence to move up |
|---|---|---|
| Observe | records and assesses silently | assessments look sane on history |
| Recommend | shows a suggestion; human decides | acceptance rate high, overrides understood |
| Ask | proposes a specific action; human approves | approved actions rarely reversed |
| Act (narrow) | acts within a tight, reversible scope | low error rate, fast rollback, monitoring |
| Act (broad) | acts under governed policy | sustained record, audit, clear kill switch |

Authority can also move down. A regression, a new input type, or a changed
consequence profile is a reason to step back a level.

---

## Context, not just events

The same event can matter differently depending on people, systems, assets,
goals, commitments, prior events, and the opportunity to act. Prefer models
that preserve these relationships over flattening everything early into
independent scores. Flatten only at the last responsible moment, and keep the
inputs that produced the score.
