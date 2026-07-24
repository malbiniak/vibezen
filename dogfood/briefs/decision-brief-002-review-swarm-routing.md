# Decision Brief 002 — Independent Review Swarms and Subagent Model Routing

**Date:** 2026-07-03
**Source:** Consuming project's post-mortem — a real-money cost failure surfaced in session review, routed here as playbook intake
**Status:** Approved for integration
**Instruction to Claude Code:** Read this brief and the current playbook in full. Integrate the decisions below into the playbook. This brief is the spec; do not re-litigate the reasoning, but do flag any direct contradiction with existing playbook content before writing.

---

## Context

At a consuming project's session end, Claude spontaneously ran an independent multi-angle review — eight finder subagents plus an adversarial-verify pass — before calling the build done. The review itself was correct practice: it caught real issues, and it is worth keeping as the standard for anything that writes real data. The cost was not correct: every subagent silently inherited the **session** model, so a disposable, high-volume, cross-checked review ran on the most expensive tier available.

Root cause, confirmed by exploration in that project:

- The review was a **convention, not a documented ritual** — its only record was a prose note in the project's STATUS file. It ran off the model's memory, not off any file the model reads.
- **No configuration anywhere set a subagent model**, so finder subagents silently rode the session model.
- The project's **model-routing table governed only the driver model** (the one conversation doing the work). It had no row for review or finder swarms.

One structural note: this is an instruction/documentation fix, not an enforceable config fix. There is no reliable settings knob to force a model onto inline-spawned subagents; Claude honors the rule when it authors the review, because it can pin each subagent with a model override. That is exactly why the rule must live in the documents Claude reads — see Decision 3.

## Decisions

### 1. Adopt: the independent multi-angle review as standard practice

Before any build that writes real data is called done: finder subagents review independently across **correctness / reuse / simplification / efficiency / altitude / conventions**, followed by an **adversarial-verify pass** over their findings. Timing is automatic — the review runs before "done" is declared, without the operator asking.

The finders are not the quality gate. The verify pass, the test suite, and the operator are the real gate; the finders exist to feed it cheaply and from many angles.

### 2. Adopt: swarm model routing — fast-execution tier, never the session model

Every review and verify subagent runs on the **fast-execution tier**. Finders are high-volume, disposable, and cross-checked; per-agent judgment matters less than cost, so the expensive model is wasted there.

Scope clarification this decision forces: the model-routing table's rows — and the "cheapest tier: never" default — describe the **driver** model. Subagent swarms route independently and cheaply. Cheap is *safe* here precisely because the intelligence lives in the repo and the verification structure, not in the individual finder. This is not an exception weakening the routing rule; it is the routing rule ("match the model to how expensive a mistake is") applied to a situation the table had been silent on.

*(Names as of 2026-07: fast execution = Sonnet. The names age; the rule doesn't — tiers INVARIANT, names PARAMETER, per the routing template's own convention.)*

### 3. Adopt as playbook principle: rules live where the model reads

A routing or ritual rule only bites if it lives in a file Claude reads every session — the project's `CLAUDE.md`, the always-loaded charter. A convention living in the model's memory, in STATUS prose, or in a doc consulted occasionally will silently default to the expensive (or wrong) path, and no one notices until the bill arrives.

Consequence for integration: the swarm rule lands as a **ground rule in `CLAUDE.template.md`** (the enforceable home), with the rationale carried in the process docs (build playbook, model routing).

## Verification

Behavioral, on the next consuming-project session that runs the review: the swarm should be announced on the fast-execution model — visible in the run output — not the session model. If it silently uses the session model, the ground-rule wording in that project's `CLAUDE.md` needs to be blunter; the failure is a wording problem, not a routing-design problem.
