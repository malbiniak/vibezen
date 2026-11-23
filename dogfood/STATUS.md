# Status

*Last updated: 2026-07-28 (Session 11 — closed at wrap-up)*

*Wrap-up checks: cross-references resolve ✓ (no new citations introduced this session) · privacy scrub clean on all docs changed this session (`STATUS.md`, `JOURNAL.md`, `AUDIT.md`) ✓ · `git status` confirms the only untracked-by-git change this session is `.claude/settings.json`, which is gitignored (repo-tracked files untouched) ✓*

> **Read this first at `/resume`.** This session opened as an off-repo detour again — Matt asked how to inspect what Claude Code loads (skills/plugins/MCP connectors) and then had Code trim this project's own local config, not playbook content — and again never invoked `/vibezen:resume`. **Fifth straight session skipping the ritual open** (Sessions 7, 8, 9, 10, now 11). Local `main` is still **ahead of origin** by 5 commits — nothing this session added a repo commit until this wrap; push is still Matt-paced.

## Where things stand, in plain English

Config-hygiene session, off-repo-work in spirit even though it touched a file inside this repo's tree. Matt noticed `/context` showing 77.7k tokens of MCP tool schemas he never uses in this project (Gmail, Google Drive, a Home Assistant connector) plus the full `vercel` plugin's skill set, and asked to scope both down per-project. Fix: `.claude/settings.json` (gitignored, machine-local, never committed) now carries `disabledMcpjsonServers` for the three unused connectors and `enabledPlugins: {"vercel@...": false}` to turn `vercel` off just for this repo, while `caveman` (judged generally useful) stays on. No template, command, or playbook doc was touched — this was Claude Code harness config, not plugin content.

1. **No new Later capture this session.** The work was local tooling hygiene, not a playbook idea — nothing routed to SCOPE.md.

## What works

- **Scope discipline held again.** The instinct to treat `.claude/settings.json` as local/gitignored (confirmed before editing) and keep the edit out of repo-tracked docs, out of SCOPE.md, and out of the scrub's concern, was correct and unprompted.
- Everything in Session 10's "what works" stands.

## What's half-done

- **Freeze leg (a) — still reported passed, still not reflected in SCOPE.md's banner.** Unchanged since Session 9; needs Matt's yes/no at triage before the banner text updates. Leg (b) — a teammate's independent install — still unmet.
- **Unpushed local commits — five sessions deep now** (Sessions 8, 9, 10, this session's wrap, plus the intervening Perplexity-link commit). `main` ahead of `origin/main`. Push is Matt-paced.
- **`/vibezen:resume` still unverified — five sessions running without it being invoked** (7, 8, 9, 10, 11). This session had no task-continuation excuse either; it opened cold on a harness question.
- **Three Brief-008 candidates + the part-four capture** await triage (unchanged, SCOPE.md Later).
- **Sessions 8, 9, and 10's audit entries** still stack, untriaged — this session adds a fourth.
- **Sam dry-run rounds 2–3** — unchanged.

## Not tasks (parked deliberately)

- Install-verification freeze — in effect, leg (a) reported passed pending confirmation, leg (b) unmet.
- All Later entries (unchanged this session — nothing new added).
- The herdr/firstmate/Lavish/OpenSuperWhisper trial — still parked outside this repo per Session 10.
- The org-scale contribution pattern — still with Chat.
- The 2026-07-05 dry-run project; `../meta-private/docs/start/`; no DATA-MODEL.md — unchanged.

## Next session: proposal (drafted — confirm at /resume)

0. **Open with `/vibezen:resume`.** Five sessions running without it now — confirm it resolves; if it errors, fixing the install is finding #1 before any other work.
1. **Confirm freeze leg (a) and update the SCOPE.md banner** — Matt's install report needs a yes/no on whether it counts as the scripted test, then the banner text updated to match.
2. **Triage the stacked audit entries** (Sessions 8, 9, 10, and this one), including the Brief-008 pick.
3. **Push, or confirm local-only intent** — five sessions of captures now sit only on this machine.
4. **Design the flywheel's first leg** (adoption handoff packet scoping) — unchanged from Sessions 7–10.

## Open questions for Matt (for the next /resume — not posed now)

- **Does the work-machine install count as freeze leg (a)?** If yes, SCOPE.md's banner needs updating and leg (b) — a teammate's install — becomes the only thing left gating the freeze.
- **Push the local commits?** Five sessions of captures + wraps sit only on this machine; the published repo is behind it.
- All prior open questions from Sessions 7–10 stand (Brief-008 pick; lunch volunteers; adoption target; killed-diagnosis routing; does the part-four capture change the Brief-008 queue).
- **What should `/resume` be renamed to?** Konnichiwa / hello / lfg / something else — Matt's call, no lean given yet.
- **Is skipping `/vibezen:resume` becoming the norm rather than a lapse?** Five consecutive sessions is no longer a fluke; worth Matt deciding whether the ritual-open habit needs a stronger nudge, or whether cold-open sessions are simply how he's using Code now and the doc should say so.
