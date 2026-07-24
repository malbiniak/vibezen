# Build Playbook — `<project name>` (template)

> **Template.** Instantiated by the playbook plugin's `/new-project` command at Phase 0 (defined in `PHASE-0.md`; Brief 004): the interview fills every `<placeholder>`, and copies of this file, `SESSION-0-PROMPT.md`, and the file-definition templates land in the new project's repo (template notes deleted, provenance line added). The plugin's bundled source templates are never modified. **INVARIANT** sections keep their substance in every project; **PARAMETER** marks per-project decisions. Ritual design follows Brief 001 (see PLAYBOOK.md in the playbook plugin).

The operating model for building `<project name>` as `<operator descriptor — e.g. "a solo non-developer", from the Phase 0 operator profile (Brief 004, Decision 3)>`, using Claude Code as the single source of truth. Chat and design tools are consultants; the repo is the boss.

---

## Core principles (INVARIANT)

1. **The repo is the only source of truth.** Nothing is real until it's in a file in the repo. Conversations, mockups, and ideas travel as short instructions to Code, never as artifacts to import.
2. **Minimize the rooms where truth is interpreted.** One repo, one tool (Code) that reads and writes it, one person (the operator) who approves.
3. **Behavior is the fixed point; implementation is negotiable.** `<the project's named core rule and key workflows>` are the product. Layout, stack, and structure serve them, never the reverse.
4. **The operator never touches `<what their profile rules out — e.g. schemas, foreign keys, code>`.** They describe behavior, verify by using what was built, and answer questions. Code translates and explains back in plain language.
5. **Restart cost must be near zero.** The project carries its own memory. The operator is not the state-carrier.

---

## The working files (all maintained by Code)

**These files do not exist yet at Phase 0.** Session 0 creates every one of them from the `.template.md` files that Phase 0 placed in `templates/` — that is Session 0's whole job (Brief 005, Decision 4). They live at `<docs location — confirmed at the Phase 0 checkpoint, e.g. the repo root or docs/>`, except CLAUDE.md, which convention puts at the repo root.

| File | Created | Job | Changes | Who triggers changes |
|---|---|---|---|---|
| **SPEC.md** | Session 0 | What the product does, behavioral, plain language. Personas and per-persona user stories. Explicit non-goals. | Rarely, deliberately | The operator, via one-sentence instruction; Code announces "this changes the spec" |
| **SCOPE.md** | Session 0 | Now / Next / Later. Slice order + backlog. Every new idea goes to Later. | When promoting slices or parking ideas | The operator says "add to Later" or "promote X" |
| **CLAUDE.md** | Session 0 | Instructions for Claude Code: read SPEC/SCOPE/STATUS first; split wrap-up ritual (Brief 001); never build outside Now without asking; log its own failures. | Almost never | The operator, if the process itself changes |
| **DATA-MODEL.md** | Session 0 | Schema + plain-language translation. The operator only reads the plain-language half. *(PARAMETER — only for projects with persistent data.)* | Rarely, alongside SPEC changes | Code, announced |
| **STATUS.md** | Session 0 | Product memory: what works, what's half-done, what's next, open questions for the operator. | Every session | Code, automatically |
| **JOURNAL.md** | Session 0 | Process memory: intended vs. actual, friction named honestly, how-we-work decisions, mood read, Claude's own failures. Append-only, dated, never rewritten. | Every session + notable mid-session moments | Code, automatically |

Brief 001 adds one more: **AUDIT.md** — the wrap-up self-audit's capture file, first written by Code at a session's end, read only at the next `/resume` (see the wrap-up ritual below).

---

## Slice order (method INVARIANT; the slices themselves PARAMETER)

The method lives in `slice-method.template.md` (playbook plugin). This project's slices:

1. **Slice 1 — `<the core rule, proven on hand-entered data>`.** `<What it unlocks, stated behaviorally.>`
2. **Slice 2 — `<name>`.** `<The concrete moment it serves.>`
3. `<…>`

Once the design sprint has run, every slice carries two documents — a design doc (WHY) and a build spec (WHAT) — and no slice enters a build session until the readiness gate passes its spec (Brief 003; skeletons and gate checklist in `design-sprint.template.md`, playbook plugin).

---

## The sequence

### Phase 0 — Founding (Code, `/new-project` from the installed playbook plugin — Brief 004; run from the project's own directory — Brief 005)
The founding conversation, defined in the plugin's `PHASE-0.md`: entry path (discovery sprint / one-liner / point at context) → retro on prior build failures → behavioral vision → personas (including the operator profile) → scope negotiation → excavation. Exit when Session 0's placeholder contract is satisfiable without invention; then, on the operator's confirmation, the instantiated playbook, `SESSION-0-PROMPT.md`, and file-definition templates land in the project's directory, each in its confirmed place. Source templates are read-only. After Phase 0, all project thinking lives in the project's own repo; Chat hosts only pressure-tests and meta thinking, which land as decision briefs in the playbook repo.

### Session 0 — Kickoff (Code, most capable tier)
No code written. Claude:
1. Interviews the operator about the domain: the people involved and what they can take on, how the work happens today, existing resources, current priorities.
2. Writes SPEC.md (including per-persona user stories), SCOPE.md, CLAUDE.md, DATA-MODEL.md (if the project has persistent data), STATUS.md, JOURNAL.md.
3. Creates the `/resume` slash command (definition in PLAYBOOK.md rituals; Brief 001).
4. Explains the data model back in domain language. The operator verifies by whether the described behavior is right, never by reading the schema.

