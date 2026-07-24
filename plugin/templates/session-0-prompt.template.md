# Session 0 Kickoff Prompt — `<project name>` (template)

> **Template.** Instantiated by the playbook plugin's `/new-project` command at Phase 0 (Brief 004), written into the new repo as `SESSION-0-PROMPT.md`, and pasted by the operator into a fresh Claude Code session there. No human fills placeholders by hand: the `<placeholder>` list below IS Phase 0's output contract (see `PHASE-0.md`) — every value comes from the Phase 0 interview, without invention. The structure — carry-forward context, interview in small batches, a checkpoint before any file is written, ✅ confirmations, explicit stop condition — is INVARIANT; the content is per-project.

---

## Context (carry forward)
- Project: "`<name>`" — `<one-sentence definition, including what is explicitly OUT of scope>`
- Builder: `<operator profile — name, role, developer or non-developer, what they take on and what they never touch; from the Phase 0 personas stage (Brief 004, Decision 3)>`. The operator describes behavior; you handle all technical translation. NEVER require them to read anything their profile rules out — always explain the data model back in plain domain language
- Process is defined in `<build playbook filename>` in this directory. It is the founding process document. Read it FIRST and treat it as authoritative
- Slice order is locked: (1) `<slice 1>`, (2) `<slice 2>`, `<…>`
- The core behavioral rule of the product: `<state it behaviorally in one to three sentences — what the product decides or does, based on what>`

## Task: Session 0 — Founding session. NO application code will be written today.

Starting state: this directory contains `<build playbook filename>` (instantiated), this prompt, and the still-template file-definition templates in `<docs location>/templates/` — all created by `/new-project` at Phase 0 (Brief 005). `<If the directory holds pre-existing project or context files, name them here so Session 0 reads, and never disturbs, them.>`

Target state: the working files created from those templates and committed — SPEC.md, SCOPE.md, DATA-MODEL.md `<if the project has persistent data>`, STATUS.md, JOURNAL.md at `<docs location — confirmed at the Phase 0 checkpoint, e.g. the repo root or docs/>`, and CLAUDE.md at the repo root — plus a `/resume` slash command, per the playbook's definitions of each. Turning the templates into these live files is this session's job; they are templates on purpose until now.

Execute in this order:

1. Read `<build playbook filename>` in full.
2. Interview me about `<the domain>` before writing anything. Ask questions in small batches (max 3 at a time), covering: `<the people involved and what they can take on; how the work happens today; recurring and seasonal items; existing resources and contacts; current priorities>`. Continue until you can write per-persona user stories for every persona. Do not pad the interview — stop when you have enough.
3. CHECKPOINT: Summarize what you learned and present the plain-language version of the proposed data model. Wait for my confirmation before writing any files.
4. Write all the files per the playbook, using the file-definition templates in this repo as the structural reference. SPEC.md MUST include per-persona user stories, `<the core rule>` stated behaviorally, `<any key workflow or state machine, stated as states in order>`, and explicit non-goals (`<…>`).
5. Create the `/resume` command per PLAYBOOK.md's ritual definition (Brief 001): reads the most recent AUDIT.md entry first and triages it, reads STATUS.md and SCOPE.md, reports project state in plain English, proposes the session goal. (No audit exists yet at Session 0 — the command must handle that.)
6. Write the first JOURNAL.md entry covering this session, then update STATUS.md so the next session starts the **design sprint** — the interview-driven design of the Now/Next slices, each of which must pass the readiness gate before any build begins (Brief 003; see the design-sprint stage in the build playbook). Building slice 1 does not start until its spec passes the gate.
7. ✅ After each numbered step, output one line confirming what was completed.

Constraints:
- MUST NOT write any application code, choose implementation details beyond what session 1 needs, or scaffold the product today
- Only make changes directly requested. Do not add extra files, abstractions, or features beyond the working files and the `/resume` command
- Stop and ask before deleting any file or adding any dependency
- All files MUST be in plain language the operator can read, except the schema half of DATA-MODEL.md

Stop condition: all files committed, `/resume` works, and I have confirmed the plain-language data model matches how `<the domain>` actually operates. Then end the session with a proper wrap-up per CLAUDE.md — pure capture, nothing for me to read or decide at session end (Brief 001).

Next in the pipeline (not today): the design sprint, then gated build sessions — Session 0 → design sprint → build sessions (Brief 003).
