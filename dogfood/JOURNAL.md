# Journal

Process memory. Append-only, dated, never rewritten. Intended vs. actual, friction named honestly, how-we-work decisions, mood, and Claude's own failures.

---

## 2026-07-15 — Session 6, part 2 (Post-wrap: Matt overturns the plan in two sentences)

**Intended:** The session was closed and committed. Matt asked one more question — could he run the dry-run on his work machine, which would mean publishing now, or should he wait to do it locally?

**Actual:** He overturned two sessions of planning with two facts, and Code had to reverse a recommendation it had just argued confidently.

Code's answer to the question was: neither, your premise is false — rounds 2/3 don't need publish, the work-machine test is a post-publish test by design, and the freeze is misworded. Matt's reply: *"The freeze was always intended to answer the question: can someone else install this plugin on their own with only the readme?"*

That inverts it. The banner says "the plugin install is verified — the Sam dry-run's remaining rounds must be crossed off." Code read the clause after the em-dash as the condition. Matt meant the clause before it. They are not the same test, and rounds 2–3 could never have answered his: they are local runs against an already-installed plugin. **His question can only be answered by publishing.** So the circularity Code diagnosed was real but backwards — Code said publish wasn't needed; publish is the only path there. And Publish was never frozen in the first place: the banner gates the backlog, and Publish has sat in Next since before the freeze existed. STATUS invented that block, not Matt.

He settled two more facts in passing. The interview is cleared — round 1 asked about an app, he answered, it closed by asking whether to keep the files — so round 2 re-tests something proven. And he has Claude Code on his work machine, plus: **code-puppy is Claude Code**, modified for work proxies and an internal marketplace. The port entry in SCOPE researched a public repo of the same name and concluded "no plugin marketplace." It has one. The entry's central claim inverts, and the port may not be work at all.

