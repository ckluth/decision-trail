# ADR-0013: Rename the method from "the-way" to "decision-trail"

- Status: accepted
- Date: 2026-06-28
- Promoted from: [idea 0005](../ideas/0005-renaming-the-way.md)

## Context

The method's name, "the-way", reads as grand and pretentious. It fails the test
that matters most for adoption: handing it to a colleague — *"look what I made,
try it"* — should feel inviting, not self-important (idea 0005). A name is the
first thing an adopter meets; a humble, self-descriptive one lowers the barrier
to trying the method (Borrow-don't-invent #8, Genericity #7).

Candidates weighed: `trail`, `throughline`, `cairn`, `stepwise`, `ledger`,
`paper-trail`, and `decision-trail`.

### Decision drivers

- **Low ego / shareable:** the name should explain itself and not posture.
- **Descriptive of the method:** the method carries a thought through its life
  (idea → proposal → decision → plan → execution) in plain markdown.
- **Greppable and collision-light** as a repo/method name.
- **Echoes the method's own language:** cross-links are meant to be *walkable
  from either end* — a "trail" you can follow.

### Trade-off considered

`decision-trail` foregrounds the **decision** (ADR) stage and slightly undersells
the idea and plan/execution ends — a reader might mistake it for a pure ADR log.
This was accepted because decisions are the *spine* of the lifecycle: ideas
mature into them and plans implement them, so naming after the spine is honest,
and "trail" reintroduces the full journey from idea to execution.

## Decision

The method is renamed from **the-way** to **decision-trail**.

- The provenance citation string becomes `Based on decision-trail vX.Y`.
- All self-referential prose ("the-way", "work the-way") is reworded to use the
  new name or a neutral phrasing ("work decision-trail" / "the method").

## Consequences

- A rename touches many surfaces — these are **execution work for a follow-up
  plan** that `Implements:` this ADR, not done by this decision:
  - the repository name (`ckluth/the-way`);
  - the citation string `Based on the-way vX.Y` in `starter/` and docs;
  - `AGENTS.md`, `.github/copilot-instructions.md`, `README`/method text,
    `starter/` skeleton, and `CHANGELOG.md`;
  - the next semver tag, which records the rename as a released change.
- Already-adopted repos cite a version; their existing `Based on the-way vX.Y`
  citation stays valid as historical provenance, and they move to
  `decision-trail` when they take the version that ships this rename. The
  upgrade-path concern is tracked separately by idea 0004.
- This is a use-phase change to the method, made decision-trail (the method
  applied to itself): captured as idea 0005, promoted here, to be carried out by
  a plan.