### Design sprint (Code, most capable tier) — Brief 003
A short run of interview-driven design sessions covering the entire Now/Next queue, run **before** any build session — full-tank work, at session start (Brief 001's energy-cycle principle). Per design, in order:
1. The operator approves a plain-language **Problem + Solution**. The interview does not proceed past this until they confirm the direction.
2. Code writes the design doc — the WHY: rationale, behavior semantics, constraints, what doesn't change.
3. Code derives the build spec — the WHAT: contracts, phases, plain-language acceptance criteria. No operator time; no duplication between the two documents.
4. The **readiness gate** runs: a fresh-context adversarial swarm (fast-execution tier, Brief 002 routing) hunts undesigned decisions — ambiguity, unstated assumptions, weasel words ("appropriate," "as needed," "etc."). Findings go to the next interview's agenda, never to a builder. A slice is **executable** when the gate finds nothing.

The sprint exits when every queued slice passes — the exit is the gate, not a session count. Doc skeletons and the gate checklist: `design-sprint.template.md` (playbook plugin).

### Building sessions (Code, fast execution tier)
- **Start:** `/resume` — triage the latest AUDIT.md entry with the operator first (Brief 001), then approve or redirect the proposed goal. Only gate-passed slices enter a build (Brief 003).
- **During:** one slice item per session. New ideas → "add to Later." Scope creep is the enemy; the backlog absorbs it.
- **Mid-build (Brief 003):** never ask the operator a design question mid-build. An undesigned decision that escaped the gate gets the safest easily-reversible default, a prominent log (STATUS.md open questions + the wrap-up audit entry), and the build keeps moving — triaged at the next `/resume`, where a wrong default costs one revert.
- **Before "done" (Brief 002):** any slice that writes real data gets the independent multi-angle review before the build is called done — finder subagents across correctness / reuse / simplification / efficiency / altitude / conventions, then an adversarial-verify pass over their findings. The verify pass, the test suite, and the operator are the real gate; the finders feed it cheaply from many angles. The swarm routes per the model-routing table: fast-execution tier, never the session model. **Then the behavioral spec-fidelity pass (Brief 003):** every requirement in the build spec extracted into a checklist and traced through the built behavior — the spec is the oracle; this catches correct-looking work that does the wrong thing. Swarm discipline throughout (Brief 003): fixed prompt templates for swarm subagents, capped subagent output, no repeated file reads.
- **After verify (Brief 003):** Code generates the **acceptance script** — a plain-language "try these N things" checklist drawn from the build spec's acceptance criteria. The operator works it async by using the app: accept; "behavior X is wrong" (routes to the fix queue); or roll the slice back (Code does all git work). It never blocks the next build.
- **End:** "wrap up" — pure capture, zero operator judgment (Brief 001). Code updates STATUS.md and JOURNAL.md, writes the self-audit to AUDIT.md (the operator does not read it now), commits. Open questions are captured in STATUS.md and raised at the next `/resume`, never pushed on the operator at session end. If the operator bails mid-session, the next `/resume` reports the half-done state honestly.
- **The operator's homework between sessions:** answer STATUS.md's open-questions list and work any pending acceptance script. That's it.

### Thinking sessions (Code, most capable tier)
When a decision might change SPEC.md: `/resume`, then "don't build anything today — I want to think through X." Claude reasons with the actual spec and code in view; decisions land in SPEC.md immediately, no handoff.

### Retro sessions (Code, most capable tier) — every `<5 sessions or 3 weeks>` (PARAMETER), whichever first
"Read JOURNAL.md end to end and tell me what patterns you see." Scheduled *before* failure, because stalls surface weeks after their causes. If the project dies, JOURNAL.md is the autopsy; if it lives, it's the reusable playbook for the next build.

### Design moments (design tool) — PARAMETER: UI projects only; reactive, per-screen, only after a slice works
Trigger: a screen you've actually used feels wrong.
1. Screenshot the real screen, explore alternatives in the design tool.
2. Conclusions travel as *proposals*, not artifacts: tell Code "Design suggested X — check it against our data model and tell me what it changes." Code is the reviewer; it can see the wiring the design tool can't.
3. Handoff-to-Code is allowed only as a scoped import of one screen's frontend, for a screen whose behavior is already proven, reviewed by Code.

Never design the whole product visually first — the mockup would become the spec and behavior would end up negotiating with layout.

---

## Model routing

**Rule (INVARIANT): match the model to how expensive a mistake is, not how hard the task feels.** The routing table lives in `model-routing.template.md` (playbook plugin). Subagent swarms — review finders, verify passes, and the readiness gate — route independently of the driver: fast-execution tier, never the session model (Brief 002; extended by Brief 003). Design-sprint interviews ride the most capable tier; the build-session driver stays on the fast-execution tier because the gate has already removed the judgment calls (Brief 003).

---

## The operator's job description (the whole thing) — INVARIANT

- Run `/resume` to start (audit triage rides on it — Brief 001), "wrap up" to end.
- Read STATUS.md's plain-language sections; answer its open questions between sessions.
- Guard the Now list; park everything else in Later.
- Describe behavior; verify by using what was built.
- Sit the design-sprint interviews; approve each design's plain-language Problem + Solution (Brief 003).
- Work the acceptance script when one lands — try the listed things in the app, async (Brief 003).
- Approve SPEC changes; notice when Code announces one.
- Show up to the scheduled retro even when things feel fine.

## Failure tripwires (INVARIANT — watch for these)

- Sessions starting without `/resume` → duplicated or drifting work.
- Mid-slice scope creep ("it felt quick").
- The operator re-explaining something twice → SPEC.md is ambiguous; fix the file, not the conversation.
- A week away feeling like a cold start → STATUS.md discipline has slipped.
- Importing artifacts instead of issuing instructions → the drift machine is back.
