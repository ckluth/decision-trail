# Plan 0027: Carry ADR-0038 into the method — stub-plan-at-acceptance discipline and the "accepted, no plan" backstop

- Date: 2026-07-15
- Status: done
- Implements: [ADR-0038](../decisions/0038-stub-plan-at-acceptance-and-derived-no-plan-backstop.md)

Mechanical execution of ADR-0038. Two additions to the method, both reusing
existing vocabulary: (1) the stub-`draft`-plan-at-acceptance discipline stated in
the method text and agent guidance, and (2) a third derived "Accepted — no plan
yet" section added to the `overview.md` template and the refresh procedure. The
canonical spec is `starter/docs/working-method.md`; `AGENTS.md` (this repo) and
`starter/AGENTS.md` are derived renderings that must be kept in sync. The
reciprocal `Amended by:` back-links on ADR-0011 and ADR-0034 were already added at
acceptance time.

## Tasks

### Canonical spec — `starter/docs/working-method.md`

- [x] In the decision-stage / lifecycle text, state the **stub-plan-at-acceptance
  discipline**: accepting an ADR that needs execution creates its plan then and
  there — at least a one-line `draft` stub that `Implements:` it — so that the
  *absence* of a plan comes to mean "this ADR stands for itself." Reuse the
  existing `draft` status; introduce no new status, verb, or field.
- [x] In the `overview.md` section, add the **third derived view**: an
  "Accepted — no plan yet" section listing every accepted ADR that no plan points
  at via `Implements:`, regenerated wholesale in the same pass as the ADR → plans
  sub-index and carrying the same "as of" stamp.
- [x] State the view's role and the **residual ambiguity** honestly: the section
  is a review-queue *backstop*, not a classifier — it cannot by itself distinguish
  "intentionally self-standing" from "genuine gap"; the discipline draws that line
  at acceptance, and the human periodically clears the queue.
- [x] Extend the **refresh procedure** text to describe producing the
  "Accepted — no plan yet" section from the same header scan (accepted ADRs minus
  those with an `Implements:` back-pointer).

### Derived renderings — `AGENTS.md` and `starter/AGENTS.md`

- [x] Regenerate the derived method body (contract … how-to-start) in this repo's
  `AGENTS.md` from the updated canonical spec, applying the standing deltas
  (repo-root paths, construction-ADR cross-references, no provenance citation,
  entry-point framing).
- [x] Regenerate `starter/AGENTS.md` from the updated canonical spec with its
  adopter-facing deltas.
- [x] Add the discipline and the backstop to the **agent operating guidance**
  checklist where lifecycle mechanics are enumerated (flag the trap, point to
  ADR-0038), in both `AGENTS.md` and `starter/AGENTS.md` as applicable.

### Guide (narrative)

- [x] If the narrative `guide.md` (and `starter/docs/guide.md`) teach the overview
  or the acceptance step, add a short passage on the stub-plan discipline and the
  "accepted, no plan" backstop, consistent with the spec.

### Demonstrate

- [x] Regenerate `overview.md` once so it renders the new "Accepted — no plan yet"
  section, verifying it is populated correctly from the current headers.

### Verify

- [x] Confirm no new status/verb/field was introduced, ADR-0012 is untouched, and
  the canonical spec and both `AGENTS.md` renderings agree.
