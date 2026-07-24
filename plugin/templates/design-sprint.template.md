# Design Sprint (template) — Brief 003

> **Template.** Consulted from the playbook repo; the doc skeletons below are copied into a project per slice as the sprint runs. The sprint loop, the gate, and the escape policy are **INVARIANT**; storage locations, session cadence, and the gate's swarm size are **PARAMETER**. Ritual timing follows Brief 001: design interviews are full-tank work — session start, never wrap.

Why this exists: the pipeline stalls wherever a build hits an undesigned decision, and for a non-developer operator every such decision costs a dedicated interview session. The sprint batches all of that design up front and then **proves** the batching worked, so the entire build queue becomes executable with zero mid-build operator decisions. (Brief 003; the deliberate inverse of last-responsible-moment design — see PLAYBOOK.md's declined-practices log.)

---

## The sprint loop (INVARIANT)

Run interview sessions until the whole Now/Next queue is gated. Per design, in order:

1. **Problem + Solution, approved first.** Code proposes a plain-language statement of the problem and the intended solution. The interview does not proceed until the operator confirms the direction. No document is written before this.
2. **Design doc** (the WHY) — written by Code from the interview.
3. **Build spec** (the WHAT) — derived by Code, no operator time. The two documents never duplicate content.
4. **Readiness gate** — the adversarial pass below. Findings become the agenda for the next interview session; a slice with zero findings is marked **executable**.

**Exit condition:** every queued slice is executable. The exit is the gate, not a session count or a calendar.

## The design doc (skeleton — the WHY)

```
# Design — <slice name>
*Approved Problem + Solution: <date>*

## Problem
<Plain language. What moment or behavior is broken or missing, for whom.>

## Solution
<Plain language. What the operator approved.>

## Behavior semantics
<How it behaves, stated as rules and moments — never as implementation.>

## Constraints and invariants
<What must always/never happen. Ties back to SPEC.md's core rule where relevant.>

## What doesn't change
<Adjacent behavior explicitly untouched — the gate checks builds against this.>

## Decisions resolved here
<Each formerly-open question and the decision, dated. This list is what the gate audits.>
```

## The build spec (skeleton — the WHAT)

```
# Build spec — <slice name>
*Design doc: <link>. Gate status: <pending | executable, date>.*

## Contracts
<What the built thing promises, behaviorally.>

## Phases
<Ordered build phases, each with plain-language acceptance criteria — "done when X behaves like Y.">

## Out of scope
<Named exclusions, so the builder can't drift into them.>

## Acceptance script seeds
<The "try these things" list the post-build acceptance script is generated from.>

## Definition of done
<Checks + verify layers + the acceptance script handed to the operator.>
```

## The readiness gate (INVARIANT)

A fresh-context adversarial swarm — fast-execution tier, never the session model (Brief 002 routing) — reads one slice's design doc + build spec with a single charter: **find the undesigned decisions.** It proposes no fixes and talks to no builder.

Findings include:
- Unstated assumptions and silent dependencies between slices.
- Ambiguity a builder would have to resolve by guessing.
- Weasel words: "appropriate," "as needed," "etc.," "handle gracefully," "robust."
- Terms the documents use but never define.
- Missing failure behavior (what happens when the input is wrong, empty, or hostile).
- Acceptance criteria that can't actually be checked by using the app.

Verdict per slice: **executable** (zero findings) or **findings → next interview's agenda**. There is no "pass with warnings."

## The gate-escape policy (INVARIANT)

If a build still hits an undesigned decision despite the gate, the build **never asks the operator mid-build**: take the safest easily-reversible choice, log it prominently (STATUS.md open questions + the wrap-up audit entry), keep building. The escape is triaged at the next `/resume`, full-tank, where a wrong default costs one revert. Repeated escapes mean the gate's charter needs sharpening — a detection failure, not a batching failure.

## Storage (PARAMETER)

Suggested: `design/<slice-slug>.design.md` and `design/<slice-slug>.spec.md` in the project repo. Any layout works if the build spec links its design doc and STATUS.md can point at the queue's gate state.

## Staleness tripwire

If reality changes designs faster than builds consume them — repeated gate re-runs invalidating executable slices — the batch size is too big for this project's volatility. That evidence routes to the playbook as intake (it is the "revisit if" condition on Brief 003's declined-practice entry).
