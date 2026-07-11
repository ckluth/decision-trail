# Idea 0030: revisit optional skills if adopters demand structured operation

- Date: 2026-07-11
- Status: seed

## What this is

A deliberately-kept **revisit reminder**, not a fresh line of thought. It springs
from a *decision*, not from budding an idea, so it carries no `Parent:` — the prose
pointer below is enough.

[ADR-0036](../decisions/0036-render-fixed-procedures-as-optional-skills.md) rejected
rendering the method's fixed procedures as optional skills. The rejection was sound
on today's evidence: the cost saving is marginal (~1% of session cost, mostly
neutralized by prompt caching), and the one solid benefit — execution reliability —
is better served by sharpening/compacting the canonical prose (idea 0021 + the
ADR-0026 discipline) than by forking it into a tool-specific second artifact that
owes perpetual sync (ADR-0014).

## The reopen condition

One driver was left explicitly open: **structured, guided operation for users
uncomfortable with the conversational method.** That benefit is real but was
*speculative* at rejection time — no concrete adopter had demanded it. This seed
exists to catch the moment it stops being speculative.

**Revisit when:** a concrete adopter (or real, repeated user friction) demands a
more structured / guided way to operate the method — at which point the deciding
driver becomes UX / adoption, *not* cost.

## What maturing this looks like

When the condition fires, this seed matures and **promotes to a new ADR that
supersedes ADR-0036** (`Supersedes:` / `Superseded by:`, ADR-0012), re-weighing
Option B (adopt skills on the reliability/UX axis) with the fresh adopter evidence
in hand. Until then it rests as `seed`, surfacing in the idea table of
`overview.md` as a live "come back to this" marker.
