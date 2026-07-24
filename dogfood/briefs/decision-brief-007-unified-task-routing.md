# Decision Brief 007 — Unified Task Routing: Pattern + Model + Effort per Task

**Date:** 2026-07-16
**Source:** Matt, in session 2026-07-16. Prompted by a gap check: the playbook routes the *driver* model per session type (§7) and pins *codified swarms* to the fast-execution tier (Brief 002), but nothing tells the model what tier — or what reasoning effort, or what execution pattern — an ordinary delegated task gets. Well-defined easy work was silently riding the most capable tier at full effort.
**Status:** Promoted directly by Matt; the ask below is the spec, approved as given. Filed and integrated the same session.
**Instruction to Claude Code:** Read this brief, `PLAYBOOK.md` §7, `plugin/templates/CLAUDE.template.md`, and `plugin/templates/model-routing.template.md` in full before integrating. This brief is the spec; do not re-litigate the reasoning, but flag any direct contradiction with existing content before writing.

---

## The ask (Matt, verbatim intent)

One routing doctrine, judgment-based not rule-bound: for every task, pick the cheapest pattern (inline → single agent → swarm/Workflow), model, and effort that gets full quality — escalate only when stakes or difficulty demand. Not "never fan out," not "always fan out" — fan-out reserved for what earns it (real-data gates, audits, batch builds). Small well-defined work gets Sonnet/Haiku at low effort; judgment, integration, spec work stays Fable; Opus for hard verify/judge. And every delegated agent gets model+effort set explicitly — no silent Fable inheritance.

Extends the existing swarm rule from "which model for swarm agents" to "which pattern+model+effort for any task."

## Context — the coverage gap

1. **Brief 002 covered codified swarms only.** Review finders, verify passes, the readiness gate → fast-execution tier, never the session model. Ad hoc delegation — a mechanical rename, a doc sweep, a well-scoped single-agent search — had no tier rule and silently inherited the session model.
2. **Brief 006 governed *whether* to spawn, not *what tier* a spawn gets.** The subagent budget asks "does this need a subagent at all?" and stops there.
3. **Reasoning effort was routed nowhere.** Model tier was the only cost lever any document named; effort per delegated agent was never set.
4. **The tier names had drifted.** The worked example treated "Opus (or Fable where available)" as one tier; with Fable a tier above Opus, "most capable" and "hard verify/judge" are now distinct assignments.

## Decisions

### 1. Adopt: one routing doctrine — pattern + model + effort, judgment-based

For every task, pick the **cheapest combination of execution pattern, model tier, and reasoning effort that gets full quality** — and escalate only when stakes or difficulty demand it. This is §7's existing rule ("match the model to how expensive a mistake is") applied to two axes it never covered: the pattern and the effort. Judgment-based, not rule-bound: the doctrine names the default direction (cheap) and the escalation trigger (mistake cost), not a lookup table for every case.

### 2. Adopt: the pattern ladder — inline → single agent → swarm/Workflow

Neither "never fan out" nor "always fan out." Inline is the default; a single delegated agent when the work is separable and its output is compact; swarms and orchestrated workflows only for what *earns* the fan-out — real-data review gates, audits, batch builds (the codified swarms of Briefs 002/003 remain deliberate by construction). This generalizes Brief 006's subagent budget from a yes/no question into an escalation ladder.

### 3. Adopt: tier assignments by task shape (logic INVARIANT, names PARAMETER)

- **Small, well-defined, easily-verified work** — mechanical edits, scoped searches, format conversions — routes to the **fast/cheap tiers at low effort**.
- **Judgment, integration, and spec work** — anything whose mistakes compound — stays on the **most capable tier** (the driver).
- **Hard verify/judge passes** — adversarial verification, judging between designs — get the **second tier**: cheaper than the driver, stronger than the execution tiers.

Scope correction this forces: the routing template's "cheapest tier: never" default described the **driver**; it stands for drivers, but delegated well-defined micro-tasks may now use the cheapest tier. That was the original intent ("revisit for genuinely high-volume, low-stakes work") — delegated micro-tasks are exactly that.

### 4. Adopt: effort is a routing axis

Reasoning effort is set per delegated agent alongside the model: **low** for mechanical, well-defined stages; higher tiers reserved for the hardest verify/judge work. Effort was previously unrouted everywhere.

### 5. Adopt: explicit assignment — no silent inheritance

**Every delegated agent gets model and effort set explicitly at spawn.** A spawn with no override silently inherits the session model — the most expensive tier — at default effort; that silent path is the failure mode this brief closes. Extends Brief 002's "never inherits the session model" from codified swarms to all delegation.

**Worked example — names as of 2026-07 (names age; the logic doesn't):** most capable / driver = Fable (Opus where Fable is unavailable); hard verify/judge = Opus; fast execution = Sonnet; cheapest = Haiku (now in play for delegated micro-tasks; still never the driver).

## Verification

- **Cross-reference:** every new "Brief 007" citation resolves to this file; this brief's file references (`PLAYBOOK.md` §7, `plugin/templates/CLAUDE.template.md`, `plugin/templates/model-routing.template.md`) all exist.
- **Behavioral (the rule bites where the model reads it — Brief 002):** grep confirms the pattern-ladder + explicit-assignment language appears in `plugin/templates/CLAUDE.template.md` **and this repo's own `CLAUDE.md`** (which previously carried no tier rule at all), not only in `PLAYBOOK.md` and the routing template.
- **Conventions:** INVARIANT/PARAMETER split intact — the doctrine and ladder INVARIANT, model names PARAMETER.
- **Scrub:** changed files pass the `scrub-terms.local.txt` grep with zero hits.

## Relationship to existing scope

Extends Brief 002 (swarm tier routing → all delegation) and Brief 006 (subagent budget → pattern ladder; tier + count → tier + count + effort). Re-scopes, but does not reverse, the routing template's cheapest-tier default. Touches no operator-facing ritual — routing is Code-side and invisible to the operator, per §4. Filed under the install-verification freeze via direct promotion by Matt, the same path as Briefs 002/006; docs-only, no build work.
