# Plan 0025: enumerate the heading-transition and reciprocal-cross-link rules in the agent checklist

- Date: 2026-07-11
- Status: done
- Implements: [ADR-0035](../decisions/0035-enumerate-checklist-gaps-heading-and-reciprocal-links.md)

## Goal

Land what ADR-0035 accepted: add two bullets to the enumerated "Follow the
spec's mechanics exactly" checklist in § *Agent operating guidance* —
(1) the decision heading transition (`## Proposed decision` → `## Decision`),
and (2) the reciprocal cross-link rule (forward link always; add the
reciprocal back-link on amend/supersede/promotion). No underlying rule
changes; ADR-0033 and ADR-0012 stand as decided.

## Sync rules (critical — read before editing)

§ *Agent operating guidance* is **not** part of the derived method body (which
runs `## The contract` → `## How to start working`, ADR-0032). It is a
**hand-authored, audience-forked** section: `starter/AGENTS.md` is the
adopter-facing rendering and this repo's `AGENTS.md` is the method-home
rendering. The two must stay in lock-step in *content*, but each keeps its
declared audience delta (ADR-0014, ADR-0032):

- **`starter/AGENTS.md`** — bullets reference the spec by section only, pointing
  at `docs/working-method.md`; **no construction-ADR citations**.
- **this repo's `AGENTS.md`** — same bullets, but each cites the governing
  construction ADR (e.g. `ADR-0033`, `ADR-0012`), matching the existing four
  bullets' style.

Edit both files; do **not** regenerate one from the other (this section is not
derived). The `working-method.md` spec is **not** touched — the two rules
already live in its narrative body (§ *The lifecycle*, § *Cross-link
vocabulary*); this plan only surfaces them in the agent checklist.

## Tasks

### `starter/AGENTS.md` (adopter-facing rendering)

- [x] After the **Disentangling a large idea** bullet in the "Follow the spec's
      mechanics" sub-list, add a **Decision heading transition** bullet:
      `## Proposed decision` while `proposed`, renamed to `## Decision` on
      acceptance; check/fix when authoring or accepting an ADR (§ *The
      lifecycle*). No ADR citation (adopter delta).
- [x] Add a **Reciprocal cross-links** bullet: forward link always; add the
      reciprocal back-link when amending/superseding an ADR or promoting an
      idea — never ship only the forward half (§ *Cross-link vocabulary*). No
      ADR citation (adopter delta).

### this repo's `AGENTS.md` (method-home rendering)

- [x] Add the same two bullets in the same position, **with** construction-ADR
      citations: heading-transition → `(§ *The lifecycle*; ADR-0033)`;
      reciprocal cross-links → `(§ *Cross-link vocabulary*; ADR-0012)`,
      matching the style of the existing four bullets.

### Reconcile the index

- [x] Regenerate `overview.md` wholesale from the artifact headers (picks up
      idea 0029 `promoted`, ADR-0035 `accepted`, this plan, and the new
      ADR-0035 → Plan 0025 sub-index row). Re-stamp "as of <date>".

## Verification

- [x] `grep` confirms both new bullets appear in `starter/AGENTS.md` **without**
      ADR citations and in this repo's `AGENTS.md` **with** the ADR-0033 /
      ADR-0012 citations — the audience delta is preserved, not flattened.
- [x] Confirm `starter/docs/working-method.md` and this repo's `AGENTS.md`
      **derived method body** (§ *The contract* … § *How to start working*) were
      **not** touched — this change is confined to the hand-authored guidance
      section.
- [x] `overview.md` rows for idea 0029, ADR-0035, and plan 0025 match their
      headers, and the ADR-0035 → Plan 0025 sub-index row is present.

## Notes

- Scope is the agent-guidance **checklist text** only. Cutting a decision-trail
  **release** (version bump, `CHANGELOG.md` entry with an `Adopter migration:`
  line, per ADR-0021/ADR-0022) is separate downstream work, not part of this
  plan. The migration is "none" anyway — these bullets restate existing rules,
  no adopter behavior change.
- No back-migration of artifacts: ADR-0033 and ADR-0012 are unchanged; this is
  purely a checklist-placement fix.
