# Instructions for Claude Code — The Playbook Repo

## Who you're working with

Matt is a Staff PM and a non-developer. He describes intent and behavior; you handle all translation. Never require him to read anything but plain language. He never edits files by hand — every file in this repo is written and maintained by you, with his approval.

## What this repo is

The playbook, shipped as an installable Claude Code plugin (Brief 004). The layout: the plugin (`plugin/` — the three commands plus the bundled templates in `plugin/templates/`, delivered by `.claude-plugin/marketplace.json` at the root), the process document (`PLAYBOOK.md`), and this repo's own self-application fenced in `dogfood/` (its working docs — `SPEC.md`, `SCOPE.md`, `STATUS.md`, `JOURNAL.md`, `AUDIT.md` — and the amendment archive `dogfood/briefs/`). Docs and plugin manifests only, forever. **If you find yourself drafting app features, product schemas, or code, stop — you have drifted out of this repo's scope.**

This repo's own working docs live in `dogfood/`, not the root — whenever a ritual or rule below names `SPEC.md`, `SCOPE.md`, `STATUS.md`, `JOURNAL.md`, or `AUDIT.md`, that means the copy in `dogfood/` (Brief 004, Decision 5). The `/new-project`, `/resume`, and `/wrap-up` commands come from the installed `vibezen` plugin — since 2026-07-24 installed from the published GitHub repo (`malbiniak/vibezen`), not referenced in place. **Edits to `plugin/` are no longer live:** they reach the installed commands only after a push plus `claude plugin update vibezen` (or a marketplace update).

## Session start

Sessions start by **invoking `/vibezen:resume` as a command** — not by performing its steps from this summary. The command is the ritual; this summary exists so you recognize it (Session 6 part-3 audit: performing the steps from here is running a copy of the ritual, not the ritual). If the command doesn't resolve, flag that to Matt first — it's a finding, not a detour — then follow the steps:

1. If `AUDIT.md` has entries, read the most recent one **first** and triage it with Matt before new work begins (Brief 001): **fix now** (correctness, drift from SPEC.md, scope violations — these compound), **backlog** (→ SCOPE.md Later), or already-routed speculation. If the entry says "No material gaps," say so in one line and move on.
2. Read `SPEC.md`, `SCOPE.md`, `STATUS.md`.
3. Report where things stand in plain English — including anything half-done if the last session ended early. Propose today's goal; wait for Matt to approve or redirect.

## Ground rules

- **Never modify `plugin/templates`, the plugin commands, or `PLAYBOOK.md` without Matt's explicit approval.** Playbook changes require a decision brief filed in `dogfood/briefs`; every section derived from a brief cites its number ("Brief NNN").
- **Privacy scrub is a product requirement** (see SPEC.md): this repo is public; every file carries zero project-private content. Before any commit, grep the changed files against `scrub-terms.local.txt` (gitignored, local-only — the term list itself must never be committed): `grep -v '^#' scrub-terms.local.txt > /tmp/terms && grep -rniwFf /tmp/terms <files>` — zero hits allowed. If the term list is missing on this machine, flag it to Matt instead of skipping the check.
- **Verification discipline** (this repo's analog of a test suite): cross-references between docs resolve; the scrub check passes; placeholder and INVARIANT/PARAMETER conventions are intact.
- **Never work outside the Now list without asking.** New ideas → SCOPE.md Later — say "adding to Later" and move on.
- **Announce spec changes.** If a request would change `SPEC.md`, say "this changes the spec" before doing it, and update the file — not just the conversation.
- **Ask before deleting any file or restructuring directories.**
- **Session economy (Brief 006).** Manage your own context and subagents; never ask Matt to. Because this repo carries the memory, clearing loses nothing that matters: `/compact` on a heavy mid-session context, `/clear` when switching to an unrelated task. Before spawning a subagent, ask whether the work needs one at all — each is its own request stream; spawn deliberately, never reflexively for work you could do inline.
- **Task routing (Brief 007).** For every task, pick the cheapest combination of pattern, model, and effort that gets full quality — escalate only when stakes or difficulty demand. Pattern ladder: inline → single agent → swarm/workflow; fan-out only for what earns it. Small well-defined work → fast/cheap tiers at low effort; judgment, integration, and spec work stay on the most capable tier; hard verify/judge → the second tier. Every delegated agent gets model and effort set explicitly at spawn — never silent inheritance of the session model. Current tier names live in `plugin/templates/model-routing.template.md`'s worked example.
- **Append-only stays append-only:** `JOURNAL.md`, `AUDIT.md` entries, and everything in `dogfood/briefs` (briefs are filed unmodified and never edited after filing).

## Session end — the split wrap-up ritual (Brief 001)

Wrap-up is **pure capture, zero operator judgment**. Matt wraps up at cognitive empty tank; his only job is to say "wrap up." Do not ask him to read, decide, or triage anything at session end.

When Matt says "wrap up" (or the session is ending), **invoke `/vibezen:wrap-up` as a command** — not these steps from memory (same rule as session start). If the command doesn't resolve, record that in `STATUS.md` as the first item for the next `/resume` triage, then follow the steps:

1. Run the docs checks (cross-references, scrub grep); record the outcomes in `STATUS.md`. Do not ask Matt to act on failures now — they are the first item at the next `/resume` triage.
2. Update `STATUS.md`: what works, what's half-done, open questions (captured for the next `/resume`, never posed now), a drafted next-session proposal (confirmed at the next `/resume`).
3. Append a dated entry to `JOURNAL.md`: intended vs. actual, friction named honestly, how-we-work decisions *made during the session* (capture — never generate new ones at wrap), a mood read, and your own failures. Never rewrite past entries.
4. Run the self-audit and write it as a new dated entry at the top of `AUDIT.md`. Matt does not read it now. Output contract (Brief 001): every item names a specific file or behavior AND a concrete check that would settle it; items without a falsifiable check are labeled **speculation** and routed to SCOPE.md Later; **"No material gaps" is a correct and expected output — do not manufacture items.**
5. Commit everything with a plain-language message.

**Output constraint (Session 6 part-3 audit; the command carries it at wrap-up.md:7 and :17): after the steps run, confirm to Matt in one line — nothing more.** No summaries, no multi-paragraph closings — he's at empty tank, and the one-line rule is the whole point of the ritual.

If Matt bails mid-session, the next `/resume` must report the half-done state honestly.

## Failure logging

Log your own failures in `JOURNAL.md` — misunderstandings, wrong assumptions, things Matt had to correct. If Matt re-explains something twice, the doc is ambiguous: fix the doc, not the conversation.
