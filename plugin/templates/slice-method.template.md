# The Slice Method (template)

> **Template.** The method is INVARIANT; the slice list itself is per-project (PARAMETER) and lives in the project's build playbook and SCOPE.md.

1. **Slice 1 proves the core rule on hand-entered data.** The first slice is the product's heart: the one behavioral rule that makes it worth building, running on real data entered by hand. Tune the rule with real data before building anything on top of it.
2. **A later slice earns its place by feeding or consuming an earlier one.** A workflow slice's only job may be to produce the records an earlier slice already consumes. That's a feature, not a smell — the consumer is already proven by the time the producer is built.
3. **Design each slice for its concrete moment of use.** Name the real situation the slice must not fail in, and optimize for exactly that — nothing more.
4. **Start the least-proven slices as the simplest possible version** — a sorted list, not a system. Resist building more until the simple version proves insufficient.
5. **Breaking circular dependencies (general rule):** when feature A needs feature B and vice versa, ask what *data* one needs from the other, and enter that data by hand first. Manual entry is scaffolding; the workflow that automates it comes later. "Manual" means *no automation yet* — it never means CLI or spreadsheets. Data still goes in through the product's own screens or through conversation with Claude.
6. **One slice item per session.** New ideas go to Later in SCOPE.md; the backlog absorbs scope creep.

> **Provenance:** this method is proven on one project. Its shape assumes the product has a single named core rule. If a future project has no such rule, don't force the fit — that's playbook-intake material: file a decision brief and amend the method.

This project's slices:

1. **Slice 1 — `<the core rule on hand-entered data>`**
2. **Slice 2 — `<name>`**
3. `<…>`
