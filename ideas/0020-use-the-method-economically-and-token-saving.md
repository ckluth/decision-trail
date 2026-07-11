# Idea 0020: advice and means to run the method economically and token-saving

- Date: 2026-07-10
- Status: decomposed

## What this idea became (a decomposed map)

This idea asked a single question — *how do we operate the method economically,
given that today's operators are AI agents paying in tokens and context budget?*
On inspection that question braided **three orthogonal axes** that only had weight
together as a map. Per the method's disentangling procedure (ADR-0027), the idea is
**decomposed**: its own content moved out into three budded children, and this file
now stands as a pure map. It holds no idea-content of its own — only the reasons for
the split and the pointers below. (`decomposed` is hand-curated and reversible: flip
back to `seed` to bud one more child.)

The children's fate is told by *their* statuses, not this one.

## The three axes (and why they split)

The single "economy" question separated cleanly by **when the cost is paid** and
**whether fixing it changes mechanism**:

1. **Resume-time economy — advisory.** The cost an agent pays *only when it reads
   the trail*, and can already avoid via the existing greppable headers, derived
   `overview.md`, and travel diary. Naming these as a stated discipline is largely
   advice, no mechanism change.
   → [0023 — name the resume-time economy practices as a discipline](0023-name-the-resume-time-economy-practices-as-a-discipline.md)

2. **Always-loaded weight — a refactor.** The cost paid *every session,
   unconditionally*, because `AGENTS.md` is injected as custom instructions before
   any task; it restates its rules ~3×. Compacting it is a concrete refactor of
   existing prose.
   → [0021 — shrink the always-loaded agent instruction weight](0021-shrink-the-always-loaded-agent-instruction-weight.md)

3. **Fixed procedures as skills — a new mechanism.** The method's deterministic
   procedures (overview refresh, artifact creation, insert-and-shift, disentangling,
   adopter update) sit in always-loaded prose but only matter *when invoked*. Moving
   them into optional, on-demand skills adds an (optional, tool-specific) mechanism.
   → [0022 — render fixed procedures as optional skills](0022-render-fixed-procedures-as-optional-skills.md)

Axes 2 and 3 are close cousins (skills *enable* deeper compaction) but are separable
— one tightens existing prose, the other adds a mechanism — so each gets its own
thread and, at promotion, likely its own ADR. Axis 1 is advisory and stands apart.

Each child carries the authoritative `Parent:` link back here (ADR-0012's
forward-only rule); this map is the human-facing companion to those links.
