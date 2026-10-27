# 2026-10-27: Is the philosophy skill too big?

## Observation

First real use of kelly-os surfaced a question about the
design-development-philosophy skill: 17.5 KB, 22 principles, mixing core
philosophy, detailed guidance, and concept material.

The skill is being asked to obey itself: principle 3 (complexity must earn its
place) and principle 22 (resist premature generalization) apply to the skill's
own shape.

## Hypothesis

A kernel with triggered references (v0.2) produces design advice at least as
good as the full file (v0.1), with clearer separation between philosophy and
untested ideas.

## Test (to run)

Same prompts, same model, two fresh sessions: one with v0.1, one with v0.2.

1. Should the PhishER classifier quarantine reported messages automatically?
2. I want to add a vector database so the agent remembers past tickets. Good
   idea?
3. Design a feature that tells me which emails I'll regret not answering.
4. We have a working rules-based triage script. Should we replace it with an
   LLM agent?

Criterion, set before running: for each answer, Kelly marks which applies the
philosophy better (asks for the problem and evidence, separates judgment from
authority, proposes a baseline or smallest test, flags uncertainty). Also note
whether the v0.2 session opened a reference file when its trigger applied
(prompts 1 and 4 should trigger ai-system-design.md; 2 and 4 should trigger
evaluation.md).

v0.2 is accepted if it wins or ties on at least 3 of 4 and reference loading
works when triggered.

## Result

_Not yet run._

## Principles exercised

3, 9 (baseline), 10 (smallest disproving test), 16 (record decisions),
17 (resist generalization).
