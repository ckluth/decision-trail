# Idea 0029: enumerate two missing "lookup, not judgment call" rules in the agent operating checklist

- Date: 2026-07-11
- Status: promoted
- Promoted to: [ADR-0035](../decisions/0035-enumerate-checklist-gaps-heading-and-reciprocal-links.md)

## Observation

While authoring ADR-0034 (`Status: proposed`), the decision section was headed
`## Decision` from the start, instead of `## Proposed decision` as ADR-0033
requires while a proposal is still open. The mistake only went unnoticed
because the ADR was accepted in the very next turn, which made the heading
retroactively correct by coincidence — had it stayed `proposed` for longer, it
would have sat non-conformant.

Root cause: drafting looked at an already-`accepted` sibling ADR (ADR-0011) to
confirm the overview's shape/format, and its `## Decision` heading was copied
as a stylistic default — a pattern-match off observed sibling reality instead
of a status-conditional lookup applied at the moment of writing. This is
exactly the failure mode ADR-0033 itself names ("author from the spec, never
from a sibling").

The heading-transition **rule text is not vague** — AGENTS.md § *The lifecycle*
states it plainly and unambiguously. What is missing is its presence in the
**enumerated checklist** in § *Agent operating guidance* ("Follow the spec's
mechanics... they are lookups, not judgment calls"), which already lists:
ordinal numbering, per-family status, canonical header + title line, and
disentangling a large idea. The `## Proposed decision` ↔ `## Decision`
transition is the same *kind* of pure, mechanical lookup, but it currently
lives only in prose in the narrative spec body — easy to skip when attention
is on authoring content rather than scanning for format compliance.

## The candidate

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

Both are pure agent-guidance additions — no change to either underlying rule
(ADR-0033 and ADR-0012 already settled them), just making them more likely to
be *applied* mechanically by living in the checklist an agent scans before
acting, not only in the narrative section.

## Why this deserves a thread

It is **generic** — any agent working this method authors ADRs and cross-links
regularly, so the same lapse can recur for any adopter, not just this repo.

It is narrow and low-risk: no new mechanic, no reopening of ADR-0033 or
ADR-0012's decisions — only a placement/discoverability fix in the
agent-guidance checklist, landing as its own small ADR.

## Open questions — resolved

- **Amend which ADR?** Resolved: a dedicated new ADR. Keeps ADR-0033 and
  ADR-0012 stable and gives this specific checklist-placement gap its own
  paper trail, rather than reopening either settled ADR for a placement tweak.
- **Scope of the fix.** Resolved: a single checklist bullet per rule is enough
  — the bullet itself is the operational trigger; no separate step-check
  workflow beyond that.
- **Any other checklist gaps?** Resolved via a quick audit of AGENTS.md's
  narrative spec against the enumerated checklist: one more matching gap found
  — the **reciprocal cross-link** rule (§ *Cross-link vocabulary*: "forward
  link always; add the reciprocal back-link for amend/supersede and
  promotion") — now folded into this idea's scope as the second bullet. No
  further gaps of the same shape were found; the other narrative rules
  (overview refresh, travel diary, intermediate artifacts, release-migration)
  already have their own dedicated checklist bullets.
