# Evaluation (reference)

Read this before designing a feasibility spike, an evaluation, a feedback loop,
a rollout from shadow to automated operation, or a decision record. It expands
principles 4, 9, 10, 16, and the feedback and historical-evaluation guidance
from v0.1.

---

## Feasibility spike record

A spike produces evidence, not merely code. Record:

- **Question / hypothesis**: one sentence.
- **Why it matters**: what design decision depends on it.
- **Test performed**: exactly what was run, against what.
- **Evidence observed**: outputs, logs, screenshots, counts.
- **Result**: confirmed / refuted / inconclusive.
- **Limitations**: what the test did not cover.
- **Decision**: what we will do differently because of it.

---

## Baseline comparison

Pick the baseline before building the clever version:

- existing human workflow
- deterministic rules
- recency or urgency ordering
- simple heuristics
- direct LLM judgment with no extra architecture

Define the success criterion before looking at results. Compare on the same
inputs. If the sophisticated system does not beat the baseline by enough to
justify its cost and new failure modes, keep the baseline. Record negative
results; they are evidence too.

A distinguishing experiment, where practical:

baseline vs simple deterministic vs LLM-only vs structured hybrid

---

## Historical evaluation, then shadow, then live

1. **Historical**: replay past data. Cheap way to find systematic errors,
   missing features, odd edge cases, bad thresholds, weak correlations, and
   unnecessary complexity. It does not prove future reliability.
2. **Shadow**: run live alongside the current process with no authority.
   Compare its outputs to what humans actually did.
3. **Supervised**: human approves each action.
4. **Narrow automation**: only after the earlier stages produce evidence that
   matches the consequence of error.

---

## Feedback loops

Decide how judgments will be evaluated before building anything adaptive, and
define what "successful" means first.

Possible signals: accepted or rejected recommendation, corrected assessment,
successful or failed action, override, dismissed notification, explicit
usefulness rating, final verified disposition.

Behavior is not ground truth. A dismissal may mean irrelevant, badly timed,
misunderstood, inconvenient, or wrong. Keep enough context with each signal to
tell these apart, and prefer verified outcomes over inferred ones.

---

## Decision record (lightweight ADR)

File as `decisions/NNNN-short-title.md`:

- **Status**: proposed / accepted / superseded by NNNN
- **Decision**
- **Context**
- **Alternatives considered**
- **Evidence**
- **Reason**
- **Trade-offs**
- **Revisit if**: the conditions that would reopen it

Write one when the reasoning would otherwise be lost. Skip it when it wouldn't.
