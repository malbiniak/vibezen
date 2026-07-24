# Decision Brief 004 — Distribute the Playbook as an Installable Plugin

**Date:** 2026-07-05
**Source:** A role-play pressure-test this session — "a teammate gets the GitHub link; is the repo self-explanatory?" — plus verification of current (2026) Claude Code plugin/skill distribution mechanics
**Status:** Drafted 2026-07-05. Integration (the plugin-packaging work) is deferred and sized as its own effort — confirm at the next `/resume` before building.
**Instruction to Claude Code:** Read this brief and the current playbook in full before integrating. This brief is the spec; do not re-litigate the reasoning, but flag any direct contradiction with existing content before writing. Integration here is not a doc edit — it is a packaging change; treat the "Decisions" as the target state and sequence the build accordingly.

---

## Context

The playbook is currently shipped as a **repo you read**: a teammate is handed a GitHub link and is expected to open the README, then `PLAYBOOK.md`, then `templates/README.md`, and to hand-edit the hardcoded operator profile ("Matt is a Staff PM and non-developer") out of the templates before they can found anything. The `/new-project`, `/resume`, and `/wrap-up` commands only exist when Claude Code is opened *inside the cloned repo*, because they live in `.claude/commands/`.

The pressure-test exposed the mismatch bluntly. The product's own core principle is that the operator never reads code or schemas — they describe intent and Claude translates — yet onboarding forces a teammate to *read three documents* before they can begin. The front door contradicts the house. The teammate's own first question — "where do I run this? is it a skill? is the whole project a skill?" — was the right one: they were already reaching for the correct unit of distribution.

Verified mechanics (current Claude Code): a **plugin** bundles slash commands and their supporting template files together; a teammate installs it once (`/plugin marketplace add <owner/repo>` then `/plugin install <name>`), after which the commands are available **user-level, in any directory** — exactly what `/new-project` needs, since it founds a new project *elsewhere*. Plugin-bundled files are referenced by a path convention (`${CLAUDE_PLUGIN_ROOT}` / `${CLAUDE_SKILL_DIR}`) rather than the relative `templates/` path the commands use today. One mechanic is under-documented and must be tested before distribution (see Verification).

## Decisions

### 1. Adopt: the playbook is an installable plugin, not a read-first repo

The unit of adoption becomes a Claude Code plugin. A teammate goes from "GitHub link" to a working `/new-project` in two commands and no file-reading:

```
/plugin marketplace add <org>/<playbook-repo>
/plugin install <playbook>
```

The repo's job shifts from "documents to study" to "the source the plugin installs from." Reading `PLAYBOOK.md` becomes optional depth, never a prerequisite to start.

### 2. Adopt: onboarding is install-then-run; the README collapses to match

The README's front section becomes the two install commands and "then run `/new-project`." The current three-way "Start here" pile (templates/README vs `/new-project` vs PLAYBOOK) is replaced by a single path. Depth docs remain, below the fold, for those who want the reasoning.

### 3. Adopt: operator parameterization by interview — absorb the standing Later item

There is no longer a repo to hand-edit, so the hardcoded operator profile is removed at the root. The operator's identity (role, developer/non-developer, what they can take on) is elicited by the first `/new-project` run and written into that project's instantiated files. This closes the "Operator parameterization" item that has sat in SCOPE Later since 2026-07-03; parameterization stops being a manual chore and becomes a question the founding interview asks.

### 4. Adopt: templates travel with the plugin, referenced by the plugin path convention

The file-definition templates and process templates are bundled inside the plugin and referenced via `${CLAUDE_PLUGIN_ROOT}/templates/...` (or the skill-dir equivalent), replacing today's relative-path reads in the command files. Instantiation still writes a filled founding set into the new sibling project; only the *source path* the commands read from changes.

### 5. Adopt: the repo's own dogfooding docs get fenced from the adopter's view

Because the repo is now a plugin source rather than a project to read, its self-hosted working docs (its own `SPEC.md`, `SCOPE.md`, `STATUS.md`, `JOURNAL.md`, `AUDIT.md`, `briefs/`) must not read as "the thing you adopt." They are relocated under a clearly-labelled subfolder or otherwise fenced, so a newcomer browsing the repo sees the product and its install path first, and the self-application second. *(This is a directory restructure — it requires Matt's explicit go-ahead at integration time, per the "ask before restructuring" ground rule.)*

### 6. Keep off the critical path: GitHub "Use this template"

"Use this template" copies the repo's structure into a teammate's new repo; it does not deliver `/new-project` as a reusable tool, and it re-introduces the read-and-edit burden. It is not the adoption path. It may remain available for someone who explicitly wants to fork the playbook's own structure, but it is not what a teammate is pointed at.

## The honest floor (state it in the README; do not pretend it away)

Even as a plugin, a teammate needs: Claude Code installed, a Claude subscription or API key, and the willingness to run the two `/plugin` commands. That floor cannot drop to zero. What it *does* drop is everything above it: no cloning, no repo-structure comprehension, no name-editing, no learning where commands live. A teammate who already runs Claude Code is roughly one minute from `/new-project`.

## Verification

- **Blocking pre-distribution test:** whether a marketplace-installed plugin copies its bundled supporting files into cache or references them in place is under-documented. Before sharing with anyone, build a throwaway plugin that reads and copies out a bundled template via `${CLAUDE_PLUGIN_ROOT}`, install it from a marketplace, and confirm the template is found and instantiated correctly. If in-place vs cached behavior breaks the copy, adjust the reference convention before distributing.
- **Behavioral acceptance:** on a machine that has never seen the repo, run the two install commands, open Claude Code in an empty directory, run `/new-project`, and confirm it interviews for the operator profile and founds a project — with no file editing and no reading of `PLAYBOOK.md`.
- **Regression:** `/resume` and `/wrap-up` still work inside an instantiated project after the path-convention change.

## Relationship to existing scope

Supersedes the framing of the standing **Publish** item (SCOPE Next): publishing the repo *as-is* ships the read-first clunk this brief removes. Plugin packaging should land before — or as — the publish step. Absorbs the **Operator parameterization** Later item (Decision 3).