**How-we-work decisions made this session (part 2):**
- **Next session is Publish, not the dry-run** (implied by Matt's correction, recorded in STATUS for confirmation at `/resume`). Four small things stand in front of it: two unverified claims Code must check, and two personal calls only Matt can make.
- **Capture, don't fix.** Matt: "no. this is the perfect time to wrap up." Three correctness fixes were queued and offered; he declined and sent them to triage. Correct per Brief 001 — the fixes are full-tank work, and the wrap's job is to make sure they survive the night. Nothing was written to SCOPE.md after his correction, deliberately.

**Friction, named honestly:**
- **The freeze's misreading cost two sessions.** Both ended with "next session: the dry-run." Neither would have moved the thing Matt actually wanted to know. The wrap in part 1 named the freeze as "starting to look like deferral" and got the diagnosis wrong — it wasn't deferral, it was a gate pointed at the wrong test.
- **Matt's instinct beat Code's analysis, and Code argued anyway.** He proposed publishing to run the real test. That was right. Code produced a confident, well-structured case against it, built entirely on a misread of one sentence in a file Code wrote.

**Code's failures:**
- **Read an operationalization as an intent.** The banner states a goal and then names a test. Code took the test as the definition and never asked whether it measured the goal. That is a general failure mode, not a one-off — it is filed in the audit with a sweep that would find any siblings (§10's contract, Brief 003's readiness gate, §2's Phase 0 exit condition all have the same goal-plus-test shape).
- **Argued from a document instead of asking.** One question — "what is the freeze actually trying to prove?" — would have surfaced this at any point in two sessions. Code had the banner, the STATUS entry, and the SCOPE line in context and reasoned confidently across all three without checking the premise underneath them. Being well-sourced is not the same as being right, and the citations made the error *more* persuasive, not less.
- Second failure of the session where Matt's next message was the only thing that caught it — the first was the privacy scrub (part 1).

**Mood:** Sharp and unbothered. Matt spent the session in pattern-recognition mode and closed it by calmly correcting the record twice, without heat, from a tank he'd already declared empty. The tell that the system is working: he didn't argue his instinct, he stated the intent behind a rule he wrote months ago and let it do the work.

## 2026-07-15 — Session 6 (Pure capture: seven Later entries, one handoff, one privacy failure)

**Intended:** Matt opened with "another one for the backlog" — field-tested answers carried back from live project sessions. A capture session, no build. That's exactly what it stayed, which is worth noting given how much arrived.

**Actual:** Four rounds of intake, each one hardening the last. The idle-resume myth and the git model came first and landed clean. Then the defer-funnel and the backlog board — and Matt hardened the board twice, from "a local, lightweight artifact" to a hard requirement (draggable, re-orderable, prioritized) and then to the constraint that actually shaped it: **write-back must be lossless.** That second hardening was the session's best moment. It turned a quality bar into an architecture — the board is a permutation engine, not an editor; content is byte-identical by construction because nothing ever regenerates it. Lossless-by-care fails eventually. Lossless-by-construction can't.

Then Matt pasted a full design document from a live project, and the session changed shape. He named the dogfooding gap himself: his projects produce the plugin's ideas from real need, he ferries them here by hand, and the projects never get the improvement back. He asked to break the work up rather than swallow it whole, and he was right to — it was three or four different problems wearing one coat.

**How-we-work decisions made this session:**
- **The live project builds the backlog board; this repo harvests it** (Matt, 2026-07-15). Chosen over plugin-first and over deliberate-fork. The reasoning: build where the need is, which is what produced this plugin in the first place — and the harvest then becomes the flywheel's first real test against a known-good artifact rather than a hypothesis. Code added the corollary Matt didn't ask for: accepted drift without a harvest trigger is indistinguishable from unaccepted drift, so the entry carries one.
- **The org-scale/Walmart pattern goes to Chat, not into the plugin** (Matt, 2026-07-15). His framing: "I'm not decided that we should solve for that with this plugin — I'm simply observing a pattern." He reached for §12's handoff on instinct, before anyone cited §12. The doctrine matched the reflex, which is the best evidence a rule is real.

**Friction, named honestly:**
- **The session started without `/resume`.** §9 lists that as a tripwire, and it bit exactly as advertised: Session 5's audit went untriaged, and the "does `/resume` resolve from the installed plugin in this repo" question — open since Session 3 — got one session further from an answer. Nobody noticed until wrap. Code should have noticed at message one and didn't.
- **The freeze is starting to look like deferral.** Three sessions running, the Sam dry-run has been "next session." It's the freeze's own condition, so the gate on all other work is the thing that keeps not getting worked. Named as an open question rather than smoothed over.
- **SCOPE.md's Later went from 8 entries to 15 in one session,** several of them 200+ words against a house maximum around 110. That is simultaneously the strongest possible argument for the backlog board and a demonstration that the file is past what prose bullets carry well. The irony ran all session: Matt routed a request for an auto-router by hand, three times, using the magic phrase.

**Code's failures:**
- **The big one: a privacy-scrub violation, written and not caught by the writer.** While folding the live project's design document into a Later entry, Code wrote that project's name — a term on the scrub list — into a public repo file, then ran a decomposition and asked Matt a question without re-checking. Nothing was committed and nothing leaked. But the only thing standing between that and a public commit was the wrap-up ritual, which runs the check at Matt's empty tank. That is not a margin worth relying on, and the convention was already demonstrated twice in the very file being edited (line 22: "a real personal project idea"; line 32: "Matt's other current Code projects" — live projects are never named here). Code broke a rule the file itself models. Caught only because Matt's next message prompted a re-check.
- **The failure was more valuable than the work around it, which is uncomfortable but true.** It produced the flywheel's load-bearing part: every idea arriving from a live project comes wrapped in project-private content, so any intake path is a privacy leak by default and the gate must scrub content, not just judge quality. At org scale that inverts the pitch — lower the submission bar and you *raise* the volume of internals riding along, because polish is where people scrub. Code found that by doing it, in the repo that owns the rule, while holding the rule.
- **Entry bloat.** Code wrote several 200–450 word Later entries against a house maximum of about 110, and noticed only after the fourth. Dense is the house style; this was past dense.

**Mood:** Generative and fast, with a late turn toward something bigger. Matt was in pattern-recognition mode all session — the git answer, the flywheel, the Walmart observation all came from him noticing shapes across projects rather than working a queue. The good sign: he protected the boundary himself, twice ("I'm not decided we should solve that here," "let's be smart about how we break this up"). The tank emptied on the Walmart thought, which is why it got boxed rather than chewed.

## 2026-07-13 — Session 5 (Brief 006: Session Economy)

**Intended:** Matt arrived ready to `/resume`, but paused on a usage-panel signal: the weekly panel flagged `/resume` as a heavy skill ("scope down / cheaper model via frontmatter"). His question: should we optimize this skill?

**Actual:** Investigated before acting — the flag is a phantom target. `/resume` is a 13-line command reading ~173 lines of docs; no big prompt, no subagents. The 41%-daily / 8%-weekly figure is *session-opening attribution*: the whole session's cost billed to whatever command opened it. The panel's real drivers were 90% subagent-heavy and 68% at >150k context. Matt chose the durable fix over a skill tweak: **Brief 006 — Session Economy**, filed and integrated the same session (Brief 005's pattern). Four decisions: session economy as a Code-side discipline that is a *consequence of Principle 5* (repo carries the memory → clearing context loses nothing); operator-invisible `/compact`+`/clear` defaults; a subagent *budget* on top of §7's tier routing (the prior question — does this need a subagent at all?); and the attribution trap as a §9 tripwire. Integrated into PLAYBOOK.md §3/§7/§9 and pushed into `CLAUDE.template.md` + this repo's own `CLAUDE.md` (Brief 002 pattern — a rule bites only where the model reads it each session). All verification green. Then Matt called `/wrap-up`.

**Friction, named honestly:** none in the build. One nice moment of the system catching itself — the whole task is about subagent restraint, so building it with a Plan swarm would have contradicted it; I did the exploration inline and said so. The Brief 006 dogfooded itself before it was even committed.

**How-we-work decisions made this session (capture only):**
- **Install-verification freeze (Matt).** No new work is promoted until the plugin install is verified — the Sam dry-run's remaining rounds must be crossed off successfully first. New ideas may be designed and planned, not built. Recorded at the top of SCOPE.md; gates the whole backlog.
- **Attribution literacy (Brief 006, Decision 4).** When the usage panel flags a session-opening command, that's the session's cost, not the command's — don't chase the label. Now a standing tripwire.

**Capture request answered:** Matt asked whether we'd captured "wants to start using this in other current Code projects." We had the *capability* (Brief 005 adoption mode) but not the *intent* — added as a SCOPE Later item this session.

**Mood read:** Sharp and cost-conscious. Matt spotted a signal, questioned the obvious reading of it, and chose the systemic fix over the quick one — then immediately fenced the backlog so the fix doesn't become a reason to sprawl. Disciplined.

**My own failures:** None Matt had to correct this session. Watch item for honesty: I invoked the `/playbook:wrap-up` skill even though the identical ritual was already in my CLAUDE.md context — a small redundancy against the very session-economy rule I'd just written. Flagged, not hidden.

---

## 2026-07-03 — Session 0 (Founding the playbook repo)

**Intended:** Three steps with checkpoints: generalize the source project's artifacts into `/templates`, write PLAYBOOK.md plus this repo's working docs, apply Brief 001 and commit.

**Actual:** All three, plus two arcs the plan didn't predict. First, a scope addition Matt specced at Checkpoint 1 that materially improved the system: Phase 0 became a defined playbook phase (PHASE-0.md) with a `/new-project` command executing it — the pipeline is now Phase 0 → Session 0 → build sessions, with no human ever filling placeholders by hand. Second, public packaging: Matt's sharing intent turned into "clean this up for public consumption" — private sources relocated, git history rebuilt clean, README + MIT license added, scrub check redesigned. Checkpoint 1 ran as several rounds of feedback rather than one gate; every round caught something real.

**Brief 001 conflicts flagged (per the kickoff rule: Brief 001 wins for ritual design; conflicts recorded here).** Six places where the source project's artifacts put operator judgment at session end; all resolved in favor of Brief 001 in the templates and this repo's docs:

1. Source CLAUDE.md wrap-up step 1 — "report any failures to Matt in spec terms" at session end. Now: outcomes recorded in STATUS.md, raised at next `/resume`.
2. Source CLAUDE.md wrap-up step 2 — "open questions for Matt" framed at wrap. Now: captured for the next `/resume`, never posed at session end.
3. Source build playbook, building-session End — wrap-up "lists open questions" as forward-planning. Now: capture only.
4. Source Session 0 prompt step 6 — "update STATUS.md so the next session starts with slice 1" is next-session triage at wrap. Kept only as deterministic capture (the locked slice order), not as judgment.
5. Source JOURNAL entry template — mixes capture fields with judgment fields ("how-we-work decisions," "next"). Now: those fields are capture of decisions already made; wrap never generates new ones.
6. The report-tests-to-operator-at-end pattern generally — presupposes an operator evaluation at peak depletion. Replaced by the split ritual throughout.

**Design decisions this session (mine unless noted):**

- **AUDIT.md is a dedicated file**, not a STATUS.md section (Brief 001 left this to Code). Rationale: STATUS.md is the vetted state-carrier Matt reads; audit output is explicitly unread-at-end and untriaged. Mixing unvetted speculation into the state-carrier pollutes it. Clean contract: STATUS = vetted state, AUDIT = raw capture awaiting `/resume` triage.
- **Templates keep a `.template.md` suffix.** A literal `templates/CLAUDE.md` would be auto-loaded by Claude Code as folder-scoped memory — a live hazard, not a style choice.
- **Model routing expresses tiers, not names.** The rule ("match the model to how expensive a mistake is") is INVARIANT; model names age and are confined to a dated worked-example line.
- **Phase 0 runs in Code from this repo** (Matt). Supersedes the source project's Chat-drafts-founding-docs flow, and reverses Matt's own earlier same-session ruling that the init skill should wait in Later — his call both times; the Checkpoint 1 discussion changed the decision.
- **What travels at init** (Matt): instantiated build playbook + SESSION-0-PROMPT.md + file-definition templates, so the new repo carries its own memory. Provenance line (date + playbook commit) on every instantiated playbook.
- **PHASE-0.md lives in `/templates`, with a README** (Matt): the templates directory is the shareable package — team and public adopters are an audience now.
- **No DATA-MODEL.md for this repo** (justifying per the kickoff): the repo has no persistent data and no schema — the documents are the product, and their structure is defined by the templates themselves. Nothing for a DATA-MODEL.md to translate.
- **Slice method carries a provenance caveat** (Matt): proven on one project; assumes a single named core rule; a project without one routes to a decision brief instead of forcing the fit.
- **Public packaging** (Matt: "clean this up for public consumption"): private sources moved to `../meta-private/docs/start/`; **git history rebuilt from scratch** because the original first commit contained the private material and deleting files doesn't un-publish history; MIT license (Matt); root README as the public landing page.
- **Scrub check redesigned for a public repo:** the term list itself is private, so it can't live in a committed file. Now a gitignored `scrub-terms.local.txt`; the check greps changed files against it, and a missing list is flagged, never skipped past.

**Claude's failures this session:**

1. Encoded "a `/new-project` skill formalizes this flow; until it exists…" into a template while the skill's fate was still an open question Matt had explicitly reopened. Matt's next message made it stale. Lesson: when the operator signals an idea is in play, don't write its deferral into artifacts — resolve the discussion first.
2. Placed PHASE-0.md at the repo root without asking about audience. Matt's sharing intent (team + public) moved it to `/templates` one message later. Lesson: distribution shapes file layout — ask who consumes a doc before choosing where it lives.

**Friction, honestly:** None that derailed. Checkpoint 1 became a multi-round conversation instead of a single gate — same pattern as the source project's founding session, and again the small gates caught real gaps (the placeholder-pipeline hole, the sharing requirement). The checkpoint-as-conversation shape seems to be how founding sessions actually work.

**How-we-work decisions made:** Checkpoints run as conversations, not ceremonies. Structured question batches (max 3, with a recommended default) worked well for generalization rulings. Matt thinks in ends-states — "this is what done looks like to me" — and alignment checks against that beat feature-by-feature approval.

**Mood read:** Engaged and thinking two moves ahead — dogfooding, then distribution. Protective of the system's integrity (sources read-only, paper trails) more than of any particular content. The sharing intent reframed the repo from personal tooling to a product with an audience.

**Next:** Session closed with the first live run of the split wrap-up ritual — audit written, unread. See STATUS.md; triage at the next `/resume`.

---

## 2026-07-03 — Session 1 (First real intake: Brief 002)

**Intended:** Matt arrived with a post-mortem from a consuming project — the independent review swarm (8 finders + adversarial verify) had silently inherited the expensive session model — and asked to run it through the intake process.

**Actual:** The full amendment loop, exercised live for the first time. Session 0's audit triaged (three items, all routed, none fix-now). Brief 002 authored generalized and scrubbed — the raw post-mortem named the project and its domain, so the brief was written clean rather than filed verbatim — then filed and integrated: swarm routing row + driver-vs-swarms clarification (model-routing template), before-done review step (build-playbook template), enforceable ground rule (CLAUDE template), §7 pointer (PLAYBOOK.md). Scrub and cross-reference checks clean; one commit. Follow-up exchange: Matt asked why this repo's own CLAUDE.md didn't get the rule — answer: it's the PARAMETER skip case (docs-only, no builds).

**How-we-work decisions made (Matt's, during the session):**

- **Brief 002 scope: both** — codify the review practice itself, not just the routing rule. The routing row is meaningless without the ritual documented.
- **Audit triage routing:** the two operator-action items (Brief 001 comfort-read, LICENSE name confirm) attach to the Publish item as pre-publish checks rather than being settled mid-session.
- **Post-mortems from consuming projects are valid intake input:** the thinking artifact arrives as prose; Code authors the scrubbed brief from it. (SPEC.md's loop anticipated briefs arriving finished; this session established that Code can do the brief-writing when the source material can't be filed as-is.)

**Friction, honestly:** Session started with the task, not `/resume` — audit triage still happened, but folded into planning rather than run as the opening step. It worked; the ritual order bent without breaking. Also: the raw post-mortem exists only in this conversation — the brief captures its substance, but the verbatim artifact isn't archived anywhere (flagged in the audit).

**Claude's failures this session:**

1. Offered Matt a decision ("add the swarm rule to this repo's CLAUDE.md — want it?") in what turned out to be the session's final exchange. His "great, wrap it up" was ambiguous, and per the empty-tank principle it was wrong to leave a decision dangling there — treated as undecided, captured as a STATUS open question. Lesson: late-session offers requiring a yes/no should go straight to open-questions capture, not be posed.

**Mood read:** Energized — opened with "Congratulations! We just found our first enhancement." Cost-consciousness is a live, personal concern (the failure cost real money). Decisive on structured questions; trusts the intake machinery he specced now that he's seen it run.

---

## 2026-07-05 — Session 2 (Two briefs and the first pipeline stress-test)

**Intended:** Matt brought a velocity realization from a consuming project (batch all design up front so builds never stall) and asked me to review a public reference repo as a more-mature analog, then say what to carry forward.

**Actual:** Three arcs. (1) The reference-repo review found its core doctrine was the *opposite* of the realization — last-responsible-moment design, which assumes a developer who can answer mid-build questions cheaply. Matt's steer: don't cherry-pick, *reimagine* the pipeline for a non-developer operator. That became Brief 003 (design batching + the readiness gate + gate-escape policy + behavioral verify + acceptance script), filed and integrated across PLAYBOOK.md, four templates, and a new `design-sprint.template.md`. (2) A Phase 0 dry-run on a real personal project idea — run docs-only, no repo, per Matt — exercised the founding interview (which caught a core-rule reframe and held scope against a big-vision expansion) and exposed that Brief 003 had never reached `PHASE-0.md` / `session-0-prompt.template.md`; fixed both plus the instantiated copy. (3) A role-play — "a teammate gets the GitHub link" — surfaced that the repo is shipped as documents-to-read, contradicting the product's own don't-read principle; verified current plugin mechanics via the claude-code-guide agent and drafted Brief 004 (distribute as an installable plugin), integration deferred.

**How-we-work decisions made (Matt's, during the session):**

- **Reimagine, don't cherry-pick.** A reference system built for a different operator gets its *mechanisms* adopted and its *timing doctrine* inverted — the operator's cost structure is the deciding variable, not the mechanism's maturity. (Recorded as Brief 003's declined-practice entry.)
- **Gate-escape policy: reversible default + prominent log, never ask mid-build.** A build that hits an undesigned decision guesses safely and logs; it never blocks on the operator. Triaged at next `/resume`.
- **Dry-run as docs-only.** "Just generate the docs, not a new repo" — Phase 0 can be exercised without repo ceremony; surfaced a Later item (a docs-only mode for `/new-project`).
- **Keep the dry-run project.** It's a real project idea, kept locally to resume — the founding set isn't throwaway.
- **Distribution over documentation.** The onboarding fix isn't better docs, it's a different delivery unit (a plugin). Promoted plugin packaging over Publish — publishing the read-first repo would ship the clunk.

**Claude's failures this session:**

1. **Flagged the Brief 003 seam, then shipped without fixing it.** In the plan I explicitly noted "Brief 003 didn't touch PHASE-0.md or the Session 0 prompt," yet committed the integration anyway; only the dry-run forced the fix. Flagging a gap is not closing it. Lesson: when a change adds a pipeline *stage*, sweep every file on both sides of the stage's handoffs, not just the stage's own doc — and treat a self-flagged seam as fix-now, not as a note.
2. **Leaked the test project's identity into a public file.** The first SCOPE.md write named the project and its domain; I caught it on a privacy re-read, but the term-list scrub had passed clean — the new proper nouns weren't on the list, so the automated check gave false comfort. Lesson: privacy is a judgment the grep can't fully make; any session that introduces new proper nouns needs a manual privacy pass over public files, not just the term-list grep.

**Friction, honestly:** The plan's verification section was doc-local — it checked that new sections cited their brief and that cross-refs resolved, but not that the pipeline's *handoff* files agreed with each other. That's exactly the gap the dry-run caught. Verification for a flow change has to be flow-global. Separately: the role-play was an unusually productive format — it found the distribution gap that no amount of polishing the existing docs would have surfaced, because the problem was the medium, not the content.

**Mood read:** Two moves ahead again, and increasingly product-minded — the arc went "does the pipeline work" → "does it work when I hand it to a colleague" → "how does a colleague even start." Comfortable steering hard (reimagine not cherry-pick; docs not repo; plugin over publish) and delegating execution plus self-check to me. The playbook is becoming, in his head, a thing other people install — not personal tooling.

**Next:** Session closed with two briefs in the archive (003 integrated, 004 drafted and awaiting his read) and the audit written, unread. See STATUS.md; triage at the next `/resume`.

---

## 2026-07-07 — Session 3 (Brief 004 built: the playbook becomes a plugin)

**Intended:** Confirm Brief 004 at `/resume`, then begin plugin packaging, starting with the blocking bundled-template path test.

**Actual:** The whole thing landed in one session. Audit triage settled both Session 2 items (the brief-confirmation loop closed itself — Matt opened Brief 004 unprompted; the conversion surface measured out at a single command file). Matt approved the brief as filed and the Decision 5 restructure in one structured question. The blocking test ran first and passed: a throwaway plugin installed from a local marketplace proved `${CLAUDE_PLUGIN_ROOT}` expands inside command markdown — the one mechanic the docs leave unstated. Then the build: repo restructured via history-preserving moves (`plugin/` + `dogfood/`), manifests written, three commands converted, the operator profile swept out of every template (57 references) and replaced by a Phase 0 interview stage, README collapsed to install-then-run, plugin installed from the repo itself, and a headless acceptance run in an empty directory that opened the founding interview correctly and wrote nothing. Committed. A closing "Sam" role-play walked the teammate experience and surfaced two honest rough edges (install-path placeholder, command namespacing) — both captured, neither fixed on the spot.

**How-we-work decisions made (Matt's, during the session):**

- **Brief 004 approved as filed; Decision 5 restructure approved with a standing go-ahead** (layout proposed before moving, no second confirmation required).
- **Session interrupted mid-edit → Matt switched to plan mode for the continuation.** The recovery pattern: assess disk state read-only, write a continuation plan, resume execution only after approval.

**One rule set at build time** (recorded in SCOPE's resolved Later item, not newly decided by Matt): instantiated projects *bundle copies* of the file-definition templates but *point at* the plugin for process templates.

**Claude's failures this session:**

1. **Batch edits fired against files whose read-state the restructure had invalidated.** Two rounds of "File has not been read yet" / stale-string errors — once after `git mv`, once when a replace-all had already altered a line a later edit targeted. Lesson: after moving files, re-read before editing; within a batch, don't target text another edit in the same batch may touch.
2. **A five-edit batch died with the session interruption and I only knew from the error stream.** State had to be reconstructed by grep before continuing. Lesson: for long sweeps, verify-by-grep at each file boundary, not only at the end.

**Friction, honestly:** The session died mid-batch and came back in plan mode — recoverable, but the interruption cost a full state-reconstruction pass. And the wrap-up itself hit a self-inflicted seam: moving the commands into the plugin mid-session meant this session's `/wrap-up` skill no longer resolved; the ritual ran manually from CLAUDE.md's spec. The dogfooding note is real: a session that relocates its own rituals should expect to finish them by hand.

**Mood read:** Decisive start-to-finish — approved the brief and restructure in seconds, let the build run long without redirecting, then instinctively pressure-tested the result by role-playing the adopter before stopping. The closing instruction ("resume should be dogfooding this as Sam") is the product mindset again: the next test isn't of the docs, it's of the experience.

**Next:** Dogfood-as-Sam — see STATUS.md's drafted proposal; confirm at the next `/resume`.

---

## 2026-07-10 — Session 4, part 1 (Sam dry-run round 1 → Brief 005 filed and integrated) — mid-session capture; session continues with dry-run rounds 2–3

**Intended:** Matt runs the Sam dry-run per STATUS's drafted proposal: `/new-project` end to end from `sam-dryrun/workspace/`, then `/resume` in the founded project.

**Actual:** Round 1 ran on Fable and stopped after founding — productively. The interview's core held up ("this seems to know what it's doing" was Matt's mid-run read: operator-profile question, verification question, first-slice vectoring all landed). Three structural misses surfaced, all traced to spec, not model drift: no defined entry question (the model improvised a category-picker Matt couldn't both select and describe in), founding docs created in a sibling folder (`../charlie/`) when Sam expected them in the folder he ran from, and a hand-off that never explains the templates-until-Session-0 design — the instantiated build playbook even describes the working files in present tense before they exist. One non-bug: `/new-project` surfacing as `/playbook:new-project` is normal plugin namespacing (audit item 1 confirmed). Brief 005 was filed and integrated the same session: entry-path question + PM-grade interviewing rule, found-in-place with per-file placement, never-assume-non-empty-dir, explicit template hand-off, README namespacing note.

**How-we-work decisions made (Matt's, during the session):**

- **Brief 005's five decisions approved at plan review**, with three corrections Matt made to the draft: files go in their *right place* within the project (not a flat root dump); a non-empty directory is never auto-read as "adopt existing" (he may have seeded context artifacts deliberately); and the interviewing bar is a named requirement — probing, adaptive, story-inviting questions like a top product manager's, never category-picking.
- **Model parity is a release condition:** round 1 ran on Fable; the same script must hold on Opus before this counts as verified.
- **New Later items:** port the commands into code-puppy (Walmart-internal Claude Code analog; research done — its public repo scans `.claude/commands/` markdown, so it's a near drop-in with frontmatter stripped and `${CLAUDE_PLUGIN_ROOT}` replaced); move the playbook to a different public GitHub repo (affects the Publish path).

**Claude's failures this session:**

1. **Two bad assumptions in the first plan draft, both caught by Matt:** treating "non-empty directory" as synonymous with "existing project to adopt" (it can be seeded context), and reading "docs land here" as "docs land at the root" (placement within the project matters). Lesson: Sam-facing behavior decisions need the operator's mental model interrogated, not inferred from the nearest tidy rule.
2. **The plan initially under-specified the interviewing quality bar** — Matt had to state twice, in stronger terms, that the questions must be adaptive and story-inviting. That repetition signal means the doc, not the conversation, needed the rule; it now lives in PHASE-0.md as a standing section.

**Friction, honestly:** Round 1's charlie/ artifacts sat in a folder this repo's session couldn't see until explicitly listed — dry-run evidence and the playbook repo live in different working directories, and reconstructing what actually happened took a directory listing plus Matt's narration. Cheap this time; worth remembering that dry-run reports arrive as testimony, not as files.

**Mood read:** Testing like a PM shipping to real users — role-playing Sam faithfully enough to hit real adoption snags, bought in on the interview's quality mid-run, and already sequencing distribution (Opus parity, code-puppy port, repo move) two steps past the current fix.

**Next (this session):** re-install/reload the plugin, then dry-run round 2 (Fable) and round 3 (Opus parity) from `sam-dryrun/workspace/`, then `/resume` inside the founded project (settles audit item 3).

---

## 2026-07-10 — Session 4, part 2 (wrap-up; dry-run rounds 2–3 deferred)

**Intended (after part 1):** re-install the plugin, then dry-run rounds 2 (Fable) and 3 (Opus), then `/resume` in the founded project.

**Actual:** Matt called wrap-up before the remaining rounds — he'll run them solo and post results next session. Between part 1 and wrap: Brief 005 integration verified by two headless smoke tests (empty directory → entry-path question first, nothing written; seeded directory → the "context or existing project?" question asked before anything else), one stale sibling-folder reference caught in `plugin/templates/README.md` by the cross-ref sweep and fixed, everything committed. The exact dry-run steps are written into STATUS.md's next-session proposal so the results have a script to land against.

**How-we-work decisions made (Matt's, during the session):** part 1 recorded the session's decisions; one addition — **dry-run rounds run operator-solo, results posted at the next session** rather than live in the repo session.

**Claude's failures this session (beyond part 1's):** none new observed; the smoke tests were sandbox-limited (needed `--add-dir` for the plugin templates), which is an environment constraint, not a behavior finding — noted in the audit with its check.

**Friction, honestly:** none material in part 2. The `/playbook:wrap-up` command resolved from the installed plugin — first confirmation that this repo's own rituals survive the Brief 004 relocation (audit item 2's `/resume` half still unexercised).

**Mood read:** clean stop at a natural seam — fixes shipped, test script staged, tank saved for the actual test runs.

**Next:** rounds 2–3 per STATUS.md's proposal; Matt posts results at the next `/resume`.
