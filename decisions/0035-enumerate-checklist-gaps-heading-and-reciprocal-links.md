# ADR-0035: Enumerate two missing "lookup, not judgment call" rules in the agent operating checklist

- Status: accepted
- Date: 2026-07-11
- Promoted from: [idea 0029](../ideas/0029-enumerate-heading-transition-in-agent-checklist.md)

## Context

While authoring ADR-0034 (`Status: proposed`), the decision section was headed
`## Decision` from the start instead of `## Proposed decision`, as ADR-0033
requires while a proposal is still open. The mistake only went unnoticed
because the ADR was accepted in the very next turn, which made the heading
retroactively correct by coincidence — had it stayed `proposed` for longer, it
would have sat non-conformant. Root cause: drafting looked at an
already-`accepted` sibling ADR to confirm shape/format, and its `## Decision`
heading was copied as a stylistic default — a pattern-match off observed
sibling reality instead of a status-conditional lookup applied at the moment
of writing. This is exactly the failure mode ADR-0033 itself names ("author
from the spec, never from a sibling").

The heading-transition **rule text is not vague** — AGENTS.md § *The
lifecycle* states it plainly and unambiguously. What is missing is its
presence in the **enumerated checklist** in § *Agent operating guidance*
("Follow the spec's mechanics... they are lookups, not judgment calls"), which
already lists: ordinal numbering, per-family status, canonical header + title
line, and disentangling a large idea. The `## Proposed decision` ↔
`## Decision` transition is the same *kind* of pure, mechanical lookup, but it
currently lives only in prose in the narrative spec body — easy to skip when
attention is on authoring content rather than scanning for format compliance.

A follow-up audit of AGENTS.md's narrative spec against the enumerated
checklist found one more matching gap of the same shape: the **reciprocal
cross-link** rule (§ *Cross-link vocabulary*: "forward link always; add the
reciprocal back-link for amend/supersede and promotion"). No further gaps of
this shape were found — the other narrative rules (overview refresh, travel
diary, intermediate artifacts, release-migration) already have their own
dedicated checklist bullets.

### Decision drivers

- **Economy (#2) / reliability of the checklist mechanism:** the enumerated
  checklist exists specifically to make pure lookups mechanical rather than
  memory-dependent. A rule stated only in narrative prose is easy to skip when
  attention is on content, not format compliance — the checklist is the
  intended catch, so gaps in its coverage undermine its purpose.
- **Avoid reopening settled ADRs:** ADR-0033 and ADR-0012 already settled the
  underlying rules; this is purely a discoverability/placement fix in the
  agent-guidance checklist, not a reconsideration of either decision.

## Decision

Add **two** bullets to the enumerated "Follow the spec's mechanics exactly"
checklist (§ *Agent operating guidance*, both `starter/AGENTS.md` and this
repo's `AGENTS.md`), alongside the existing four (ordinal numbering,
per-family status, canonical header + title line, disentangling a large idea):

1. **Decision heading transition** — *"Decision heading tracks status —
   `## Proposed decision` while `proposed`, renamed to `## Decision` on
   acceptance; check and fix this whenever authoring or accepting an ADR
   (§ *The lifecycle*; ADR-0033)."*
2. **Reciprocal cross-links** — *"Forward link always; add the reciprocal
   back-link when amending/superseding an ADR or promoting an idea — never
   ship only the forward half (§ *Cross-link vocabulary*; ADR-0012)."*

Both are pure agent-guidance additions — no change to either underlying rule.
This lands as its own dedicated ADR, touching neither ADR-0033 nor ADR-0012.

## Consequences

- The enumerated checklist becomes a more complete catch-net for "lookup, not
  judgment call" rules, reducing the chance an agent skips a mechanical rule
  because it lives only in narrative prose.
- No underlying rule changes: ADR-0033's heading-transition rule and
  ADR-0012's reciprocal-link rule stand exactly as decided.
- A small plan is needed to carry this out: add both bullets to
  `starter/AGENTS.md`, mirror into this repo's `AGENTS.md`, and regenerate
  `overview.md`.
