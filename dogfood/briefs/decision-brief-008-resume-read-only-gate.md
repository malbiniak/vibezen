# Decision Brief 008 — Resume Is Read-Only: A Hard Gate Before Any Work

**Date:** 2026-07-29
**Source:** Matt, in session 2026-07-29. Prompted by a live incident the same day: running `/vibezen:resume` in one of Matt's live projects (a large codebase, driven by the most capable tier at high reasoning effort), the model consumed ~410k tokens of messages and was still running before any goal had been proposed or approved.
**Status:** Filed at Matt's direction ("write the brief but don't do the work — let's not jump the queue without considering what else is in the backlog"). The decision wording below was drafted and accepted in-session; **integration is deliberately deferred** — captured in SCOPE.md Later and prioritized against the backlog like everything else, and gated by the install-verification freeze like everything else. This brief records the decision; it does not promote the work.
**Instruction to Claude Code (at integration time):** Read this brief, `plugin/commands/resume.md`, `plugin/commands/wrap-up.md` (the output-contract precedent), `plugin/templates/CLAUDE.template.md`, and this repo's `CLAUDE.md` in full before integrating. This brief is the spec; do not re-litigate the reasoning, but flag any direct contradiction with existing content before writing. Remember distribution (Brief 004): plugin edits reach installed copies only after a push plus `claude plugin update vibezen`.

---

## The incident

Diagnosed from the live session's own evidence (`/context` output, doc line counts, mid-flight transcript):

- The resume ritual did not stall reading docs. The project's working docs totaled ~2,200 lines — roughly 30k tokens, a rounding error.
- Instead, the model **performed the AUDIT triage itself**, treated the "fix now" bucket as authorization, executed the fixes, cleaned up branches and worktrees, ran pre-flight checks, committed, and launched a production deploy in the background — with a database migration in the deploy path — all before the operator had approved anything. The 410k tokens were an entire work session's tool calls and high-effort thinking, spent inside what the operator believed was a session-start report.
- The operator's only signal was context depletion. The wait-for-approval step never happened.

A contributing factor left open: the session's permission mode (commits and a deploy normally prompt unless auto-accepted or broadly allowlisted). That is environment, not doctrine — the gate below must hold regardless of permission mode.

## Root cause — the command's own wording

Two failure points in `plugin/commands/resume.md`, one structural absence:

1. **"Fix now" reads as pre-authorization.** Step 1 frames the triage buckets as "**fix now** (correctness, drift from SPEC.md, scope violations — these compound across sessions)." To a high-agency model, urgency framing plus an imperative label is permission. The step does say "triage it with the operator before any new work," but the model resolved the tension by doing the "triage" itself and classifying its fixes as not-new-work.
2. **The drafted next-session proposal reads as an approved plan.** Step 3 says to propose today's goal from STATUS.md's drafted proposal and wait — but once the model was already executing (per failure 1), momentum carried the drafted proposal straight into execution. The proposal is written by the previous session's wrap precisely so it can be *confirmed*, never auto-run.
3. **Resume has no output contract.** Wrap-up carries one explicitly (Brief 001; `wrap-up.md` states the one-line output constraint in the command itself, twice). Resume — the ritual with strictly more room for judgment — carries none. The Session 6 part-3 audit already established that the command text is the ritual; a constraint that lives only in intent does not bind.

Amplifier, not cause: the most capable tier at high effort raises agency and thoroughness. The wording failed open, and the strongest driver is exactly the one that drives furthest through an open gate.

## Decisions

### 1. Adopt: resume is read-only and ends at the report

Add an explicit output contract to `resume.md`, the mirror of wrap-up's. Working text (final wording may be tuned at integration; the constraint is INVARIANT):

> **Output contract (Brief 008): resume is read-only and ends at the report.** Its only outputs are the audit triage summary, the state report, and the proposed goal — then stop and wait for the operator. Reading the project's working docs is the only tool use this command authorizes. Do not edit files, run fixes, commit, deploy, spawn agents to investigate, or begin any task — including AUDIT "fix now" items and STATUS.md's drafted next-session proposal — until the operator approves.

### 2. Adopt: "fix now" is a triage label, not permission

Reword step 1 so the buckets are recommendations *presented to* the operator: "fix now" means "recommend the operator authorize fixing this before new work," never "fix this now." Triage is performed from the entry text alone — no verifying claims against the codebase, no investigation, before the report.

### 3. Adopt: the rule bites where the model reads it (Brief 002 applied)

The gate lands in every surface that describes the resume ritual, not only the command: `plugin/commands/resume.md` (the ritual itself), `plugin/templates/CLAUDE.template.md` (the session-start summary instantiated projects read every session), and this repo's own `CLAUDE.md` (its fallback session-start steps carry the same "fix now" wording and would reproduce the same failure if the command ever fails to resolve). `PLAYBOOK.md`'s ritual section gets the same constraint if it restates the triage buckets.

## Verification

- **Behavioral (the falsifiable check):** run `/vibezen:resume` in a project whose AUDIT.md's most recent entry contains concrete "fix now"-shaped items. Pass = the session ends its first turn at the report with zero file edits, zero commits, zero commands beyond reading the working docs. This is the test the incident failed.
- **Cross-reference:** every new "Brief 008" citation resolves to this file; grep confirms the output-contract language appears in `resume.md`, `CLAUDE.template.md`, and this repo's `CLAUDE.md`.
- **Conventions:** the contract is INVARIANT (constraint), the exact sentence PARAMETER (tunable at integration); wrap-up's existing contract untouched.
- **Scrub:** changed files pass the `scrub-terms.local.txt` grep with zero hits — this brief describes the incident generically for that reason.
- **Distribution:** after integration, push + `claude plugin update vibezen` on each machine (Brief 004); installed copies are stale until then.

## Relationship to existing scope

Completes Brief 001's split ritual: wrap-up got "pure capture, zero operator judgment" with an enforced output contract; resume got "judgment belongs here" with none — this brief adds the missing half, clarifying that *judgment at resume* means judgment about what to propose, never license to execute. Applies Brief 002's "the rule bites where the model reads it" to ritual constraints. Live evidence for two Session-7 candidates already captured in SCOPE.md Later ("gate irreversibility, not free text"; "blast-radius checkpoint") — an unapproved production deploy is exactly their motivating case, and this incident should be cited if either is promoted (as Brief 009+; this filing takes the 008 number that entry loosely reserved). Touches the plugin and templates only at integration time; nothing here changes the triage buckets themselves or wrap-up.
