# Decision Brief 003 — Design Batching and the Executable-Queue Pipeline

**Date:** 2026-07-05
**Source:** Consuming project's velocity realization, routed here as playbook intake; mechanisms adapted from a public reference repo (leogodin217/leos_claude_starter, reviewed 2026-07-05)
**Status:** Approved for integration
**Instruction to Claude Code:** Read this brief and the current playbook in full. Integrate the decisions below into the playbook. This brief is the spec; do not re-litigate the reasoning, but do flag any direct contradiction with existing playbook content before writing.

---

## Context

Two intake streams converged on the same session.

**The realization (consuming project).** The operator's goal is velocity, and the pipeline stalls wherever a build hits an undesigned decision — every design so far has needed a dedicated interview session, discovered mid-build. The fix: batch **all** remaining design and planning into a short sprint of interview-driven design sessions up front, so the entire build queue becomes executable without an operator decision mid-build. The operator's remaining mid-build role is acceptance testing — verifying by using what was built — which is async and never blocks a build.

**The reference repo.** A public Claude Code starter (leogodin217/leos_claude_starter) encodes a mature build pipeline: interview-driven design with an explicit human checkpoint, sprint specs derived from design docs, an adversarial spec review *before any code*, a fully automated build with the operator as final acceptor, and layered post-build verification. Its mechanisms are further along than ours. Its *timing philosophy* is the opposite of the realization above: "last responsible moment" design, staggered across the build, with the implementer instructed to "ask if unclear."

That collision is not a contradiction — it is the same tradeoff under two cost structures. A developer operator answers a mid-build question in minutes, so deferring design until context is richest is cheap and correct for them. A non-developer operator answers the same question with a dedicated interview session, so every deferred decision is a stalled build. The playbook's operator is the second kind. We therefore adopt the repo's **mechanisms** and invert its **timing**: all design moves ahead of the build queue, and a gate verifies the batching actually worked.

## Decisions

### 1. Adopt: the Design Sprint — a new pipeline stage

The pipeline gains a stage: **Phase 0 → Session 0 → Design Sprint → build sessions → async acceptance.**

The Design Sprint is a short run of interview-driven design sessions covering the entire Now/Next build queue. For each design: the operator approves a plain-language **Problem + Solution** statement first — the interview does not proceed past it until the operator confirms the direction — and Claude Code then writes the full design doc (rationale, behavior semantics, constraints, what doesn't change). Design interviews are full-tank work: they run at session start, never at wrap (Brief 001's energy-cycle principle applies).

The sprint's exit condition is Decision 3's gate, not a session count: the sprint is done when every queued slice passes.

### 2. Adopt: the WHY/WHAT split — design docs and build specs

Each design doc (the WHY) yields a **build spec** (the WHAT): contracts, phases, and plain-language acceptance criteria. Claude Code derives build specs without operator time. The two documents never duplicate content — the design doc carries rationale and constraints; the build spec carries what a build session executes and how done is measured. One document feeds the interview; the other feeds the build.

### 3. Adopt: the readiness gate — adversarial review before any build

Before a slice may enter a build session, a fresh-context adversarial review examines its build spec and design doc with one charter: **find the undesigned decisions.** Ambiguity, unstated assumptions, weasel words ("appropriate," "as needed," "etc.") are findings. The gate runs as a subagent swarm on the fast-execution tier (Brief 002 routing).

Findings do not go to the builder — they become the **agenda for the next design interview**. A slice passes when the gate finds nothing left undesigned. This makes the Design Sprint's claim — "no build will stall on a missing decision" — checkable instead of hoped.

### 4. Adopt: the gate-escape policy — reversible default, log, keep building

If a build still hits an undesigned decision despite the gate, the build **never asks the operator mid-build**. It takes the safest easily-reversible choice, logs it prominently (STATUS open questions + the wrap-up audit entry), and keeps moving. The escape is triaged at the next `/resume`, full-tank, where a wrong default costs one revert. (Operator decision, 2026-07-05.) This lands as a ground rule in `CLAUDE.template.md` — rules live where the model reads (Brief 002, Decision 3).

### 5. Adopt: behavioral spec-fidelity verify — the second verification layer

Brief 002's independent review swarm catches sloppy work. It does not catch correct-looking work that does the wrong thing. Before a build is called done, a second pass extracts every requirement from the build spec into a checklist and traces each one through the built behavior — the spec is the oracle. Same swarm routing: fast tier, adversarially verified.

Swarm hardening adopted alongside: fixed prompt templates for swarm subagents, caps on subagent output length, and a no-repeated-file-reads rule — the swarm's cost discipline, from the reference repo's context-budget engineering.

### 6. Adopt: the acceptance script — how a non-developer accepts a build

After verification, Claude Code generates a plain-language checklist from the build spec's acceptance criteria: *"try these N things."* The operator accepts by **using the app**, async, on their own schedule. Three outcomes, all expressed behaviorally: accept; "behavior X is wrong" (routes to the fix queue); roll the slice back (Claude Code does all git work). The operator never reads diffs, coverage, or reviewer output. This replaces the reference repo's accept/fix/reset decision, which assumed a diff-reading operator.

### 7. Adopt: a build-orchestrator row in model routing

The model-routing table gains a row for the **build-session orchestrator** — the driver of a gated, spec-executing build. Because the readiness gate has already removed the judgment calls, the orchestrator's job is routing and sequencing, not design: an agentic-workflow-tuned middle tier fits, and the expensive tier is reserved for the interviews and design work where a mistake is costly. *(Names as of 2026-07: middle agentic tier = Sonnet 5. Tiers INVARIANT, names PARAMETER, per the routing template's convention.)*

## Declined: last-responsible-moment design timing

- **Practice:** Defer each design decision until just before the code that needs it — the reference repo's core doctrine, and a defensible mainstream position ("design when you have enough context to decide well — not before, not after").
- **Why declined:** It prices mid-build questions at a developer's cost (minutes) rather than this playbook's operator cost (a dedicated interview session per question). Under the playbook's cost structure, deferred decisions are stalled builds; batching design up front, with the readiness gate verifying completeness, buys velocity precisely where this operator loses it.
- **Revisit if:** the operator profile changes to someone who can answer design questions mid-build cheaply (e.g., a developer adopts the playbook), or dry-run evidence shows batched designs going stale faster than builds consume them.

## Verification

Behavioral, on the consuming project's next cycle: (1) the Design Sprint runs and the readiness gate passes the whole queued slate; (2) the builds that follow complete with **zero mid-build operator interviews**; (3) any gate escape appears in STATUS/audit and is triaged at the next `/resume` rather than having interrupted a build; (4) the operator receives an acceptance script and can act on it without reading any engineering artifact. If builds still stall on undesigned decisions, the gate's charter wording is the first suspect — a detection failure, not a batching-design failure.
