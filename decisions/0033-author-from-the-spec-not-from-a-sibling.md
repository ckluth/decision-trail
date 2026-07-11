# ADR-0033: author new artifacts from the spec, not from a sibling as a template

- Date: 2026-07-11
- Status: accepted
- Promoted from: [idea 0027](../ideas/0027-author-artifacts-from-spec-not-from-a-sibling-template.md)

## Context

When drafting a new artifact, an agent's reflex is to open a recent same-family
artifact "to see the shape" and fill in the blanks. The human caught this while a
proposed ADR was being prepared (promoting [idea 0026](../ideas/0026-guide-sync-model-cant-hold-audience-deltas.md)).

The reflex is dangerous even though the format is *already fully pinned*: the
header block (ADR-0026), the typed zero-padded title line (ADR-0028), per-family
status (ADR-0024), and the classic Status / Context / Decision / Consequences body
with Decision Drivers / Considered Options when weighing alternatives
(ADR-0001, ADR-0003, ADR-0014). Copying a sibling imports its **incidental
reality** — a wrong status (`accepted` instead of `proposed`), its particular
`Amends:` / `Promoted from:` cross-links, its specific section choices. That is a
fresh source of exactly the drift the method works to prevent, and the agent
operating guidance currently says nothing against it.

The same investigation exposed a **latent spec gap**: the spec pins the header and
the template *sections* but not the *wording* a proposal uses for its decision
heading. Existing proposals wrote `## Proposed decision` while `Status: proposed`,
reading as `## Decision` once accepted — an observed habit, not a written rule. An
agent authoring strictly from the spec has no instruction telling it `## Proposed
decision` vs `## Decision`, which is precisely the kind of hole that sends an agent
reaching for a sibling in the first place.

## Decision Drivers

- **Transparency (#3) and drift-prevention.** Copying a sibling silently absorbs
  incidental content; the method exists to keep artifacts clean and consistent.
- **The mechanics are lookups, not judgment calls.** The guidance already frames
  format as fully specified; the missing piece is the *sourcing* question — where
  the shape of a new artifact comes from.
- **Genericity (#7).** Every adopter's agent shares the reflex, so any rule belongs
  in the guidance that ships via `starter/AGENTS.md`, not only this repo's copy.
- **A rule is only as good as the spec behind it.** "Author from the spec" fails if
  the spec has holes; closing the `## Proposed decision` gap makes the spec actually
  sufficient, so the two changes reinforce each other.
- **Honesty about genuinely novel sections.** An absolute ban over-reaches; there
  must be room to consult prior art *to verify format-conformance* without opening
  the fill-in-the-blanks door.

## Considered Options

1. **Agent-guidance rule only** — forbid sibling-as-template. Rejected alone: leaves
   the `## Proposed decision` spec gap that drives the reflex.
2. **Spec sharpening only** — pin the heading convention. Rejected alone: closes one
   hole but does not name the sourcing anti-pattern generally.
3. **Both, with a bounded exception (chosen).** A guidance rule plus the spec
   sharpening, the rule carrying a narrow escape hatch for format-conformance
   checks.
4. **Single `## Decision` heading throughout**, status alone marking
   proposal-vs-decision. Rejected: discards the informative, already-established
   `## Proposed decision` signal and the visible accept-time transition.

## Decision

Adopt **both** changes.

1. **Agent-guidance rule — "author from the spec, never from a sibling."** Add to
   the agent operating guidance (shipped to adopters via `starter/AGENTS.md`,
   mirrored in this repo's `AGENTS.md`):

   > **Author from the spec, never from a sibling.** A new artifact's header, title
   > line, status, and body template are fully specified (§ *The lifecycle*). Do not
   > open an existing artifact as a *template* — copying imports incidental reality
   > (a wrong status, the wrong cross-links). Reading a sibling **to check that the
   > format is being followed** is fine; using one as a **fill-in-the-blanks
   > scaffold is not.** If you feel you need an example to know the shape, that is a
   > signal the *spec* is unclear — sharpen the spec, don't copy.

2. **Spec sharpening — pin the proposal decision-heading convention.** In the
   canonical spec (`starter/docs/working-method.md`, whence this repo's `AGENTS.md`
   method body is regenerated), pin: a proposal uses **`## Proposed decision`** while
   `Status: proposed`; on acceptance the ADR's status flips to `accepted` **and the
   heading is renamed to `## Decision`** — status and heading move together.

The **bounded exception** is the rule's own second sentence: consulting prior art to
confirm format-conformance is allowed; using it as a fill-in scaffold is not — and
the itch for an example is a signal to sharpen the spec, not a licence to copy.

## Consequences

- The sourcing question is closed: agents author from the specification, and the
  reflex to scaffold from a sibling is named and forbidden generically for every
  adopter.
- The `## Proposed decision` → `## Decision` transition becomes a written rule, so an
  agent authoring purely from the spec knows which heading to use and when to rename.
- A plan implementing this ADR touches `starter/docs/working-method.md`,
  `starter/AGENTS.md`, and this repo's `AGENTS.md`, then regenerates any derived
  renderings and `overview.md`.
- The heading rename adds one small step to the accept-a-proposal flow; the visible
  proposal-vs-decision signal is preserved rather than collapsed into status alone.
- Existing accepted ADRs already carry `## Decision`; existing proposals already use
  `## Proposed decision`, so no back-migration is required.
