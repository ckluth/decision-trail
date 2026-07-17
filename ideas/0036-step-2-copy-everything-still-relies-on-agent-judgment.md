# Idea 0036: Step 2's "copy everything under starter/" still leans on agent judgment

- Date: 2026-07-17
- Status: promoted
- Promoted to: [ADR-0042](../decisions/0042-reframe-update-step-2-as-enumerate-and-copy.md)

## The itch

v2.18.1 (ADR-0041, plan 0030) fixed the *immediate* miss: `updating.agent.md`
step 2's example list was reframed as *explicitly non-exhaustive* — "copy
**everything** under `starter/`, including but not limited to …" — so a list can no
longer be read as a closed set and drop a shipped scaffold like
`docs/scripts/regen-overview.ps1`.

That closed the specific hole, but the *shape* of the fix left the residual
weakness untouched: step 2 is still a **prose instruction the agent interprets**.
"Copy everything, but not the project-authored content, and here are some examples,
and here's a preserve rule…" — the agent still has to read a paragraph and decide
*which files* to copy. The v2.18 miss happened precisely because an agent narrowed a
copy that prose told it to widen. Non-exhaustive wording makes that narrowing
*wrong*, but it does not make it *impossible* — the next agent under the next new
subtree can still under-copy.

## The cheaper framing

The root operation step 2 wants is mechanically trivial: **mirror the `starter/`
directory tree into the adopter's `docs/`**, wholesale, then *subtract* the
preserve-list (project-authored artifact families, populated companions,
`overview.md`). That is a whole-tree copy with a small exclusion set — not a
per-file judgment call.

Framed that way, "which files ship" stops being a question the agent answers from an
example list at all: it copies the tree, full stop. The only thing it reasons about
is the short, closed *preserve* set (what **not** to overwrite) — which is already
enumerated and stable. The fragile open-ended "did I get everything?" side becomes
mechanical; the bounded "what do I protect?" side stays a small explicit list.

## Directions to weigh (for the proposal, not this seed)

- Reframe step 2 as an explicit **mirror-then-preserve** operation: copy the whole
  `starter/` subtree, then exclude the (already-listed) project-authored paths —
  rather than an enumerate-what-to-copy paragraph.
- Whether this is a pure re-wording of step 2 (execution-detail refinement of
  ADR-0022, in the same spirit as ADR-0041) or warrants its own small ADR.
- Keep it **cheap**: no post-copy tree-parity check and no new conformance-check
  item — both were weighed and dropped by ADR-0041 as over-engineering for a
  wording bug, and that judgment still holds. This idea is about removing the room
  for interpretation at the *source*, not adding safety nets after the fact.

## Boundaries this must respect

- **Copy-driven contract (ADR-0022).** `starter/`'s contents stay the single source
  of truth; no manifest is introduced. A whole-tree mirror *reinforces* "copy
  everything under `starter/`" — it is the most literal reading of it.
- **Human-intent / agent-execution split (ADR-0031).** Agent-facing procedure only;
  the human trigger and `adopting.md` are untouched. No new human step.

## Not yet decided

Whether to act at all (v2.18.1 may be judged good enough) versus tightening step 2
into a mirror-then-preserve operation; whether it rides as a patch **2.18.2** and
what its migration note says (likely "none" — a pure wording refinement that changes
no adopter-visible behavior). That belongs to the proposal, not this seed. The
omission that started this thread surfaced from a real adopter update.
