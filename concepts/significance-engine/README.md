# Significance Engine

**Status: concept, untested hypothesis.** Nothing here is established
philosophy. Do not apply it as doctrine; treat it as an idea under development.

---

## The idea

Memory is not intelligence. Knowing what deserves attention is closer to
intelligence.

A Significance Engine is a layer above memory and capture that decides what
actually matters to a person (or an organization) in context, as distinct from
what is urgent, recent, or statically "important".

## Core distinctions

- **Significance**: how much something matters in context.
- **Attention priority**: whether it is worth consuming human attention right
  now.
- **Urgency**: how soon something must happen. Neither of the above.

Something can be highly significant and still not deserve an interruption
today. Something urgent can be insignificant.

## Inputs (hypothesized)

- Stated values and goals
- Relationships (people, systems, assets)
- Commitments and their deadlines
- Consequences of acting or not acting
- **Regret cost**: high future regret with no deadline forcing it (calling a
  parent, renewing a document months early)
- Opportunity window: when action is possible or cheapest
- Confidence in the evidence
- Interruption cost and an attention budget
- Resolution and decay: whether the item is done, superseded, or stale

Modeled as a value graph rather than a flat priority list, so the reason an
item matters stays connected to what it matters to.

## Outputs

remember → surface → connect → prioritize → (eventually, with earned authority)
act

## Open problems

1. **Stated vs revealed values**: how to use behavior without letting it
   silently overwrite what the person said they value.
2. **Ground truth**: what counts as "it was right to surface this"?
3. **Cold start**: what works before the graph has history?
4. **Explainability**: every surfaced item must be able to say why, from
   recorded inputs.
5. **Paternalism**: suggest, explain, allow override.

## First experiment (proposed)

Offline evaluation on about one month of Kelly's own data (calendar, email,
tasks). Compare three rankers on the same items:

1. Urgency/recency baseline
2. LLM-only judgment ("what matters most here?")
3. Value-graph scoring

Criterion, defined up front: Kelly blind-rates the top N of each daily list for
"worth my attention today" and for "I'd regret missing this". The value graph
earns further work only if it beats both baselines by a margin worth its
complexity.

## Possible proving ground

SOC work: "operational significance" for alert and phishing-report
prioritization (PhishER Workbench), where verified dispositions provide better
ground truth than personal data does. Any work-derived notes must be
abstracted before landing in this public repo.

## Related philosophy

Draws on core principles 7 (uncertainty as data), 13 (attention is finite),
14 (resolution and decay), and 15 (stated vs revealed values) in
`skills/design-development-philosophy/`. Those principles stand on their own;
this concept is one attempt to build on them.
