# The Playbook

How Matt builds software with Claude Code: a non-developer operator describes behavior, Claude Code maintains everything — every file, every schema, every line — and a small set of documents carries all of the project's memory. Distilled from a proven project after a string of failed 0-to-1 attempts; maintained here as a living system with a paper trail for every change.

---

## 1. What this is

This repo is the playbook, shipped as an installable Claude Code plugin (Brief 004). It contains the plugin (`plugin/` — the `/new-project`, `/resume`, and `/wrap-up` commands plus the bundled templates in `plugin/templates/`, with their own README for adopters), this connective document, and the amendment archive (`dogfood/briefs`). It is a docs-only project: no application code, ever.

The unit of adoption is the plugin, not the repo (Brief 004): a teammate installs it once — two `/plugin` commands, listed in the README — and `/new-project` works in any directory. Reading this document is optional depth, never a prerequisite to start. A future project consumes the playbook through the pipeline below, the way the source project consumed its founding playbook. This repo also runs its own document system on itself — same files, same rituals, fenced in `dogfood/` (Brief 004, Decision 5).

## 2. The pipeline

**Phase 0 → Session 0 → design sprint → build sessions → async acceptance.** (Stages 3–5 reshaped by Brief 003.)

1. **Phase 0 — founding** (`/new-project`, run in Code **from the directory where the project will live** — Brief 004; Brief 005). The founding conversation defined in `plugin/templates/PHASE-0.md`: entry path first (discovery sprint / one-liner / point at context files — and a non-empty directory is never assumed to mean adoption; the command asks; Brief 005, Decisions 2–3), then retro on prior build failures, behavioral vision, personas (including the operator profile — elicited by the interview, never hand-edited; Brief 004, Decision 3), scope negotiation, excavation. Exit when Session 0's placeholder contract is satisfiable without invention. Output, in place: an instantiated build playbook, `SESSION-0-PROMPT.md`, and the file-definition templates — each file where convention puts it, layout confirmed at the checkpoint (Brief 005, Decision 1). Founding artifacts only — never product files. Existing projects can adopt the playbook the same way: same command, adoption mode.
2. **Session 0 — kickoff** (fresh Code session in the new repo). Consumes `SESSION-0-PROMPT.md`: domain interview, data-model checkpoint, then the working docs get written and committed. No product code that day.
3. **Design sprint** (Brief 003). A short run of interview-driven design sessions covering the entire Now/Next build queue — full-tank work, run at session start. Per design: the operator approves a plain-language **Problem + Solution** before anything else is written; Code then writes the design doc (the WHY — rationale, behavior semantics, constraints, what doesn't change) and derives the build spec (the WHAT — contracts, phases, plain-language acceptance criteria), with no duplication between the two. Exit is the **readiness gate**, not a session count: a fresh-context adversarial swarm (fast-execution tier, Brief 002 routing) hunts undesigned decisions — ambiguity, unstated assumptions, weasel words — in every spec. Findings become the next interview's agenda; the sprint is done when every queued slice passes. Full mechanics in `plugin/templates/design-sprint.template.md`.
4. **Build sessions** (the project's own repo, per its instantiated playbook). Only gated slices enter a build, and a build never asks the operator mid-build: an undesigned decision that escaped the gate gets the safest easily-reversible default, a prominent log (STATUS open questions + audit entry), and the build keeps moving — triaged at the next `/resume` (Brief 003). `/resume` to start, "add to Later" during, "wrap up" to end. Thinking sessions for SPEC-changing decisions; retros on a schedule; design moments per-screen for UI projects.
5. **Async acceptance** (Brief 003). After the verify layers pass, Code generates the **acceptance script** — a plain-language "try these N things" checklist drawn from the build spec. The operator accepts by using the app, async, never blocking a build: accept; "behavior X is wrong" (routes to the fix queue); or roll the slice back (Code does all git work). The operator never reads diffs, coverage, or reviewer output.

Chat's role: pressure-tests and meta thinking only. Its output lands here as decision briefs — never as artifacts imported into a project.

## 3. Principles

1. **The repo is the only source of truth.** Nothing is real until it's in a file in the repo. Ideas travel as short instructions to Code, never as artifacts to import.
2. **Minimize the rooms where truth is interpreted.** One repo, one tool that reads and writes it, one person who approves.
3. **Behavior is the fixed point; implementation is negotiable.** The named core rule and key workflows are the product; layout, stack, and structure serve them.
4. **The operator never touches schemas, foreign keys, or code.** Matt describes behavior, verifies by using what was built, and answers questions. Code translates and explains back in plain language.
5. **Restart cost must be near zero.** The project carries its own memory; the operator is not the state-carrier — which is exactly why Code can clear or compact its own context freely and reload from the repo (Brief 006, §7).
6. **Design rituals for the brain that will run them, not the brain that designed them.** (Brief 001.) Session-end rituals are run by depleted-you and must require zero judgment. Judgment-demanding steps belong at session start, when the tank is full. The human's cognitive state is part of the system — any recurring ritual declares *when in the operator's energy cycle it runs* and demands no more judgment than that moment affords.

## 4. The operator's job description (the whole thing)

- Run `/resume` to start a session, "wrap up" to end it.
- Read STATUS.md's plain-language sections; answer its open questions between sessions.
- Guard the Now list; park everything else in Later.
- Describe behavior; verify by using what was built.
- Sit the design-sprint interviews; approve each design's plain-language Problem + Solution (Brief 003).
- Work the acceptance script when one lands — try the listed things in the app, async, on your own schedule (Brief 003).
- Approve SPEC changes; notice when Code announces one.
- Show up to the scheduled retro even when things feel fine.

Nothing on this list requires reading code. That's not a simplification — it's the design.

## 5. The document system

Every project maintains these files, defined in `plugin/templates` (one `.template.md` per file, each with its job, conventions, and skeleton):

| File | Job |
|---|---|
| SPEC.md | Behavioral constitution — personas, user stories, the named core rule, non-goals. Changes rarely. |
| SCOPE.md | Now / Next / Later. Every new idea lands in Later first. The project's backlog lives here. |
| CLAUDE.md | Claude Code's standing instructions — the discipline enforcer. |
| DATA-MODEL.md | Schema + plain-language half. Only for projects with persistent data. |
| STATUS.md | Product memory — the state-carrier. Updated every session. |
| JOURNAL.md | Process memory — append-only, dated, never rewritten. |
| AUDIT.md | Wrap-up self-audit capture, read only at the next `/resume`. Added by Brief 001. |

Projects that run the design sprint also carry two per-slice documents — the design doc (WHY) and the build spec (WHAT), never duplicating each other — defined in `plugin/templates/design-sprint.template.md` (Brief 003).

**INVARIANT** parts keep their substance in every project; **PARAMETER** parts are per-project decisions. The layered memory pattern (root CLAUDE.md as always-loaded charter; optional nested per-folder CLAUDE.md → AGENTS.md via `@`-import; root precedence) is INVARIANT — whether and where to nest is PARAMETER. Details in `plugin/templates/CLAUDE.template.md`.

**Write authority:** Claude Code is the sole writer of every file, in projects and in this repo. Matt approves changes and answers questions; he never edits by hand.

## 6. Rituals

Each ritual declares when in the operator's energy cycle it runs, and demands no more judgment than that moment affords (Brief 001).

**`/resume` — session start, full tank.** Reads the most recent AUDIT.md entry *first* and triages it with the operator before new work begins — the fresh-eyes review of the prior session, gained for free by putting triage at session start (Brief 001). Routing: **fix now** (correctness, SPEC drift, scope violations — these compound), **backlog** (→ SCOPE.md Later), **playbook intake** (process learnings → routed out of the project repo, to this repo). Then reads SPEC/SCOPE/STATUS, reports state in plain English, proposes the session goal.

**"Add to Later" — during the session.** Every new idea goes to SCOPE.md's Later bucket, attributed and dated. Nothing moves up without the operator saying "promote X." The backlog absorbs scope creep.

**"Wrap up" — session end, empty tank.** Pure capture, zero operator judgment (Brief 001). Code: runs the project's checks and records outcomes; updates STATUS.md; appends the JOURNAL.md entry; writes the self-audit to AUDIT.md under the output contract (§10); commits. The operator's only job is to say "wrap up" — nothing to read, nothing to decide. Open questions are captured for the next `/resume`, never posed at session end.

## 7. Model routing

**Match the model to how expensive a mistake is, not how hard the task feels.** The table — tiers INVARIANT, names PARAMETER — lives in `plugin/templates/model-routing.template.md`. The routing works because the files exist: fast cheap models are safe exactly when the intelligence is stored in the repo instead of in the model's improvisation.

The table's rows describe the **driver** model. Subagent swarms — review finders, verify passes, and the readiness gate — route independently: fast-execution tier, never the session model (Brief 002; extended by Brief 003). The review practice itself (the independent multi-angle review before any real-data build is called done) is codified in `plugin/templates/build-playbook.template.md` and enforced as a ground rule in `plugin/templates/CLAUDE.template.md`, because a rule only bites if it lives in a file the model reads every session (Brief 002).

Two routing consequences of the design sprint (Brief 003): design-sprint interviews ride the most capable tier — design errors compound into every build they feed, the same stakes as Session 0 — while the build-session driver stays on the fast-execution tier with even more confidence than before, because the readiness gate has already removed the judgment calls; what remains is routing and sequencing against a gated spec.

**Session economy — the same rule on two more axes (Brief 006).** Model routing matches the *tier* to how expensive a mistake is; session economy matches *context size* and *subagent count* to the same standard, and it is a consequence of Principle 5, not a bolt-on: because the repo carries the memory, clearing context loses nothing that matters. Code-side defaults, invisible to the operator (never on §4's job list): **`/compact`** when context crosses a heavy threshold mid-session, **`/clear`** when switching to an unrelated task. And a subagent *budget* on top of the tier routing — the swarms stay cheap (above), but the prior question is whether the work needs a subagent at all: each is its own request stream, so spawn deliberately, never reflexively for work the driver could do inline. The codified swarms (review finders, verify pass, readiness gate) are deliberate by construction; the budget targets ad hoc fan-out.

**One routing doctrine — pattern + model + effort per task (Brief 007).** Briefs 002 and 006 each covered a slice: the swarm tier, the spawn budget. Brief 007 unifies them into a single judgment-based doctrine: for every task, pick the **cheapest combination of execution pattern (inline → single agent → swarm/workflow), model tier, and reasoning effort that gets full quality** — escalating only when stakes or difficulty demand. Fan-out is neither forbidden nor default; it is reserved for what earns it (real-data review gates, audits, batch builds). Small well-defined work routes to the fast/cheap tiers at low effort; judgment, integration, and spec work stay on the most capable tier; hard verify/judge passes get the second tier. And the enforcement rule: **every delegated agent gets model and effort set explicitly at spawn** — a spawn with no override silently inherits the session model at default effort, the failure mode Brief 007 closes. Enforced as ground rules in `plugin/templates/CLAUDE.template.md` and this repo's own `CLAUDE.md`, because a rule only bites where the model reads it (Brief 002); tier assignments and current model names live in `plugin/templates/model-routing.template.md`.

## 8. The slice method

Slice 1 proves the core rule on hand-entered data; later slices feed or consume it; circular dependencies break by entering data by hand first. Full method — with its provenance caveat — in `plugin/templates/slice-method.template.md`.

## 9. Failure tripwires

From the source project's retros. Watch for:

- Sessions starting without `/resume` → duplicated or drifting work.
- Mid-slice scope creep ("it felt quick").
- The operator re-explaining something twice → SPEC.md is ambiguous; fix the file, not the conversation.
- A week away feeling like a cold start → STATUS.md discipline has slipped.
- Importing artifacts instead of issuing instructions → the drift machine is back.
- Reflexive subagent fan-out for work the driver could do inline → cost with no coverage gain (Brief 006).
- Optimizing a session-opening command because usage is billed to it → the attribution trap; the opener's cost is the session's cost, not the command's (Brief 006).

## 10. The audit output contract (Brief 001)

The wrap-up self-audit ("what are you least confident about; what might be missing") is governed by a contract encoded in the wrap-up command itself:

- Every audit item MUST name a specific file or behavior AND a concrete check that would settle it ("run X; if it prints Y, we're fine").
- Items that cannot produce a falsifiable check are labeled **speculation** and auto-routed to backlog. Speculation never enters the fix-now queue.
- **"No material gaps" is a correct and expected output when the work is clean. Do not manufacture items.**

A language model cannot be made deterministic, but the ritual can be: fixed steps, fixed output format, falsifiability required, silence permitted. Filler is filtered structurally instead of relying on a depleted operator to detect it.

## 11. Declined practices log

Practices evaluated and rejected, kept so they aren't re-litigated from scratch. Format: practice / why declined / revisit if. Entries land here via decision briefs.

**Last-responsible-moment design timing** (Brief 003)
- **Practice:** Defer each design decision until just before the code that needs it — a defensible mainstream doctrine ("design when you have enough context to decide well — not before, not after"), encoded in a public reference repo reviewed 2026-07-05.
- **Why declined:** It prices mid-build questions at a developer's cost (minutes) rather than this playbook's operator cost (a dedicated interview session per question). Under this cost structure, deferred decisions are stalled builds; batching design up front — with the readiness gate verifying completeness — buys velocity exactly where this operator loses it.
- **Revisit if:** the operator profile changes to someone who can answer design questions mid-build cheaply (a developer adopts the playbook), or dry-run evidence shows batched designs going stale faster than builds consume them.

**Interactive session-end critique** (Brief 001)
- **Practice:** Interactive self-audit at session close ("what are you least confident about," operator triages live) — a community-popular pattern.
- **Why declined:** Assigns an evaluation task to the operator at peak depletion; demand characteristics of the question produce confabulated gap lists indistinguishable from real misses; the questions' value is preserved in the split ritual (§6, §10) without the flaw.
- **Revisit if:** the operating pattern changes such that sessions routinely end with judgment intact (e.g., timeboxed sessions ended by clock, not fatigue).

Phase-local declines (e.g. Phase 0's no-founding-brainstorm rule) live in their phase docs; this log holds the project-wide ones.

## 12. Decision briefs — how this playbook changes

- **Thinking happens elsewhere; writing happens here.** Pressure-tests run in the Chat thinking project; each one ends in a decision brief. Claude Code integrates the brief against the current playbook — it is the sole writer of playbook files.
- **Briefs are filed unmodified in `dogfood/briefs`**, numbered, and never edited after filing. The brief is the spec; Code does not re-litigate its reasoning, but flags any direct contradiction with existing content before writing.
- **Provenance:** every playbook section derived from a brief cites its number ("Brief NNN"), so every rule keeps a paper trail to its reasoning.
- **Protection:** `plugin/templates` and this file never change without Matt's explicit approval, and playbook changes require a filed brief.
