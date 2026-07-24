---
description: Run Phase 0 — found a project from the playbook templates, here in this directory
---

# /new-project — Phase 0 executor

You are running Phase 0 of the playbook, from the installed plugin. The project is founded **in the current directory** — the operator runs this command from the folder where they want the project to live (Brief 005). Read `${CLAUDE_PLUGIN_ROOT}/templates/PHASE-0.md`, `${CLAUDE_PLUGIN_ROOT}/templates/session-0-prompt.template.md`, and `${CLAUDE_PLUGIN_ROOT}/templates/build-playbook.template.md` in full before asking anything.

The person you are interviewing is **the operator** — the owner of the project. Their identity is not assumed: the interview's persona stage elicits their operator profile (role, developer or non-developer, what they take on, how they verify) and writes it into the instantiated files (Brief 004, Decision 3).

## 1. Interview

**Open with the entry-path question (Brief 005).** One question, three offered paths — the operator's own framing always welcome as a fourth:

- **Discovery sprint** — you guide them question by question, each question shaped by their last answer.
- **One-liner** — they give a short description of the idea and you build the interview from it.
- **Point at context** — they name files or artifacts already in this directory; you read those first and interview from what they contain.

If the directory already has files, do not guess what they mean (Brief 005, Decision 2). Ask: are these context for the new project, or an existing project the operator wants to bring the playbook into? **Adoption mode** — for an existing project — means: read the existing repo first, compress the interview stages the repo already answers, and keep the focus on retro, the operator profile, and scope.

Then run the PHASE-0.md interview in order: retro → behavioral vision → personas (including the operator profile) → scope negotiation → the "there's probably more" excavation. Small batches — max 3 questions at a time. Do not pad. **Interview like a great product manager** (Brief 005, Decision 3): probing questions, each adapted to the last answer; invite stories, not confirmation; never reduce the operator to picking categories — every question past the entry path accepts a free-form answer. Continue until the output contract is satisfied: every `<placeholder>` in `session-0-prompt.template.md` can be filled from the operator's answers without invention. If an answer is missing, ask; never invent.

New ideas beyond scope negotiation are not brainstormed — they go to the Later list being drafted, and you say so.

## 2. CHECKPOINT

Present the filled placeholder values as a plain-language summary — project definition, core rule, operator profile, slice order, personas, non-goals — **plus the proposed file layout** (Brief 005, Decision 1): which founding files go where in this directory. Convention-bound files (`CLAUDE.md` when Session 0 later creates it, plus `AGENTS.md` only if the project adopts that optional subtree convention — see the CLAUDE template) belong at the root; the working docs and templates go where they fit this project (e.g. a `docs/` folder, or the root for a docs-only project). Confirm the project slug and the layout with the operator. **Wait for the operator's confirmation before writing anything.**

## 3. Instantiate (only after confirmation)

Found the project **here, in the current directory**:

- `git init` only if the directory is not already a git repository.
- Write `<project-slug>-build-playbook.md`: `build-playbook.template.md` with every placeholder filled and the template notes removed. Add a provenance line under the title: `*Instantiated from the playbook plugin, YYYY-MM-DD, plugin version <version from ${CLAUDE_PLUGIN_ROOT}/.claude-plugin/plugin.json>.*`
- Write `SESSION-0-PROMPT.md`: `session-0-prompt.template.md` filled, template notes removed — including the confirmed docs location, so Session 0 writes the working files into the right place.
- Copy the file-definition templates from `${CLAUDE_PLUGIN_ROOT}/templates/` into `<docs location>/templates/`, unmodified, keeping their `.template.md` names: SPEC, SCOPE, CLAUDE, STATUS, JOURNAL — and DATA-MODEL only if the project has persistent data (the interview settles this; the SESSION-0-PROMPT must match).

## 4. Boundaries

- MUST NOT create anything beyond that founding set — no product files, no code, no scaffolding.
- Never overwrite or restructure files that were already in the directory (Brief 005, Decision 2). If a founding file would collide with an existing one (e.g. a `CLAUDE.md` is already here), propose a merge and wait — never clobber.
- Stop and ask before writing anywhere outside the current directory.
- Never modify the plugin's bundled templates under `${CLAUDE_PLUGIN_ROOT}` — sources are read-only.

## 5. Hand off

Tell the operator, explicitly (Brief 005, Decision 4):

- The files in `templates/` are **intentionally still templates**. Session 0 — the next step — is what turns them into the real, filled-in `SPEC.md`, `SCOPE.md`, `CLAUDE.md`, `STATUS.md`, `JOURNAL.md` (and `DATA-MODEL.md` if applicable). Nothing is missing.
- Next step: open a **fresh Claude Code session in this directory** and paste the contents of `SESSION-0-PROMPT.md`.

Phase 0 ends here.
