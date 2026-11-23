# Plugin findings from the BEHIND! (what-to-eat) instantiation

*2026-08-30. Source: pre-Session-0 adversarial review of the first real Phase 0 output.
Every finding below was patched locally in what-to-eat the same night, so that repo is
the reference for what the fixed output should look like. These are the root causes to
fix in the plugin before the next /new-project run.*

## 1. Session 0 template instructs building a /resume command the plugin already ships

- Where: `plugin/templates/session-0-prompt.template.md` step 5 (line 26), plus the
  target-state line (18) and stop condition (36) that reference it.
- The plugin ships `commands/resume.md` and `commands/wrap-up.md`, and the shipped
  /resume already handles the no-AUDIT.md case the template tells Session 0 to build.
  Every instantiated project therefore creates a second /resume with the same name and
  a near-identical definition. Two sources of ritual truth, guaranteed drift.
- Same line has a second bug: it references "PLAYBOOK.md", but /new-project writes the
  playbook as `<project-slug>-build-playbook.md`. Dangling filename in every project.
- Fix: step 5 becomes "verify the plugin /resume against the freshly written files, and
  note in CLAUDE.md that session rituals come from the plugin commands." Fix the
  playbook filename reference to use the instantiated name placeholder.

## 2. /new-project copies only 6 templates but CLAUDE.template references 2 more

- Where: `commands/new-project.md` step 3 copy list (SPEC, SCOPE, CLAUDE, STATUS,
  JOURNAL, optional DATA-MODEL) vs `templates/CLAUDE.template.md` line 40
  (design-sprint.template.md) and line 49 (model names live in
  model-routing.template.md's worked example). The playbook template references the
  design sprint's doc structure too.
- Result: every instantiated repo has dangling references, the design sprint's own
  process file is missing at the moment the sprint runs, and the model-routing names
  ("fast-execution tier") resolve to nothing in-repo. This violates the playbook's own
  rule 1: the repo is the only source of truth.
- Fix: add model-routing.template.md to the copy list always, and
  design-sprint.template.md whenever the project runs the design sprint (the interview
  settles this, same as DATA-MODEL).

## 3. SPEC template hardwires permanent non-goals as INVARIANT

- Where: `templates/SPEC.template.md` conventions line ("Explicit non-goals" under
  INVARIANT) and the closing section header "Non-goals (deliberately out of scope,
  permanently unless the spec changes)". Also `session-0-prompt.template.md` line 25:
  "explicit non-goals (`<...>`)".
- BEHIND!'s Phase 0 produced a deliberate finding of NO permanent non-goals, with
  discipline coming from sequencing (three buckets: true non-goals, guardrails, slice
  boundary). The template contradicts a valid instantiation, and a template header
  marked INVARIANT that says the opposite of the project's spec is exactly what a
  future session follows literally.
- Fix: the invariant should be "an explicit scope statement" with the shape as a
  parameter: permanent non-goals OR sequencing buckets, chosen at Phase 0.

## 4. CLAUDE template routes playbook intake "out of this repo"

- Where: `templates/CLAUDE.template.md` line 31: process learnings are "routed out of
  this repo to the playbook."
- The playbook is instantiated in-repo by /new-project. The wording predates that
  decision. Fix: route to the in-repo playbook file, with optional upstream intake to
  the plugin.

## 5. Parent-directory CLAUDE.md leaks into every instantiated project

- Where: not in the plugin - `/Users/malbini/vibes/CLAUDE.md` (dated Aug 16 2026, one
  line: use `npx -y lavish-axi` to write product/technical plans). vibes/ is not a git
  repo, so there is no history of where it came from.
- Claude Code loads parent-directory CLAUDE.md files into every project under vibes/.
  That line directly conflicts with Session 0's job (write SPEC/SCOPE directly from
  templates) and would have risked a lavish detour mid-founding. It affects every other
  project in the directory the same way.
- Fix, two parts: (a) delete or scope that file (operator decision); (b) plugin-side
  root cause - /new-project's collision check only looks at the current directory.
  Add a parent-directory scan: walk up from the project dir, and surface any inherited
  CLAUDE.md instructions at the Phase 0 checkpoint so the operator decides whether the
  project CLAUDE.md must supersede them. The what-to-eat fix (an explicit supersede
  constraint in SESSION-0-PROMPT.md) is the shape of the generated guard.

## 6. No seed-data existence check at Phase 0 handoff

- Where: `templates/session-0-prompt.template.md` starting-state placeholder and
  `commands/new-project.md` checkpoint.
- In BEHIND!'s case, slice 1's seed data (this week's planned meals) existed as a
  document but was missing from the starting-state file list, and nothing in the
  templates forced anyone to notice - the generated prompt even listed "this week's
  actual meals" as an interview gap when it should have been a named file. Nobody
  caught it until the operator did.
- Fix: the Phase 0 checkpoint gains one question: "list what slice 1 needs on day one;
  for each item, confirm the file exists in the repo or mark it for interview capture."
  The session-0 template's starting-state section then names those files explicitly.

## Suggested order for the plugin update

1 and 2 are correctness bugs in every future instantiation - fix first. 3 and 4 are
template wording fixes. 5b and 6 are new checks in /new-project; small, high leverage.
Bump the plugin version and re-verify by diffing a fresh dry-run instantiation against
what-to-eat's patched files.
