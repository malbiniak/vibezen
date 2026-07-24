# The Playbook Templates

A proven system for building software with Claude Code when the operator describes behavior and Claude does everything else — every schema, every line of code, every file. One operator, one repo, Claude Code as the sole maintainer.

The system's core: a set of working documents that live in the project's repo and carry all of its memory, plus three one-liner rituals (`/resume` to start a session, "add to Later" during it, "wrap up" to end it). The operator is never the state-carrier, never the typist, never the schema-reader.

These templates are the packaged version of that system, bundled inside the playbook plugin (Brief 004). The connective tissue — principles, rituals, failure tripwires, amendment process — lives in `PLAYBOOK.md` in the playbook repo; reading it is optional depth, never a prerequisite.

## What's in this directory

**Process:**

| File | What it is |
|---|---|
| `PHASE-0.md` | The founding conversation: from "I have an idea" to a new repo with founding artifacts. Run by `/new-project`. |
| `build-playbook.template.md` | The per-project operating model — principles, working files, session types. Instantiated at Phase 0. |
| `session-0-prompt.template.md` | The kickoff prompt for a new project's first session. Its `<placeholder>` list is Phase 0's output contract. |
| `model-routing.template.md` | Which model tier for which session type, and why. |
| `slice-method.template.md` | How scope gets cut into slices, and how circular dependencies break. |
| `design-sprint.template.md` | Batched interview-driven design: WHY/WHAT doc skeletons and the readiness gate that makes the build queue executable without mid-build operator decisions (Brief 003). |

**File definitions** — one per working doc every project maintains, each with its job, conventions, and skeleton:

`SPEC.template.md` · `SCOPE.template.md` · `CLAUDE.template.md` · `DATA-MODEL.template.md` · `STATUS.template.md` · `JOURNAL.template.md`

## How to use it

1. Install the playbook plugin — two `/plugin` commands, listed in the playbook repo's README (Brief 004). Open Claude Code **in the directory where the project will live** — empty, seeded with context files, or an existing project to adopt (Brief 005).
2. Run `/new-project`. Phase 0 opens with an entry-path question (discovery sprint, one-liner, or point at files in the directory), interviews you in small batches — including your operator profile: role, developer or non-developer, what you take on — checkpoints a plain-language summary plus the proposed file layout, and — only after your confirmation — founds the project in place: the instantiated build playbook, `SESSION-0-PROMPT.md`, and copies of the file-definition templates, each where the confirmed layout puts it.
3. Open a fresh Claude Code session in the same directory and paste the contents of `SESSION-0-PROMPT.md`. Session 0 interviews you about the domain and turns the copied templates into the project's live working docs. No product code gets written that day.
4. Design, then build. Run the design sprint until the readiness gate marks your whole queue executable (`design-sprint.template.md`); then start every build session with `/resume`, park every new idea with "add to Later," end every session with "wrap up," and accept builds by working the acceptance script in the app.

## Conventions

- `<angle brackets>` are placeholders. No human fills them by hand — the Phase 0 and Session 0 interviews fill them, and they may never be invented.
- **INVARIANT** sections keep their substance in every project. **PARAMETER** marks per-project decisions.
- Files keep the `.template.md` suffix until instantiated. (A literal `CLAUDE.md` in this directory would be auto-loaded by Claude Code as live instructions — the suffix is a safety, not a style.)
- Templates are read-only in use. Changing the system itself requires a decision brief — see `PLAYBOOK.md` and the decision-brief archive in the playbook repo.
- The operator profile is not hardcoded. The Phase 0 interview elicits it — role, developer or non-developer, what the operator takes on — and fills the operator placeholders in the instantiated files (Brief 004, Decision 3). Nothing to hand-edit.
