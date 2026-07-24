# Decision Brief 005 — Found In Place: the /new-project Entry, Location, and Hand-off Fixes

**Date:** 2026-07-10
**Source:** Sam dry-run round 1 (2026-07-10) — Matt role-playing "Sam," a developer teammate, ran the installed `/new-project` end-to-end for the first time (Fable model). The interview's middle and late stages landed well ("this seems to know what it's doing"); the entry, the output location, and the hand-off did not.
**Status:** Decisions approved by Matt at plan review 2026-07-10; integrated the same session.
**Instruction to Claude Code:** Read this brief and the current `plugin/commands/new-project.md` + `plugin/templates/PHASE-0.md` in full before integrating. This brief is the spec; do not re-litigate the reasoning, but flag any direct contradiction with existing content before writing.

---

## Context — what round 1 surfaced

1. **The interview starts cold and the model improvises the opening badly.** Neither the command nor `PHASE-0.md` defines an entry question, so the model invented a "pick the closest category" multiple-choice where the operator couldn't both pick a category and describe their idea. The operator's first move should never be fitting their idea into someone else's taxonomy.
2. **Docs land in the wrong place.** The command instructs "create `../<project-slug>/` (a sibling of the current directory)." Sam ran it from his intended project folder and got a new sibling folder instead. The natural operator expectation: run the command *from* your project folder; the docs land *here*. The sibling default also blocks the real upcoming use case — bringing the playbook into existing, active projects.
3. **The template hand-off is opaque.** Phase 0 correctly leaves `templates/*.template.md` for Session 0 to instantiate — but nothing tells the operator that, and the instantiated build playbook describes SPEC/SCOPE/etc. in present tense ("all live in the repo," "Now / Next / Later") while none of them exist yet. It reads as a broken promise rather than a pipeline stage.
4. **Command namespacing surprised the operator.** `/new-project` surfaces as `/playbook:new-project`. Not a bug — installed plugin commands are namespaced `plugin:command`, and the bare form resolves as a prefix match — but the README promises the bare form without saying so (flagged by the 2026-07-07 audit, item 1).

## Decisions

### 1. Adopt: found in place — and each file in its right place

`/new-project` creates the founding set in the **current directory**. The sibling-folder default is removed. Placement within the directory follows convention, not a flat dump: convention-bound files (`CLAUDE.md`, `AGENTS.md`) belong at the root; working docs go where they fit the project (e.g. a `docs/` folder); the file-definition templates live under that same docs home. The command proposes the concrete layout at CHECKPOINT for the operator's confirmation, and the confirmed placement is written into the instantiated build playbook and `SESSION-0-PROMPT.md`, so Session 0 and every later ritual know where the docs live. `git init` runs only if the directory isn't already a repo.

### 2. Adopt: never assume what a non-empty directory means

Files already in the directory could be (a) an existing project the operator wants to bring the playbook into, or (b) context artifacts the operator seeded on purpose for the interview to read. The command never switches modes on "directory is non-empty" alone — it asks: *"I see files here — are these context for the new project, or an existing project you want to bring the playbook into?"* Adoption mode — read the existing repo first, compress interview stages the repo already answers, keep the focus on retro, operator profile, and scope — runs only when the operator says that's what this is. In every mode: never overwrite or restructure existing files; a collision (e.g. an existing `CLAUDE.md`) gets a merge proposal, never a clobber.

### 3. Adopt: a defined entry-path question, and a PM-grade interviewing bar

The interview gains a stage 0 — one structured question offering three entry paths (plus the operator's own framing as "Other"):

- **Discovery sprint** — guided, question-by-question, each question shaped by the last answer.
- **One-liner** — the operator gives a short description and the interview builds from it.
- **Point at context** — the operator names files/artifacts in the directory; the interview reads them first.

Branch from the answer. And a standing interviewing rule, written into `PHASE-0.md` because it can't be overstated: ask the probing questions an incredibly motivated, curious, highly experienced product manager would ask — adapt the line of questioning to each response, invite stories rather than confirmation, and never reduce the operator to picking categories. Every question past stage 0 accepts free-form answers.

### 4. Adopt: templates stay templates at Phase 0 — fix the communication, not the mechanism

The pipeline is right: Phase 0 founds, Session 0 instantiates. What changes is that the operator is told. The hand-off says explicitly that the `templates/` files are *intentionally* still templates and that Session 0 turns them into the real SPEC.md, SCOPE.md, etc. The build-playbook template's working-files table stops claiming the files exist and instead marks when each is created.

### 5. Adopt: document the namespaced command form

README documents `/playbook:new-project` as the canonical installed form, with bare `/new-project` working as a prefix match. Settles audit 2026-07-07 item 1.

## Verification

- Headless smoke: `/new-project` in an empty scratch directory opens with the entry-path question and targets the current directory.
- Behavioral acceptance (dry-run round 2): Matt-as-Sam re-runs the full founding from `sam-dryrun/workspace/` on Fable — entry paths offered, docs land in place with sensible layout, hand-off explains the template→Session-0 relationship.
- Model parity (round 3): same script on Opus (`/model opus`) — the entry question, placement proposal, and interviewing quality must not depend on Fable.
- Regression: `/resume` inside the founded project (settles audit 2026-07-07 item 3).

## Relationship to existing scope

Extends Brief 004 (the plugin is the unit of adoption) by fixing what the first real adoption run hit. Touches the SCOPE Later item "`/new-project` refinements" — the defer-the-name and docs-only/no-repo ideas stay in Later; this brief does not absorb them. Adds one new Later item (from the same dry-run session): porting the commands into code-puppy for Walmart-internal use.
