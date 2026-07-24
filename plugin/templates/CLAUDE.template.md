# CLAUDE.md (template)

> **Job:** Claude Code's standing instructions — the file that enforces the discipline. Changes almost never; only the operator triggers a change, when the process itself changes.

## The layered memory pattern (pattern INVARIANT; whether/where to nest PARAMETER)

- **Root `CLAUDE.md`** — the always-loaded project charter: who the operator is, session rituals, ground rules. This is the file the skeleton below instantiates. **Root takes precedence on any conflict.**
- **Optional nested `<subfolder>/CLAUDE.md`** — when one subfolder needs folder-scoped rules (typically an app package with framework-specific guardrails), create a one-line `CLAUDE.md` in that folder containing exactly:
  ```
  @AGENTS.md
  ```
  and put the actual rules in a sibling `<subfolder>/AGENTS.md`. `AGENTS.md` is a cross-tool convention — any AI coding agent reads it — and the `@`-import routes it into Claude Code's memory too, loaded when work happens in that subtree. Example `AGENTS.md` shape:
  ```
  # <Folder-scoped rule title>
  <The rules: framework guardrails, "read the bundled docs before writing code," deprecation warnings — anything true only inside this folder.>
  ```
- **The nesting decision is per-project:** a docs-only repo nests nothing (root only); an app repo typically nests once, at the app package.

---

# Instructions for Claude Code — `<project name>`

## Who you're working with

`<Operator profile — filled from the Phase 0 personas stage (Brief 004, Decision 3): name and role; developer or non-developer; what they describe (intent, behavior) vs. what you translate; what they must never be required to read (e.g. schemas, foreign keys, code); how they verify (e.g. by using what was built, never by reading code); how data enters (e.g. through the product's screens or conversation, never CLI/CSV/files). State it as standing instructions, like: "X is a <role> and a non-developer. They describe behavior; you handle all technical translation…">`

## Session start (INVARIANT — Brief 001)

Sessions start with `/resume`:

1. Read the most recent dated entry in `AUDIT.md` **first**, and triage it with the operator before any new work begins — this is the fresh-eyes review of the prior session, done with fresh judgment and fresh context. Route each item: **fix now** (correctness, drift from `SPEC.md`, scope violations — these compound across sessions), **backlog** (ideas, brainstorms, efficiency improvements → `SCOPE.md` Later or the STATUS backlog), or **playbook intake** (process learnings → routed out of this repo to the playbook).
2. Read `SPEC.md`, `SCOPE.md`, and `STATUS.md`.
3. Report where things stand in plain English; propose today's goal.

## Ground rules

