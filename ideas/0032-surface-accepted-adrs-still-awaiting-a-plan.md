# Idea 0032: A stub-plan-at-acceptance discipline plus a derived "accepted, no plan" backstop

- Date: 2026-07-15
- Status: promoted
- Promoted to: [ADR-0038](../decisions/0038-stub-plan-at-acceptance-and-derived-no-plan-backstop.md)

## The itch

An accepted ADR that does **not** stand on its own — one that needs a plan to
come alive — can silently sit undone. The human has to *notice* it, and there is
no view that surfaces the gap. ADR-0034 gave us the ADR → plans sub-index in
`overview.md`, but that only lists decisions that already *have* a plan. Its blind
complement — "accepted, but nothing is carrying it out yet" — is exactly the thing
a human oversees (misses). Something should make that gap impossible to walk past
(Transparency #3, Continuity #1).

## The hard part

Not every accepted ADR needs a plan. Many are self-executing at acceptance (a
naming rule, a policy, a header-format pin). ADR-0034 deliberately keeps ADRs with
no plan *absent* from its sub-index for that reason. So the reader of any
"accepted without a plan" view faces one nagging question per row: **is this ADR
intended to stand for itself, or is a plan genuinely missing?** A view that forces
the human to re-reason that every time — and a view full of self-standing false
positives — is noise, and a noisy helper is one the human learns to ignore.

The design must answer that question **without adding new logic, state, or a verb**
to the method (no "plan-required" flag on the ADR — that is the write-once churn
ADR-0012 ruled out).

## The shape — two halves that complete each other

Neither half alone is sufficient; together they close the loop.

1. **Discipline (human responsibility) — the primary mechanism.** When accepting
   an ADR that needs execution, the human writes its plan then and there — at
   least a one-line **`draft`** stub. This reuses only existing verbs (accept an
   ADR, write a plan) and the existing `draft` status ("accepted decision,
   execution not yet started"). Crucially, this is *where the intended-vs-gap
   classification happens*: once, by a person, at the right moment. After it, the
   **absence** of a plan carries information for free — it means "this ADR needed
   none."

2. **Backstop (derived) — the safety net.** A derived "Accepted — no plan yet"
   section in `overview.md`, regenerated wholesale in the same pass as the ADR →
   plans sub-index and carrying the same "as of" stamp. Built only from existing
   data (accepted ADRs with no plan pointing at them via `Implements:`), it adds
   no new field (Economy #2, ADR-0012 untouched). Its job is not to *classify* but
   to *catch* — because the discipline, like the confirmation guard, is never
   perfectly safe (ADR-0019's spirit). It is a short **review queue** the human
   periodically clears: per row, either "yes, self-standing → leave it" or "oops →
   draft the stub."

Division of labour: the discipline minimizes real gaps; the backstop catches the
residual. A well-run repo's table trends toward just the few, stable self-standing
ADRs.

## The residual to own honestly

The backstop table *alone* can never distinguish "intentionally self-standing"
from "genuine gap" — and that is precisely *why* it is a backstop, not the
classifier. The discipline is what makes that distinction, at acceptance time. Any
proposal must state this residual plainly rather than pretend the table classifies.

## Not yet decided (for the proposal, not this seed)

- Exact phrasing of the acceptance-time discipline and where it lives (agent
  operating guidance? the lifecycle's decision-stage text?).
- Heading, placement, and columns of the backstop section; whether rows render any
  caveat text or stay bare.
- Whether the backstop is a distinct section or a rendering of the `draft`-status
  rows already inside ADR-0034's sub-index.
- How this amends ADR-0011 / ADR-0034 (the overview's shape) — and confirming it
  leaves ADR-0012 (no ADR→plan back-link) untouched.
