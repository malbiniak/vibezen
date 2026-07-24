# Decision Brief 001 — Split Wrap-Up Ritual

**Date:** 2026-07-03
**Source:** Playbook thinking project (Claude Chat) — pressure-test of r/ClaudeAI session-end questions thread
**Status:** Approved for integration
**Instruction to Claude Code:** Read this brief and the current playbook in full. Integrate the decisions below into the playbook. Where a section referenced here doesn't exist yet, create it. This brief is the spec; do not re-litigate the reasoning, but do flag any direct contradiction with existing playbook content before writing.

---

## Context

The practice under evaluation: ending every session with self-audit questions ("What are you least confident about?" / "What am I missing?"), popularized in a widely-upvoted r/ClaudeAI thread. Community consensus is strongly positive. Several refinements surfaced in the thread: requiring a verifiable test per uncertainty item, fresh-context review of prior output, and ending sessions by updating docs/memory files.

The pressure-test surfaced a design flaw specific to this operator's reality: **wrap-up happens at cognitive empty tank.** Sessions end when Matt's judgment is degraded. The Reddit pattern hands the operator an evaluation task (triage the model's uncertainty list) at exactly the moment the operator is least equipped to perform it. Additionally, the questions carry a demand characteristic — they imply a nonzero answer is expected — so the model will produce a plausible-sounding gap list even when the work is clean, and real misses read identically to filler. A tired operator cannot tell them apart.

## Decisions

### 1. Adopt: Split wrap-up ritual (capture at end, triage at start)

Split the ritual by who has to think.

**Session end — pure capture, zero evaluation.** Deterministic, mechanical steps only:

1. Update STATUS.md and JOURNAL.md per their existing definitions.
2. Run the self-audit questions (defined in Decision 2). Output goes to a dated audit section in STATUS.md (or a dedicated AUDIT.md — Code's choice, record the rationale). **The operator does not read the audit output at session end.**
3. Commit.

The operator's only job is to invoke the wrap-up command. No decisions, no triage, no reading comprehension required.

**Session start — evaluation, with fresh judgment and fresh context.** The `/resume` command reads the most recent audit output *first* and triages it with the operator before new work begins. The resuming session is a fresh context with no ego invested in the prior session's work — this is the fresh-eyes review mechanism, gained for free by moving triage to session start rather than running a separate review pass.

Triage routing at session start:

- **Fix now:** items touching correctness, drift from SPEC.md, or scope violations. These compound across session boundaries.
- **Backlog:** feature ideas, brainstorms, efficiency improvements → SCOPE.md "Later" or STATUS.md backlog section.
- **Playbook intake:** process learnings → routed out of the app repo entirely, to the playbook thinking project.

### 2. Adopt: Audit output contract (anti-confabulation)

The self-audit is governed by an output contract, encoded in the wrap-up command itself:

- Every audit item MUST name a specific file or behavior AND a concrete check that would settle it ("run X; if it prints Y, we're fine").
- Items that cannot produce a falsifiable check are labeled **speculation** and auto-routed to backlog. Speculation never enters the fix-now queue.
- The empty answer is explicitly authorized: **"No material gaps" is a correct and expected output when the work is clean. Do not manufacture items.**

Rationale: a language model cannot be made deterministic, but the ritual can be — fixed steps, fixed output format, falsifiability required, silence permitted. Filler is filtered structurally instead of relying on a depleted operator to detect it.

### 3. Adopt as playbook principle: Design rituals for the brain that will run them

New first-class principle:

> **Design rituals for the brain that will run them, not the brain that designed them.** Session-end rituals are run by depleted-you and must require zero judgment. Judgment-demanding steps belong at session start, when the tank is full. The human's cognitive state is part of the system.

This generalizes beyond wrap-up: any recurring ritual should declare *when in the operator's energy cycle it runs* and be designed to demand no more judgment than that moment affords.

### 4. Decline: Interactive session-end critique

The Reddit pattern as written — operator reads and weighs the model's uncertainty list at session end — is **declined**. Record in the declined-practices log:

- **Practice:** Interactive self-audit at session close ("what are you least confident about," operator triages live).
- **Why declined:** Assigns an evaluation task to the operator at peak depletion; demand characteristics of the question produce confabulated gap lists indistinguishable from real misses; value of the questions is preserved in the split ritual (Decisions 1–2) without the flaw.
- **Revisit if:** operating pattern changes such that sessions routinely end with judgment intact (e.g., timeboxed sessions ended by clock, not fatigue).

## Structural notes for the playbook repo (founding session only)

If this brief is being read at the playbook repo's Session 0, also establish:

- **Sections:** Principles · Rituals · Backlog · Declined Practices log · Decision Brief archive.
- **Write authority:** Claude Code is the sole writer of playbook files. Thinking happens in the Chat project; each pressure-test conversation ends in a decision brief like this one; Code integrates against the current playbook.
- **Provenance:** file this brief in the Decision Brief archive unmodified. Playbook sections cite the brief number they derive from, so every rule keeps a paper trail to its reasoning.
