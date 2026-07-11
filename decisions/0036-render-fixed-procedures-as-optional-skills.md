# ADR-0036: render the method's fixed procedures as optional skills

- Date: 2026-07-11
- Status: rejected
- Promoted from: [0022](../ideas/0022-render-fixed-procedures-as-optional-skills.md)

## Context

Several method operations are **lookups, not judgment calls** — deterministic step
lists that only matter *when invoked*, yet today they live as step-by-step prose in
the always-loaded `AGENTS.md`, taxing every session that never runs them:

- regenerate `overview.md` (header scan → rewrite the three tables);
- create the next artifact (max+1 slot, verify unused, canonical header);
- insert-and-shift renumber;
- disentangle a large idea (the fixed budding procedure);
- adopter update / conformance check (already do-guidance in `adopting.md` /
  `updating.agent.md`).

This ADR was promoted from idea 0022, itself a bud of idea 0020 ("operate the
method economically", decomposed per ADR-0027). Sibling idea 0021 handles
*compaction* of `AGENTS.md` and idea 0023 the *resume-time* discipline; this
decision is the distinct, mechanism-adding question: **should decision-trail render
its fixed procedures as optional, invokable skills** loaded only when triggered?

The proposed shape keeps procedures as **canonical prose in the method**; skills are
an *optional, derived, tool-specific rendering* of them — the same relationship
`AGENTS.md` already has to `working-method.md` (ADR-0014).

## Decision Drivers

- **Token/cent economy (the promoting motivation).** A controller-style, cost-only
  analysis (order-of-magnitude, measured against this repo):
  - Always-loaded `AGENTS.md` ≈ 21,300 chars ≈ ~5,300 tokens. The
    **skill-candidate procedures** within it total ≈ 4,000–4,600 chars ≈ **~1,100
    tokens ≈ ~20%** — the *entire* addressable prize on the cost axis.
  - **Prompt caching already neutralizes most of it.** `AGENTS.md` is a stable
    cached prefix (~10% of fresh input). A 15-turn session: ~$0.24 uncached vs
    **~$0.04 cached** — a ~6× cut before skills touch anything; skills would trim
    the *already-cheap cached* prefix.
  - **Procedures load anyway in productive sessions** (nearly every real session
    runs *create-next-artifact* / *regenerate-overview*), so the saving lands only
    on procedure-free sessions — already the cheap ones.
  - **Ratio:** method-cost : business-cost ≈ **1 : 15**; the slice skills can
    actually remove ≈ **1 : 80** of session cost. On pure economics the saving is
    ~1% of session cost, ~90% pre-neutralized by caching, and **net-negative** once
    the recurring build + sync liability is booked. The larger cost lever, if one
    is wanted, is keeping `overview.md` (~5,000 tokens) out of context — not these
    ~1,100 procedural tokens.
- **Execution reliability.** An executable skill is followed more faithfully than a
  step list buried in prose (cf. ADR-0026's "bare header silently missed" failure
  class). This is a correctness gain, independent of cost.
- **Structure for non-conversational users.** Some users are uncomfortable with a
  conversational method and want a more structured, guided way to work; skills offer
  named, invokable entry points. A UX / adoption benefit — *not* tokens or cents.
- **Tool-agnosticism (ADR-0006) and transparency (promise #3).** Skills are somewhat
  tool-specific and the method prizes plain-markdown transparency; a skills mechanism
  must not become a second authority or a tool lock-in.
- **Sync burden (ADR-0014).** A derived rendering must regenerate from the canonical
  procedure text whenever a procedure changes, or it drifts — a recurring maintenance
  cost paid against a ~1% gross saving.

## Considered Options

- **A — Do not adopt (reject).** The cost case is ~1% and net-negative after sync
  maintenance; the reliability/UX case, while real, may not clear the
  tool-agnosticism and transparency tensions. Record the finding; procedures stay as
  prose. (Rejecting this ADR lands here — a documented decision against.)
- **B — Adopt on the reliability/UX axis (propose).** Introduce skills as an
  *optional, derived, tool-specific rendering* of canonical prose, framed around
  structured guidance for non-conversational users and more faithful procedure
  execution — explicitly recording that the **token saving is marginal**. Home-repo
  tooling first; **not** shipped in `starter/` (adopters regenerate their own for
  their toolchain).
- **C — Park.** Keep the thread dormant; revisit only if a concrete adopter demand
  for structured/guided operation appears, since that — not cost — is the deciding
  driver.

## Decision

**Rejected — do not adopt optional skills (Option A), for now.** The weighing:

- The **cost motivation evaporated** under analysis: ~1% of session cost is
  addressable, ~90% of that is already neutralized by prompt caching, and the move
  is **net-negative** once the recurring sync liability (ADR-0014) is booked. Cost
  cannot carry a "yes."
- The one solid remaining benefit — **execution reliability** — has a **cheaper
  substitute already in flight**: sharpening and compacting the canonical procedure
  prose (idea 0021 + the ADR-0026 discipline). If prose is the failure surface,
  sharpen the prose; don't fork it into a tool-specific second artifact that owes
  perpetual regeneration.
- The **structured-guidance / UX benefit is real but speculative** — no concrete
  adopter has yet demanded it — and does not currently clear the **tool-agnosticism
  (ADR-0006)** and **transparency (promise #3)** tensions.

This ADR is deliberately kept as a **documented decision against**, not dropped, so
the costing and the tensions are preserved in the decisions log.

**Reopen condition.** Revisit if a **concrete adopter demand for structured / guided
operation** appears (the deciding driver would then be UX/adoption, not cost). A
future revisit is a **new ADR that supersedes this one** (`Superseded by:`,
ADR-0012), promoted from the reminder below.

**Reminder.** An active revisit reminder is tracked as seeded idea
[0030](../ideas/0030-revisit-skills-if-adopters-demand-structured-operation.md) —
so the reopen condition surfaces in the idea table of `overview.md` rather than
lying dormant inside this rejected ADR.

## Consequences

*If accepted (Option B):*

- The listed procedures gain optional skill renderings; `AGENTS.md` procedural prose
  can shrink toward *principles + when to invoke which procedure* (informing the
  compaction thread, idea 0021).
- A sync discipline is owed: skills regenerate from canonical prose on any procedure
  change (ADR-0014), a standing maintenance cost accepted for the reliability/UX gain.
- The method's cost profile is materially unchanged; no economy claim is made.

*If rejected (Option A):*

- Procedures remain canonical prose in `AGENTS.md`; no skills mechanism is added.
- This ADR records *why* — the marginal cost case and the unresolved
  tool-agnosticism/sync tensions — so the "no" is documented, not lost to a dropped
  idea.
