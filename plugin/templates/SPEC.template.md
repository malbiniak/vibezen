# SPEC.md (template)

> **Job:** the behavioral constitution. What the product does, in plain language the operator can read. Changes rarely and deliberately — only the operator triggers a change, and Code announces "this changes the spec" before making one.
>
> **Conventions (INVARIANT):** behavior only, never implementation. One single *named* core rule. Explicit non-goals. Inline date-stamped amendments — "(Added YYYY-MM-DD.)" — so the spec records when a clause entered. Requirements that look like niceties (tone, vocabulary, feel) get their own section flagged **"this is a product requirement"** so they can't be dismissed as polish.

---

# `<Project Name>` — What It Does

`<One paragraph: what this is, who it's for, and — in the same breath — what it is deliberately NOT about.>`

## `<The experience rule>` (this is a product requirement)

`<If the product has a tone, vocabulary, or feel requirement, state it here as enforceable behavior — including any words that must or must never appear.>`

## The people

| Person | Who they are | What they can take on |
|---|---|---|
| **`<Persona>`** | `<role / relationship to the product>` | `<capabilities, in plain words>` |
| **`<Persona>`** | `<…>` | `<…>` |

`<Name the dimensions capabilities vary on, what the fixed starting set is, and what's deferred to Later (e.g. a configurable version).>`

## User stories, per persona

**`<Persona>`** (`<role>`)
- I want `<…>`, so that `<…>`.
- I want `<…>`.

`<One block per persona — every persona in the table gets stories, including optional or future users. End with an "Anyone" block if some behaviors are open to all.>`

**Anyone**
- `<…>`

## The core rule: `<name it in one clause>`

`<The product's central behavioral rule — the thing that makes it worth building. Enumerate the parts as a numbered list ("every <record> carries N things"), then state each behavioral consequence with a bold lead-in ("**It does X.** …"). Write it so a violated behavior reads as a broken promise, not a bug report. Edge cases and reversals ("if <input> changes, everything derived from it re-decides") belong here, not in code comments.>`

## `<Supporting behavior sections>`

`<One section per named workflow or lifecycle. State machines as numbered states in prose, in order, with the restart/edge rules bolded. Reminders and nudges in behavior language ("the product reminds; it never assumes").>`

## Non-goals (deliberately out of scope, permanently unless the spec changes)

- **`<Non-goal>`** — `<make the boundary precise: name the near-miss that IS in scope, so the line is testable>`.
- **`<Non-goal>`** — `<…>`
