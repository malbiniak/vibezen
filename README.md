# Vibezen

**Vibe coding × kaizen.** An operating system for building software with Claude Code when the person in charge never reads the code. The operator describes intent and behavior in plain language; Claude Code writes and maintains everything — every file, every schema, every line — and a small set of documents living in the repo carries all of the project's memory.

The name is the intent. *Kaizen* — continuous improvement — is the spine: every session ends by capturing what worked, what didn't, and what to fix; every process learning routes back as a filed decision brief; the playbook improves itself through the same loop it prescribes. Nothing here was designed on a whiteboard — it was all distilled from real projects, one captured lesson at a time.

## Install it (that's the whole onboarding — Brief 004)

In Claude Code, run:

```
/plugin marketplace add malbiniak/vibezen
/plugin install vibezen@vibezen-market
```

**The honest floor:** you need Claude Code installed, a Claude subscription or API key, and those two commands. That's it — a teammate already running Claude Code is about one minute from `/new-project`. No cloning, no reading required first.

## Your first project

1. Open Claude Code **in the folder where you want the project to live** — the founding docs are created right there (Brief 005). An empty folder works; so does one you've seeded with notes or artifacts for context; so does an existing project you want to bring the playbook into.
2. Run `/new-project`. It opens by asking how you want to start — a guided discovery interview, a one-line description, or pointing it at files already in the folder. The Phase 0 interview takes you from "I have an idea" to a founded project — it asks who you are (the operator profile is interviewed, never hand-edited), what the product does, and what to build first. Answer in plain language; nothing is written until you confirm at a checkpoint (including where the files will go).
3. When it finishes, open a fresh Claude Code session in the same folder and paste in the contents of its `SESSION-0-PROMPT.md`. That session turns the bundled templates into the project's real working documents — until then they're `.template.md` files on purpose.
4. Every session after that has the same rhythm: start with `/resume`, end with `/wrap-up`.

**A note on command names:** installed plugin commands are namespaced, so the canonical form is `/vibezen:new-project` (likewise `/vibezen:resume`, `/vibezen:wrap-up`). Typing the bare `/new-project` works too — Claude Code resolves it as a prefix match — and your interface may display the namespaced form either way.

## What you get

Three commands, available in any directory once installed:

| Command | What it does |
|---|---|
| `/new-project` | Phase 0: the founding interview → this folder founded with an instantiated build playbook, Session 0 prompt, and templates — new or existing project alike (Brief 005). |
| `/resume` | Session start: triage the last self-audit, read the working docs, report state, propose a goal. |
| `/wrap-up` | Session end: pure capture — status, journal, self-audit, commit. Zero operator judgment required. |

The system was distilled from a real project that shipped and keeps shipping — after a string of failed attempts without it. Its private details are scrubbed; its structure, conventions, and hard-won rules are all here.

## Want the reasoning? (optional depth — never a prerequisite)

- [`PLAYBOOK.md`](PLAYBOOK.md) — principles, rituals, the document system, model routing, failure tripwires, and how the playbook itself changes.
- [`plugin/templates/README.md`](plugin/templates/README.md) — what's in the template package and the conventions it follows.

## What's in this repo

| Path | What it is |
|---|---|
| [`plugin/`](plugin/) | The installable plugin: the three commands and the bundled templates. This is what the install commands deliver. |
| [`PLAYBOOK.md`](PLAYBOOK.md) | The connective tissue: principles, rituals, the document system, amendment process. |
| [`dogfood/`](dogfood/) | This repo running its own playbook on itself — its working docs and decision-brief archive. Not the thing you adopt; see its README. |

## License

[MIT](LICENSE)
