# Phase 0 — The Founding Conversation

The playbook phase that precedes every project. Runs in Claude Code via the installed plugin's `/new-project` command, **from the directory where the project will live** (Brief 004; Brief 005).

## Purpose

Take the operator from "I have an idea" to "this directory holds an instantiated build playbook and a filled Session 0 prompt." Phase 0 is conversation + instantiation; it writes founding artifacts only — never product files, never code.

## How to interview (Brief 005, Decision 3)

Ask the probing questions an incredibly motivated, curious, highly experienced product manager would ask. That kind of interviewer adapts the line of questioning to each response — the next question comes from the last answer, not from a script marched through. Invite stories, not confirmation. Never reduce the operator to picking categories; every question past the entry path accepts a free-form answer.

## The interview, in order

Questions come in small batches (max 3). Each stage feeds the next; keep the order.

0. **Entry path.** One structured question, three offered paths plus the operator's own framing: a **discovery sprint** (guided, question by question, each shaped by the last answer), a **one-liner** (a short description the interview builds from), or **point at context** (files/artifacts already in the directory — read them first, interview from what they contain). If the directory already has files, never assume what they mean (Brief 005, Decision 2): ask whether they are context for a new project or an existing project to bring the playbook into. **Adoption mode** (existing project): read the repo first, compress the stages the repo already answers — the codebase usually settles much of stages 2 and 4's raw material — and keep the interview's weight on retro, the operator profile, and scope negotiation.
1. **Retro.** If prior attempts at this idea — or adjacent ones — failed: why did the *build* fail, not the product. Build-failure causes set process parameters before anything else gets decided.
2. **Behavioral vision.** What the product decides or does, stated behaviorally. This produces the candidate for the named core rule.
3. **Personas.** Who is involved, and what each can take on. This stage elicits the **operator profile** — name, role, developer or non-developer, what they take on, how they verify built work — which fills the operator placeholders in the instantiated files; nothing about the operator is assumed (Brief 004, Decision 3).
4. **Scope negotiation.** Slice order via data-model-first thinking — what data does the core rule need, which feature produces it, what gets entered by hand first (see `slice-method.template.md`, this directory). Now/Next/Later. Explicit non-goals.
5. **The "there's probably more" excavation.** Recurring items, seasonal items, existing resources.

## Exit criteria — the output contract

Phase 0 is done when every `<placeholder>` in `session-0-prompt.template.md` (this directory) can be filled from interview answers **without invention**. That template's placeholder list IS the output contract: if an answer is missing, ask; never invent. (The template's header note points back to this file — the two are cross-referenced on purpose.)

The build playbook's placeholders fill from the same answers; any that can't are asked, never invented.

## What Phase 0 does not do

**Declined practice: founding-stage feature brainstorming.** Phase 0 does not brainstorm features beyond scope negotiation. New ideas surfacing mid-founding route to the Later list being drafted in stage 4 — even during founding, every new idea lands in Later first.

## Output

Created by `/new-project` on the operator's confirmation, **in the current directory** (Brief 005, Decision 1), and nothing else:

- `<project-slug>-build-playbook.md` — instantiated, template notes removed, playbook version noted for provenance
- `SESSION-0-PROMPT.md` — filled, ready to paste into a fresh Code session in this same directory; carries the confirmed docs location
- `templates/` (under the confirmed docs location) — the file-definition templates the Session 0 prompt expects to find

Each file goes where convention puts it, confirmed with the operator at the checkpoint — convention-bound files at the root, working docs where they fit the project (e.g. `docs/`). Files already in the directory are never overwritten or restructured; collisions get a merge proposal (Brief 005, Decision 2).

The `templates/` files are **still templates on purpose** — Session 0 instantiates them into the live SPEC.md, SCOPE.md, etc. The hand-off tells the operator this explicitly (Brief 005, Decision 4).

Pipeline: **Phase 0** (`/new-project`, in Code, run from the project's directory) → **Session 0** (fresh session in that directory) → **design sprint** (interview-driven design of the queued slices, each gated before any build; Brief 003) → **build sessions**.
