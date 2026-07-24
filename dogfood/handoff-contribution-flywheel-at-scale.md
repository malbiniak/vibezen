# Handoff to Chat — the contribution-flywheel pattern at org scale

**Filed 2026-07-15 (Session 6). This is a thinking handoff, not a decision brief.** Per PLAYBOOK.md §12, thinking happens in the Chat thinking project and lands back here as a brief. This packet boxes up an observation for pressure-testing. What should come back is a brief — or a clean "this isn't the playbook's problem, and here's what it actually is."

**Explicitly not being asked (Matt, 2026-07-15):** whether this plugin should solve it. He is undecided, leaning no. This is a pattern observation seeking a shape, not a feature request. No implementation wanted.

---

## The observation

This playbook plugin was produced by a live project's real needs. The flow that actually happens:

> live project hits a real need → Matt notices → Matt carries the idea here by hand, in a chat message → we sort it out → the plugin improves → **the live project never gets the improvement back**

So the project that generated the insight keeps using its own divergent version. The tools drift from what's maintained here. Every good idea makes the gap wider, because the idea gets refined *here* and shipped *nowhere*.

Two structural facts found while writing this up:

- **PLAYBOOK.md §6 already names the intake route.** `/resume` triage routes three ways: fix now, backlog, and **playbook intake** — "process learnings → routed out of the project repo, to this repo." The route is named. It has no vehicle. Matt *is* the vehicle.
- **The return trip does not exist at all** — not as a mechanism, not as a concept, not as a line in any document.

Matt's observation, which is what this packet is really about: **this pattern is everywhere at Walmart.** Everyone builds things and creates tools useful to them, with no good way for those to traverse the org. The existing answer is a marketplace. It fails for a specific, diagnosable reason — **people feel they need a polished thing to submit.** That bar filters out precisely the rough ideas, concepts, and half-working tools that carry the most real signal.

## Four seeds worth pressure-testing

**1. The two-tier structure may already be the shape.** This playbook has exactly the thing a not-a-marketplace wants: **Later accepts rough** (the lowest possible bar — every idea lands there first, attributed and dated, with no quality gate whatsoever), and **briefs are the gate** (rigor, one approver, no fast path, and every resulting rule cites its brief). Rough in, gatekeeping downstream, provenance preserved. The question is whether that survives contact with N contributors instead of one.

**2. The hard problem is not distribution. The useful artifact and the sensitive context are the same document.** Discovered by failure this session, which is the strongest evidence in this packet: Code was handed a genuinely excellent design document from one of Matt's live projects — hard-won, real-need thinking, exactly what a flywheel exists to move upstream. It was ~30 mentions deep in that project's private internals: its name, its file names, a person's name, physical details of a home, entity IDs. Code transcribed one of those names into this public repo and did not re-run the privacy scrub. Nothing was committed and nothing leaked, but the only thing between that and a public commit was a session-end ritual.

  The generalization is uncomfortable and load-bearing: **lower the submission bar and you raise the volume of internals riding along, because polish is where people scrub.** An org-scale flywheel's gate cannot only judge quality — it must scrub content, at volume, on rough input, from contributors who are being actively encouraged not to tidy first. And it must do that reliably enough that one leak doesn't kill the whole program's credibility.

**3. Provenance and privacy pull against each other.** This playbook's core rule is that every rule cites the brief it came from — ideas keep a paper trail back to their reasoning. But the reasoning lives inside the private project. Scrubbing the context can strip exactly what makes an idea legible: in this session, the design document's sharpest insight was only *understandable* with the originating project's failure modes attached. A scrubbed contribution may arrive as an assertion with its evidence amputated — which is the form least likely to survive a gate.

**4. Bidirectionality is the unsolved half.** Intake is a route with no vehicle; the return trip isn't even a route. A flywheel that only spins one way is a tax on the contributor: they do the noticing, they do the writing, they do the scrubbing, and their own project gets nothing. That is a straightforward explanation for why voluntary contribution programs die, and it does not require anyone to be lazy or territorial.

## Questions worth the firepower

- Is the marketplace-polish problem a **bar** problem or an **identity** problem? People may not submit rough things because submitting means publicly authoring something that will be judged — in which case lowering the stated bar changes nothing, and the fix is about attribution and framing rather than criteria.
- Does **rough inbox / rigorous gate** survive N contributors and one gatekeeper? Where does the gatekeeper become the bottleneck, and what is the failure mode when they do — backlog rot, or silent quality collapse as they start rubber-stamping?
- Can scrub be **automated** enough to be safe at volume? If it needs a human pass, does that reintroduce the polish tax under a different name?
- Is the return trip a **push** (updates flow to every install) or a **pull** (projects re-adopt on a cadence)? What makes a non-developer actually take an update to their tooling, given they didn't ask for it and it might break what works?
- Is the unit of contribution an **idea** or an **artifact**? This playbook's answer is emphatic — ideas travel as short instructions, never as imported artifacts (Principle 1, §2), because importing artifacts is "the drift machine." Does that survive at org scale, or does it collapse back into the marketplace it was trying not to be?
- Is the honest answer that this is **two problems** — a playbook-sized one (how do this repo and its own projects stop drifting) and an org-sized one (how does anything traverse Walmart) — that only look like one because the same person noticed both?

## What is already in this repo, for context

- The playbook-sized version of this is filed in `dogfood/SCOPE.md` Later as **"The contribution flywheel."** It is frozen behind install verification like everything else.
- The first real test case is chosen: a live project builds a backlog board from its own need, and this repo harvests it upstream (Matt's call, 2026-07-15). That harvest is the flywheel's first end-to-end run, with a known-good artifact rather than a hypothesis.
- The privacy rule that caught the failure above is in `dogfood/SPEC.md`, enforced by a gitignored scrub-term list and a grep before every commit.
