# Decision Brief 006 — Session Economy: Context and Subagent Discipline as a Consequence of Restart-Cost-Zero

**Date:** 2026-07-13
**Source:** Session — usage-panel analysis 2026-07-13. Matt's weekly usage panel flagged `/resume` as a heavy skill ("scope down or run a cheaper model via skill frontmatter"). Analysis found the flag is *session-opening attribution*, not skill cost: `/resume` is a 13-line command reading four small docs (~173 lines total), with no large prompt and no spawned subagents. The panel's real signals — **90% of usage from subagent-heavy sessions**, **68% at >150k context** — point at drivers the playbook did not yet name.
**Status:** Decisions approved by Matt at plan review 2026-07-13; integrated the same session.
**Instruction to Claude Code:** Read this brief, the current `PLAYBOOK.md` §3/§7/§9, `plugin/templates/CLAUDE.template.md`, and `plugin/templates/model-routing.template.md` in full before integrating. This brief is the spec; do not re-litigate the reasoning, but flag any direct contradiction with existing content before writing.

---

## Context — what the usage panel surfaced

1. **The flagged skill was a phantom target.** The panel's own remediation tip ("scope down heavy skills / run a cheaper model via frontmatter") does not apply to `/resume`: it has no heavy prompt to scope and spawns no subagent to re-tier. The 41%-daily / 8%-weekly figure is the whole session's cost billed to whatever command *opened* the session. Optimizing the opener optimizes nothing.
2. **The playbook already tiers subagents but never budgets them.** §7 and Brief 002 route subagent swarms to the fast-execution tier — a cost-*per-request* lever. Nothing addresses subagent *count*: the reflexive fan-out that spends N request streams on work the driver could do inline. "90% subagent-heavy" is a count problem, not a tier problem.
3. **Long context is a cost the playbook is uniquely equipped to cut — and doesn't mention.** "68% at >150k context" is expensive even when cached. Principle 5 ("restart cost must be near zero — the repo carries its own memory") is exactly the property that makes aggressive context clearing safe, yet the playbook never draws the line from the principle to the practice.

## Decisions

### 1. Adopt: session economy is a first-class Code-side discipline, and it is a consequence of Principle 5

Because the repo is the state-carrier, Code can clear and compact its context freely and reload from `SPEC.md` / `SCOPE.md` / `STATUS.md` with near-zero loss. This is not a new principle bolted on for cost — it is what Principle 5 already guarantees, finally named on the cost axis. Session economy sits beside model routing (§7): routing matches model *tier* to how expensive a mistake is; session economy matches *context size and subagent count* to the same standard. Both are downstream of the file discipline.

### 2. Adopt: context-window defaults, operator-invisible

- **`/compact`** when context crosses a heavy threshold mid-session (the threshold is a PARAMETER; the practice is INVARIANT).
- **`/clear`** when switching to an unrelated task — the repo reloads the state that matters.

These are Code-side and never appear on the operator's job description (§4). Matt is never asked to remember, run, or approve them; they are hygiene Code performs on itself, the same way it manages its own tool calls.

### 3. Adopt: a subagent budget on top of tier routing

§7's tier routing stands unchanged — swarms stay on the fast-execution tier. This adds the prior question: **does the work need a subagent at all?** Each subagent is its own request stream; spawn deliberately, not reflexively. The named trap: fanning out finders/explorers for work the driver could do inline in less total cost. The review swarm and readiness gate (Brief 002/003) are deliberate by construction — this decision targets the *ad hoc* fan-out, not the codified swarms.

### 4. Adopt: the attribution caveat, as a failure tripwire

Usage attributed to a session-opening command (`/resume`) is not that command's cost — it is the session's cost billed to its opener. Chasing the label optimizes the wrong thing. Recorded as a tripwire so this exact investigation isn't re-run from scratch when the panel flags an opener again.

## Verification

- **Cross-reference:** every new "Brief 006" citation in `PLAYBOOK.md` resolves to this file; this brief's file references (`PLAYBOOK.md` §3/§7/§9, `plugin/templates/CLAUDE.template.md`, `plugin/templates/model-routing.template.md`) all exist.
- **Behavioral (the rule bites where the model reads it — Brief 002):** grep the changed files confirms the compact/clear + subagent-budget language appears in `plugin/templates/CLAUDE.template.md` and this repo's own `CLAUDE.md`, not only in `PLAYBOOK.md`.
- **Conventions:** INVARIANT/PARAMETER split intact in touched templates (the *practice* INVARIANT; the compact threshold PARAMETER).
- **Scrub:** changed files pass the `scrub-terms.local.txt` grep with zero hits.

## Relationship to existing scope

Extends Brief 002's routing model (tier-per-mistake-cost) onto two axes it didn't cover — context size and subagent count — and grounds both in Principle 5. Touches no operator-facing ritual: `/resume`, `/wrap-up`, and the operator's job description are unchanged. Explicitly does **not** modify `plugin/commands/resume.md` — editing the lean opener would be the phantom-target mistake Decision 4 warns against.
