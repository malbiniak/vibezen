# The Playbook Repo — What It Is

This repo is the playbook: the templates, process documents, and amendment archive for how Matt runs vibe-coded projects with Claude Code. It is not an app and never will be — the only deliverables are markdown documents. Product code, product schemas, and app features are permanently out of scope; drafting any of them means work has drifted and must stop.

## The people

| Person | Who they are | What they can take on |
|---|---|---|
| **Matt** | Operator and owner | Describes intent, approves every system change, answers questions. Never reads schemas or code; never edits files by hand. |
| **Claude Code** | Sole maintainer | Writes and maintains every file in this repo. Translates Matt's intent into documents and explains everything back in plain language. |
| **Future projects** | Consumers | Each new project's Phase 0 and Session 0 consume the templates and PLAYBOOK.md without needing Matt to explain the system. |
| **Teammates & the public** | Readers and adopters | Should be able to understand and adopt the system from the README and PLAYBOOK.md alone, with Matt not in the room. |

## User stories, per persona

**Matt** (operator)
- I want to take a new idea to a founded project in one sitting, by running `/new-project` and answering interview questions.
- I want every change to the system to pass through my approval with a paper trail, so the playbook never drifts silently.
- I want this repo to run the same rituals it prescribes, so the system is tested on itself before any project inherits it.

**A future project's founding session**
- I want templates complete enough to instantiate without inventing structure, so every project starts with the proven anatomy.

**A teammate or public adopter**
- I want to read one README and understand what this is, how to use it, and what I'm allowed to change.

## The core rule: nothing changes without a paper trail

The system only changes through the amendment loop, stated behaviorally:

1. A process learning surfaces — in a project's `/resume` triage (routed as "playbook intake"), or in a pressure-test conversation.
2. The thinking happens outside this repo and ends in a **decision brief**.
3. The brief is filed **unmodified** in `/briefs`, numbered, never edited after filing.
4. Claude Code integrates the brief against the current playbook, with Matt's explicit approval. It does not re-litigate the brief's reasoning, but flags any direct contradiction with existing content before writing.
5. Every section derived from a brief cites its number ("Brief NNN").

`/templates` and `PLAYBOOK.md` never change without Matt's explicit approval. There is no fast path.

## The privacy rule (this is a product requirement)

This repo is public: every committed file carries zero project-private content — no person's name but Matt's, no family details, no vendor names, no addresses, nothing identifying from any source project. Enforced by a scrub check before every commit: changed files are grepped against a local, gitignored term list (the private source material and the term list itself both live outside the published repo). This rule is what makes the repo shareable with a team and the public.

## Non-goals (deliberately out of scope, permanently unless the spec changes)

- **Product code, product schemas, app features** — in any form, including "just an example app." Examples in templates stay as neutral placeholders.
- **Hosting project content** — project documents live in project repos. Only process learnings come back here, and only as decision briefs.
