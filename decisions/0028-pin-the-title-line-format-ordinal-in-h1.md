# ADR-0028: Pin the title-line format so the ordinal is always visible in the H1

- Date: 2026-07-11
- Status: accepted
- Promoted from: [Idea-0024](../ideas/0024-pin-the-title-line-format-ordinal-in-h1.md)
- Amends: [ADR-0026](0026-pin-canonical-artifact-header-format.md)

## Context

The artifact **title line (H1) has no stated format**. It drifted into two schemes
per family and diverged across families:

- **Ideas** — `# N. Title` (0001–0005, 0014, 0015) vs. `# Idea: Title` (the rest).
- **Decisions** — `# N. Title` (0001–0014) vs. `# ADR-NNNN: Title` (0015–0027).
- **Plans** — `# N. Title` (0001–0004) vs. `# Plan: Title` (the rest).

This is the same class of bug ADR-0025 (numbering) and ADR-0026 (header rendering)
diagnosed: a convention that lives as **folklore, not a stated, checkable rule**,
so each new artifact copies its nearest neighbor and the drift self-propagates.
ADR-0026 pinned the bulleted header block but left the title line specified only
as "a `# Title` line" — an unpinned corner, which is why the three families each
drifted a different way.

This is not cosmetic. The **ordinal is the spoken handle** for an artifact — "promote
idea 17", "does ADR-27 cover this?". The one place a reader is actually looking,
the open editor pane, is exactly where that handle should appear. When the H1
omits the number, a reader who has just read the content must cross-reference the
filename tab to recover the very identifier they will use to talk about it.

## Decision Drivers

- **Readability** — the spoken handle should be visible where the reader is
  looking, not require a filename lookup.
- **Reliability** — title and filename ordinals must not silently disagree.
- **Consistency** — reuse the existing conformance check (ADR-0022 / ADR-0026)
  rather than add a parallel mechanism.
- **Economy (#2)** — one stated template, checked once, not per-artifact vigilance.

## Considered Options

1. **Typed + zero-padded title, ordinal echoes the filename slot, checked for
   agreement.** *(Chosen.)*
2. **Bare classic `# 17. Title`** (Nygard/MADR tradition, no family name) —
   rejected: less self-describing when a title is read out of context (e.g.
   pasted into a chat) and inconsistent with the cross-link vocabulary's typed
   references (`ADR-0015`, `Idea-0019`).
3. **No ordinal in the title at all** — rejected: the filename-only number forces
   a lookup at the exact moment (mid-read, in the editor) a reader needs the
   spoken handle most.
4. **Hand-patch ADR-0026 in place** instead of a new amending ADR — rejected: an
   accepted ADR is a closed record (promise #3 Transparency); refinements are new,
   cross-linked ADRs (promise #5 Agility via new threads, not silent mutation) —
   the same precedent ADR-0026 itself set by amending ADR-0011 and ADR-0022.

## Decision

Take **Option 1**. The canonical title-line form, for all three families, is:

- `# Idea 0017: Title`
- `# ADR-0017: Title`
- `# Plan 0017: Title`

Typed and zero-padded to match the filename slot exactly, naming the family. This
keeps the **filename authoritative** (ADR-0015: the number lives in the slot)
while surfacing the spoken handle at a glance — the H1 number is a *visible echo*
of the filename, not a second source of truth.

Because the title ordinal must equal the filename ordinal, that agreement becomes
a **machine-checkable invariant**: the conformance check (ADR-0022, already
carrying the header-format check from ADR-0026) is extended with a trivial string
compare of the H1 ordinal against the filename slot. This turns "two copies can
disagree" into a *caught error* rather than silent drift — the same hardening
pattern as ADR-0025 / ADR-0026.

**Implementation, carried out in one plan:**

- Sweep all three families together to the canonical title-line form (not
  per-family passes, not forward-only).
- Update the overview-refresh procedure text at its **canonical source**,
  `starter/docs/working-method.md` (currently "scan for `# N. Title`"), then
  regenerate `AGENTS.md`'s derived method body from it (ADR-0014) — never
  hand-patching `AGENTS.md` directly.
- Extend the conformance check with the title↔filename ordinal comparison.
- Regenerate `overview.md` once, at the end.
- Add reciprocal `Amended by: ADR-0028` to ADR-0026.

## Consequences

- The spoken handle ("idea 17", "ADR-27") is visible directly in the open
  editor pane — no filename lookup needed mid-read.
- Title↔filename agreement is a stated, checked invariant; drift becomes both
  less likely (template) and detectable (conformance step), not silently
  corrupting `overview.md` or conversation.
- A large but mechanical one-time sweep across all existing artifacts.
- Slightly more prescriptive title guidance — a small, justified cost, consistent
  with ADR-0025 / ADR-0026's hardening of previously unstated conventions.