- **Behavior is the fixed point; implementation is negotiable.** `<The project's named core rule and key workflows>` are the product. Layout serves them, never the reverse.
- **Every behavioral rule in `SPEC.md` gets an automated test**, named in plain language after the behavior it protects, so a failing test reads like a broken promise, not a stack trace. *(PARAMETER — projects with code. A docs-only project states its verification discipline here instead.)*
- **Real-data builds get the independent review before "done" (Brief 002):** finder subagents across correctness / reuse / simplification / efficiency / altitude / conventions, then an adversarial-verify pass. **Every review and verify subagent runs on the fast-execution tier — never the session model.** The verify pass, the tests, and the operator are the real gate; the finders are disposable. Then the behavioral spec-fidelity pass (Brief 003): every build-spec requirement extracted into a checklist and traced through the built behavior — the spec is the oracle. Swarm subagents use fixed prompt templates and capped outputs (Brief 003). *(PARAMETER — projects whose builds write real data; docs-only projects skip.)*
- **No slice enters a build without a passed readiness gate (Brief 003):** the design sprint's fresh-context adversarial gate must have found nothing undesigned in the slice's build spec. Gate findings are the next design interview's agenda — never yours to resolve silently. *(PARAMETER — projects running the design sprint; see `design-sprint.template.md`.)*
- **Never ask the operator a design question mid-build (Brief 003).** If an undesigned decision surfaces mid-build anyway, take the safest easily-reversible choice, log it prominently in `STATUS.md`'s open questions and the wrap-up audit entry, and keep building. It gets triaged at the next `/resume`, where a wrong default costs one revert.
- **Acceptance is behavioral (Brief 003):** after verify passes, generate the acceptance script — a plain-language "try these N things" checklist from the build spec's acceptance criteria. The operator accepts by using the app; they never read diffs, coverage, or reviewer output.
- **Never build outside the Now list without asking.** New ideas go to Later in `SCOPE.md` — say "adding to Later" and move on. Scope creep is the enemy; the backlog absorbs it.
- **One slice item per session.**
- **Announce spec changes.** If a request would change `SPEC.md`, say "this changes the spec" before doing it, and update the file — not just the conversation.
- **Data model changes** happen rarely, alongside spec changes, and are always announced and explained in plain language. *(PARAMETER — only if DATA-MODEL.md exists.)*
- **Ask before deleting any file or adding any dependency.**
- **Session economy (INVARIANT — Brief 006).** Manage your own context and subagents; never ask the operator to. Because the repo carries the memory, clearing loses nothing that matters: **`/compact`** when context crosses a heavy threshold mid-session, **`/clear`** when switching to an unrelated task *(the threshold is PARAMETER; the practice is INVARIANT)*. And before spawning a subagent, ask whether the work needs one at all — each is its own request stream; spawn deliberately, never reflexively for work you could do inline. The codified review swarm and readiness gate are deliberate by construction; this targets ad hoc fan-out.
- **Task routing (INVARIANT — Brief 007; model names PARAMETER).** For every task, pick the cheapest combination of **pattern, model, and effort** that gets full quality — escalate only when stakes or difficulty demand. Pattern ladder: inline → single agent → swarm/workflow; fan-out only for what earns it (real-data review gates, audits, batch builds). Small well-defined work → fast/cheap tiers at low effort; judgment, integration, and spec work stay on the most capable tier; hard verify/judge passes get the second tier. **Every delegated agent gets model and effort set explicitly at spawn — never silent inheritance of the session model.** Current names in `model-routing.template.md`'s worked example.
- **`<Product-requirement tone rules>`** — restate here any SPEC.md tone/vocabulary requirements that constrain your output. *(PARAMETER.)*
- **UI:** consult the frontend-design skill for all UI work. *(PARAMETER — UI projects only; note who the users are and on what devices.)*

## Session end — the split wrap-up ritual (INVARIANT — Brief 001)

Wrap-up is **pure capture, zero operator judgment**. The operator wraps up at cognitive empty tank; their only job is to say "wrap up." Do not ask them to read, decide, or triage anything at session end.

When the operator says "wrap up" (or the session is ending):

1. Run the project's checks (`<test suite / link check / none>`); record the outcomes in `STATUS.md`. Do not ask the operator to act on failures now — they are the first item at the next `/resume` triage.
2. Update `STATUS.md`: what works, what's half-done, open questions (captured for the next `/resume`, never posed to the operator now), and a drafted next-session proposal (confirmed at the next `/resume`).
3. Append a dated entry to `JOURNAL.md`: intended vs. actual, friction named honestly, how-we-work decisions *made during the session* (capture them — never generate new ones at wrap), a mood read, and your own failures. `JOURNAL.md` is append-only — never rewrite past entries. Also add entries mid-session for notable moments, especially your own mistakes.
4. Run the self-audit and write it to a new dated entry in `AUDIT.md`. The operator does not read it now. The audit is governed by an output contract (Brief 001):
   - Ask: what are you least confident about; what might be missing.
   - Every item MUST name a specific file or behavior AND a concrete check that would settle it ("run X; if it prints Y, we're fine").
   - Items that cannot produce a falsifiable check are labeled **speculation** and auto-routed to backlog. Speculation never enters the fix-now queue.
   - **"No material gaps" is a correct and expected output when the work is clean. Do not manufacture items.**
5. Commit everything with a plain-language commit message.

If the operator bails mid-session, the next `/resume` must report the half-done state honestly.

## Failure logging

Log your own failures in `JOURNAL.md` — misunderstandings, wrong assumptions, things the operator had to correct. If the operator re-explains something twice, the spec is ambiguous: fix `SPEC.md`, not the conversation.
