# ADR-0038: A stub-plan-at-acceptance discipline plus a derived "accepted, no plan" backstop

- Status: accepted
- Date: 2026-07-15
- Promoted from: [idea 0032](../ideas/0032-surface-accepted-adrs-still-awaiting-a-plan.md)
- Amends: ADR-0011 (extends the overview's shape with a third derived view), ADR-0034 (adds the blind-complement view alongside the ADR → plans sub-index)

## Context

An accepted ADR does not always stand on its own. Some decisions are
self-executing at acceptance — a naming rule, a policy, a header-format pin — and
need no plan. Others are only a *spec*: they come alive only when a plan carries
them out (ADR-0037). The second kind can silently sit undone. Nothing in the
rendered trail surfaces "accepted, but nothing is carrying it out yet."

ADR-0034 gave `overview.md` an ADR → plans sub-index, but by design it lists only
ADRs that *already have* a plan, and deliberately keeps plan-less ADRs absent. Its
blind complement — the accepted decisions with no plan — is exactly what a human
oversees (misses). A human scanning for "what still needs execution?" has nothing
to read; they must grep, reason, or ask the agent (against Transparency #3 and
Continuity #1).

The naive fix — a derived table of every accepted ADR with no `Implements:`
back-pointer — fails on its own, because it cannot answer the one question its
reader asks per row: **is this ADR intended to stand for itself, or is a plan
genuinely missing?** Most rows would be self-standing false positives, and a noisy
helper is one the human learns to ignore. Encoding the answer as a "plan-required"
flag on the ADR is rejected up front: that is the write-once, churn-prone
reciprocal field ADR-0012 already ruled out.

### Decision drivers

- **Transparency (#3) / oversight:** a human should see "accepted but not yet
  executed" by reading a plain file, not by grepping or asking the agent.
- **Economy (#2):** the view must be free — derived from data artifacts already
  carry (`Implements:`, plan `Status:`), with no new hand-maintained field.
- **No new state or verb (Agility #5 / Borrow #8):** solve this with the existing
  lifecycle vocabulary; do not add a "plan-required" flag or a new status.
- **Honesty about safety (ADR-0019's spirit):** whatever catches the gap must
  acknowledge that the human who classifies it is fallible.

### Considered options

1. **Derived "no plan" table only.** Free, but cannot distinguish intended from
   gap; dominated by self-standing false positives → noise.
2. **A "plan-required" marker on the ADR, then derive the table from it.** Precise,
   but adds a write-once reciprocal-style field — the churn/drift ADR-0012 ruled
   out. Rejected.
3. **A discipline only — stub `draft` plan at acceptance, no table.** Makes
   "no plan" mean "self-standing" for free, but offers no backstop when the human
   forgets the stub; the gap can still hide.
4. **Combine 1 + 3 (chosen).** The discipline makes "no plan" meaningful; the
   derived table catches what the discipline misses. Each covers the other's
   weakness, and no new state or verb is introduced.

## Decision

Adopt **two halves that complete each other**, reusing only existing verbs and the
existing `draft` plan status — introducing no new field, status, or cross-link.

1. **Stub-plan-at-acceptance discipline (the classifier).** When accepting an ADR
   that needs execution, the human writes its plan then and there — at minimum a
   one-line **`draft`** stub that `Implements:` it. This is agent-and-human
   operating guidance (a practice, like the confirmation guard), not a method verb.
   It reuses the existing `draft` status, whose meaning ("accepted decision,
   execution not yet started") already *is* "gap, not yet alive." The
   classification of intended-vs-gap happens here — once, by a person, at the right
   moment. From then on the **absence** of a plan carries information for free: the
   ADR needed none.

2. **Derived "Accepted — no plan yet" backstop (the safety net).** Add a third
   derived section to `overview.md` (ADR-0011), regenerated wholesale in the same
   pass as the ADR → plans sub-index (ADR-0034) and carrying the same "as of"
   stamp. It lists every **accepted** ADR that no plan points at via `Implements:`.
   It is built only from existing headers — no new field, ADR-0012 untouched. Its
   job is not to *classify* but to *catch*: because the discipline, like the
   confirmation guard, is never perfectly safe, this is a short **review queue** the
   human periodically clears — per row, either "yes, self-standing → leave it" or
   "oops → write the stub."

**The residual, owned honestly.** The backstop table *alone* can never distinguish
"intentionally self-standing" from "genuine gap" — and that is exactly *why* it is a
backstop, not the classifier. The discipline is what draws that line, at acceptance
time. The method text must state this plainly rather than imply the table
classifies. Division of labour: the discipline minimizes real gaps; the table
catches the residual. A well-run repo's section trends toward just the few, stable
self-standing ADRs.

**Scope.** This amends ADR-0011's definition of `overview.md`'s shape (a third
derived view) and sits alongside ADR-0034's sub-index. It explicitly leaves
ADR-0012 (no ADR→plan back-link) untouched — the ADR artifact gains no field; only
the derived snapshot and the operating guidance change. Reciprocal `Amended by:`
back-links are added to ADR-0011 and ADR-0034 on acceptance.

## Consequences

- A human reading `overview.md` can see, in one derived place, which accepted
  decisions have nothing carrying them out — without grep or asking the agent
  (Transparency #3, Continuity #1).
- The `draft` stub-plan discipline gives "no plan" a stable meaning, so the
  backstop's rows trend toward genuinely self-standing ADRs and stay low-noise.
- No new authoritative state, status, verb, or field is introduced; both halves
  reuse the existing `draft` status, the `Implements:` link, and existing
  practices. ADR-0012 stands unchallenged.
- The refresh procedure (in the working-method spec and `AGENTS.md`) gains one more
  derived section to produce from the same header scan it already performs — a
  small, bounded addition.
- A residual ambiguity remains by construction — the table cannot self-classify a
  row — and is deliberately accepted, carried by the discipline and the periodic
  human review rather than by new machinery.
- A plan is needed to carry this out: state the discipline in the method text and
  agent operating guidance, extend the `overview.md` template and refresh procedure
  to render the "Accepted — no plan yet" section, add the reciprocal `Amended by:`
  back-links to ADR-0011 and ADR-0034, and regenerate `overview.md` once to
  demonstrate it.
