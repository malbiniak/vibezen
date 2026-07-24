---
description: End a session — pure capture, zero operator judgment (Brief 001)
---

# /wrap-up

The operator is at empty tank. Require nothing from them — no reading, no decisions, no triage. Execute the steps and confirm completion in one line.

1. **Docs checks:** verify cross-references in every doc changed this session resolve; run any privacy or scrub check the project's `CLAUDE.md` prescribes (if a required term list is missing, record that instead of skipping). Record outcomes in `STATUS.md`. Failures are captured, not raised — they lead the next `/resume` triage.
2. **Update `STATUS.md`** per its definition: last-updated stamp, plain-English state, what works, what's half-done, parked items, drafted next-session proposal, open questions (for the next `/resume`, never posed now).
3. **Append a dated `JOURNAL.md` entry** per its definition: intended vs. actual, friction named honestly, how-we-work decisions made during the session (capture only — never generate new decisions at wrap), mood read, your own failures. Append-only.
4. **Self-audit → `AUDIT.md`:** new dated entry at the top of the file. Ask yourself: what are you least confident about; what might be missing. Output contract (Brief 001):
   - Every item MUST name a specific file or behavior AND a concrete check that would settle it ("run X; if it prints Y, we're fine").
   - No falsifiable check → label the item **speculation** and route it to SCOPE.md Later. Speculation never enters the fix-now queue.
   - **"No material gaps" is a correct and expected output when the work is clean. Do not manufacture items.**
   - The operator does not read this now.
5. **Commit** everything with a plain-language message. Confirm to the operator in one line — nothing more.

If the project's `CLAUDE.md` says its working docs live somewhere other than the repo root, write them there.
