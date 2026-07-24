# DATA-MODEL.md (template)

> **Job:** schema + plain-language translation. Changes rarely, alongside SPEC changes; Code triggers and announces every change.
>
> **PARAMETER file:** only for projects with persistent data. A docs-only project skips it — record the justification in JOURNAL.md.
>
> **Conventions (INVARIANT):** two halves with a hard boundary. Part 1 is plain language and is always the authoritative statement of intent; Part 2 is the schema, and the operator never needs to read past that line. Schema comments carry dated change annotations — "(YYYY-MM-DD: `<what changed>`)".

---

# `<Project>` Data Model

Two halves. The first is the plain-language version — the operator reads this one, and it is always the authoritative statement of intent. The second is the schema — Claude's territory; the operator never needs to open it.

## Part 1 — Plain language (the operator reads this half)

### The pieces and how they connect

**A `<entity>`** is `<what it is, in domain words>`. `<For central entities, enumerate their parts as a numbered plain-language list, mirroring SPEC.md's core-rule framing.>`

**A `<entity>`** is `<…>`. `<Records that exist for history or future learning should say so plainly — what is kept, why it's kept forever.>`

`<One bold paragraph per entity, in dependency order. Note anywhere the model is deliberately stretchy — open-ended attributes, kinds sharing one shape — so extensions never require a rebuild.>`

### How the core rule reads this

> `<Restate SPEC.md's core rule as a single walk through the data: what event starts it, which records it reads, what it writes, what happens on reversal. This blockquote is the contract between the spec and the schema.>`

### The design promises

1. **`<Promise>`** — `<a plain-language guarantee about the model that the operator can hold the schema to, checkable by behavior — e.g. extensibility, first-class history, readiness for future consumers, one source of truth for every client>`.
2. **`<Promise>`** — `<…>`

---

## Part 2 — Schema (Claude's half; the operator never needs to read past this line)

`<Conceptual schema. If no storage engine is chosen yet, say so — naming below is the contract regardless of engine.>`

### Enums

```
<enum_name>   = <value> | <value> | <value>   -- <note; date-stamp changes: (YYYY-MM-DD: <what changed>)>
```

### Entities

```
<entity>
  id, <fields>
  <field>: <type>            -- <constraint or meaning, in a comment>
  attributes: json           -- <if the extensibility promise applies>
```

### Derivation notes

`<How the core rule computes, precisely: matching semantics (ANY vs ALL), thresholds, ordering rules, tie-breakers. This is where behavioral edge cases from SPEC.md become exact.>`

### Invariants

- `<Append-only rules: which records are never deleted or rewritten, and why (history as a learning/training surface).>`
- `<Cascade rules: what must die or revert when its source record changes.>`
- `<Locale rules: which timezone/locale all date logic uses.>`
