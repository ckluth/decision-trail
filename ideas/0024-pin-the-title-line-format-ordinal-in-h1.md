# Idea 0024: pin the title-line format so the ordinal is always visible in the H1

- Date: 2026-07-11
- Status: promoted
- Promoted to: [ADR-0028](../decisions/0028-pin-the-title-line-format-ordinal-in-h1.md)

## Observation

The artifact **title line (H1) has no stated format**, so it drifted into two
schemes per family and diverged across families:

- **Ideas** — `# N. Title` (0001–0005, 0014, 0015) vs. `# Idea: Title` (the rest).
- **Decisions** — `# N. Title` (0001–0014) vs. `# ADR-NNNN: Title` (0015–0027).
- **Plans** — `# N. Title` (0001–0004) vs. `# Plan: Title` (the rest).

This is the **same class of bug** ADR-0025 (numbering) and ADR-0026 (header
rendering) diagnosed: a convention that lives as **folklore, not a stated,
checkable rule**, so each new artifact copies its nearest neighbor and the drift
self-propagates. **ADR-0026 pinned the bulleted header block but left the title
line specified only as "a `# Title` line"** — an unpinned corner. That is why the
three families each drifted a different way.

## Why it matters (not cosmetic)

The **ordinal is the spoken handle** for an artifact — we say "promote idea 17",
"does ADR-27 cover this?". The one place a reader is actually looking, the open
editor pane, is exactly where that handle should appear. When the H1 omits the
number, a reader who has just read the content must go cross-reference the filename
tab to recover the very identifier they will use to talk about it — an everyday
friction the title line should remove.

## Desired means (sketch)

Pin a canonical title-line form that **carries the ordinal, zero-padded to equal
the filename slot, with the family named**:

- `# Idea 0017: Title`
- `# ADR-0017: Title`  *(decisions already do essentially this)*
- `# Plan 0017: Title`

This keeps the **filename authoritative** (ADR-0015: the number lives in the slot)
while surfacing the spoken handle at a glance — the H1 number is a *visible echo*
of the filename, not a second source of truth.

Because the title ordinal must equal the filename ordinal, that agreement becomes a
**machine-checkable invariant**: extend the conformance check (ADR-0022, already
carrying the header-format check from ADR-0026) with a trivial string compare of
the H1 ordinal against the filename slot. This turns the "two copies can disagree"
risk into a *caught error* rather than silent drift — the same hardening pattern as
ADR-0025 / ADR-0026.

## Addressing the objections

- **Redundancy / two copies can disagree** → resolved by the conformance check
  above; the redundancy becomes a guardrail, not a hazard.
- **Insert-and-shift renumber churn (ADR-0025)** → real but rare (the exceptional
  case), and the same check makes a missed title rewrite loud instead of silent.

## Resolved (ready for proposal)

- **Exact form — settled.** Typed + zero-padded: `# Idea 0017: Title`,
  `# ADR-0017: Title`, `# Plan 0017: Title` — matches the existing cross-link
  vocabulary (`ADR-0015`, `Idea-0019`) and names the family.
- **Scope of the sweep — settled.** One implementing plan sweeps all three
  families together, then `overview.md` is regenerated once at the end (not
  per-family passes, not a forward-only cutover).
- **Relationship to ADR-0026 — settled.** The resulting ADR **amends ADR-0026**
  (reciprocal `Amended by: ADR-NNNN` added to ADR-0026) rather than superseding it
  or being folded into it — an accepted ADR is a closed record; refinements are new,
  cross-linked ADRs (promise #3 Transparency, promise #5 Agility via new threads,
  not silent mutation).
- **Refresh-procedure wording — settled.** The same implementing plan updates the
  overview-refresh text at its **canonical source**, `starter/docs/working-method.md`
  (currently "scan for `# N. Title`"), then regenerates `AGENTS.md`'s derived method
  body from it (ADR-0014) — never hand-patching `AGENTS.md` directly, which would
  only be undone by the next regeneration and split the two texts (promise #2).

All four open questions are resolved; this idea is ready to mature into a
proposal (an ADR amending ADR-0026).
