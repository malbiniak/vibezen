# Model Routing (template)

> **Template.** The rule and the tier logic are INVARIANT. Concrete model names are PARAMETER — they age; re-resolve them at each project's Phase 0.

**Rule (INVARIANT — extended by Brief 007): for every task, pick the cheapest combination of execution pattern, model, and reasoning effort that gets full quality — escalate only when stakes or difficulty demand.** The original form ("match the model to how expensive a mistake is, not how hard the task feels") is the same rule on the model axis alone.

| Situation | Tier | Why |
|---|---|---|
| Session 0 | **Most capable** | Errors here compound for weeks; the most quality-sensitive moment in the project |
| Design-sprint interviews (Brief 003) | **Most capable** | Design errors compound into every build they feed; same stakes as Session 0 |
| Building sessions | **Fast execution** | Excellent execution against a gated spec; the readiness gate has already removed the judgment calls, leaving routing and sequencing — a contractor working to plans (Brief 003) |
| Thinking sessions (SPEC-changing) | **Most capable** | Conceptual work with the repo in view |
| Retro (JOURNAL read) | **Most capable** | Pattern-finding across weeks of process |
| Execution tier fails the same thing twice | **Escalate to most capable** | Repeated failure means the problem is conceptual, not mechanical |
| Phase 0 — template instantiation (Code, from the playbook repo) | **Most capable** | Founding decisions; same compounding stakes as Session 0 |
| Subagent swarms — review finders, verify passes, readiness gate | **Fast execution** | High-volume, disposable, cross-checked by the verify pass + tests + operator; never inherits the session model (Brief 002; gate added by Brief 003) |
| Chat (outside Code) | Pressure-tests and meta only | Project thinking lives in Code where the repo is visible; Chat output lands as decision briefs |

**The cheapest tier (PARAMETER — re-scoped by Brief 007).** For the **driver**, the default stays never: the proven configuration was low session volume with high stakes per session. For **delegated well-defined micro-tasks** — mechanical edits, scoped searches, format conversions, easily verified — the cheapest tier is exactly the fit: genuinely high-volume, low-stakes work, which is what the original "revisit if" clause anticipated.

**Driver vs. swarms (INVARIANT — Brief 002).** Every other row above, and the cheapest-tier driver default, describe the **driver** model — the one conversation doing the work. Subagent swarms route independently per their row and never inherit the session model. Cheap is safe for swarms precisely because the intelligence lives in the repo and the verification structure, not in the individual finder — the same reason the routing works at all.

**The pattern ladder (INVARIANT — Brief 007, generalizing Brief 006).** Before the tier question comes the pattern question: **inline → single agent → swarm/orchestrated workflow**, cheapest pattern first. Inline is the default; a single delegated agent when the work is separable and its output compact; fan-out only for what *earns* it — real-data review gates, audits, batch builds (the codified swarms of Briefs 002/003 are deliberate by construction). Neither "never fan out" nor "always fan out" — judgment against mistake cost, not a fixed rule. And manage the driver's own context (Brief 006): `/compact` on a heavy mid-session context, `/clear` when switching tasks. All safe because the repo carries the memory (Principle 5); see `CLAUDE.template.md`'s session-economy and task-routing ground rules.

**Effort is a routing axis; assignment is explicit (INVARIANT — Brief 007).** Reasoning effort routes like tier: **low** for mechanical, well-defined delegated stages; higher effort reserved for the hardest verify/judge passes and the driver's own judgment work. And **every delegated agent gets model and effort set explicitly at spawn** — a spawn with no override silently inherits the session model at default effort, the most expensive possible combination for what is usually the cheapest possible work. Extends Brief 002's "never inherits the session model" from codified swarms to all delegation.

**Worked example — names as of 2026-07 (the names age; the rule doesn't):** most capable / driver = Fable (Opus where Fable is unavailable); hard verify/judge = Opus — cheaper than the driver, stronger than execution; fast execution = Sonnet (Sonnet 5 — a tier tuned for agentic orchestration, a natural fit for driving gated builds; Brief 003); cheapest = Haiku (delegated micro-tasks only; never the driver — Brief 007).

**Why the routing works (INVARIANT):** cheap fast models are safe exactly when the intelligence is stored in the repo instead of in the model's improvisation. The routing table is downstream of the file discipline, not independent of it.
