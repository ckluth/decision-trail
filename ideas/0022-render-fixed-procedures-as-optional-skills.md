# Idea 0022: render the method's fixed procedures as optional skills

- Date: 2026-07-11
- Status: promoted
- Parent: [0020](0020-use-the-method-economically-and-token-saving.md)
- Promoted to: [ADR-0036](../decisions/0036-render-fixed-procedures-as-optional-skills.md)

## Why this budded from 0020

Idea 0020 asked how to *operate* the method economically; it was **decomposed**
(ADR-0027) into three axes. One driver of the cost an agent pays every session is
that the method's fixed **procedures** are carried as step-by-step prose in the
always-loaded `AGENTS.md`. Sibling idea 0021 handles the *compaction* of that file
and sibling idea 0023 the *resume-time* discipline; this idea is the distinct,
mechanism-adding thought: move the procedures themselves into **invokable skills**
loaded only when needed. The three share 0020's motivation but are separable —
compaction is a refactor of existing prose, skills add a new (optional,
tool-specific) mechanism — so they get their own threads.

## Observation

Several method operations are **lookups, not judgment calls** — deterministic step
lists that only matter *when invoked*, yet today they sit in always-loaded context
taxing every session that never runs them:

- regenerate `overview.md` (header scan → rewrite the three tables);
- create the next artifact (max+1 slot, verify unused, canonical header);
- insert-and-shift renumber;
- disentangle a large idea (the fixed budding procedure);
- adopter update / conformance check (already do-guidance in `adopting.md`).

## Desired means (sketch)

Package these as optional **skills / commands** loaded **only when triggered**.
Two benefits:

- **Smaller always-loaded context** — the step lists leave `AGENTS.md`, which
  keeps only *principles + when to invoke which procedure*.
- **More reliable execution** — an executable skill is followed more faithfully
  than a step list buried in prose (cf. the ADR-0026 "bare header silently missed"
  failure class, where a procedural detail was easy to overlook).

## Open questions / tensions

- **Tool-agnosticism (ADR-0006) vs. skills.** Skills are somewhat tool-specific,
  and the method prizes plain-markdown transparency (promise #3). Clean framing:
  the procedures stay **canonical prose in the method**; skills are an *optional,
  derived, tool-specific rendering* of them — the same relationship `AGENTS.md`
  already has to `working-method.md` (ADR-0014). Does that framing hold?
- **Source of truth / sync (ADR-0014).** If skills are derived, they must
  regenerate from the canonical procedure text, never drift into a second
  authority. What keeps them in sync?
- **Do skills ship in `starter/` so adopters inherit them, or are they home-repo
  tooling?** If canonical prose is the source of truth, adopters could regenerate
  their own skills for their own toolchain; the method need not ship any.
- **Relationship to compaction (0021).** Skills *enable* deeper compaction (once a
  procedure lives in a skill, its prose can shrink to a pointer), so the two ideas
  likely inform each other at promotion even though each gets its own ADR.

## Controller's cost view (tokens & cents)

A cost-only analysis — no other optimization aspect — of what skills could actually
save. All figures are order-of-magnitude, measured against this repo.

**The cost base (always-loaded per session).**

| Always-loaded | chars | ≈ tokens |
|---|---|---|
| `AGENTS.md` (the method tax) | ~21,300 | ~5,300 |
| `copilot-instructions.md` (pointer) | ~940 | ~235 |
| `overview.md` (loaded only when status/regen is touched) | ~19,900 | ~5,000 |

The **skill-candidate procedures** (refresh, max+1 slotting, insert-and-shift,
disentangling, header/heading mechanics) total ≈ **4,000–4,600 chars ≈ ~1,100
tokens ≈ ~20% of `AGENTS.md`**. That ~1,100 tokens is the *entire* addressable
prize on the cost axis; the contract, lifecycle table, and when-to-invoke guidance
stay loaded either way.

**Two facts shrink the prize.**

1. **Prompt caching already neutralizes most of it.** `AGENTS.md` is a stable
   prefix → cached at ~10% of fresh input. Illustrative pricing (input $3/M, cached
   $0.30/M, output $15/M), a 15-turn session: the method file costs ~$0.24 uncached
   vs **~$0.04 cached** — a ~6× cut before skills touch anything. Skills would trim
   the *cached* prefix, i.e. the already-cheap part.
2. **Procedures load anyway in productive sessions.** Nearly every real business
   session invokes *create-next-artifact* and *regenerate-overview*. A skill only
   defers loading to invocation, so the saving is realized just on sessions that
   *never* run the procedures — which are already the cheap sessions.

**The ratio (representative 15-turn productive session).**

| Bucket | ≈ billed cost | share |
|---|---|---|
| Business topic: output tokens (~12k @ $15/M) | ~$0.18 | ~25% |
| Business topic: artifact reads + growing context + `overview.md` | ~$0.45 | ~68% |
| **Method tax** (`AGENTS.md`, cached) | ~$0.04 | **~6%** |
| — of which, **skill-addressable procedures** | ~$0.008 | **~1%** |

→ **Method-cost : business-cost ≈ 1 : 15.** The slice skills can actually remove
≈ **1 : 80** of session cost, and only on procedure-free sessions.

**Cost verdict.** On pure token/cent economics skills are **not** worth it: ~1% of
session cost addressable, ~90% of that already neutralized by caching, and it turns
**negative** once the recurring build + sync liability is booked (a derived
rendering per ADR-0014 must be regenerated whenever a procedure changes, or it
drifts into a second authority). Prior work — compacting `AGENTS.md`, adding user
guidance — already harvested the cheap wins. The larger cost lever, if one is
wanted, is keeping **`overview.md` (~5,000 tokens)** out of context — not these
~1,100 procedural tokens.

## The non-cost aspect: structure for non-conversational users

A separate ledger from cost. Some users are uncomfortable with a conversational
method and want a more **structured, guided** way to work; an executable skill is
also followed **more reliably** than a step list buried in prose (cf. ADR-0026's
"bare header silently missed" failure class — this idea's second stated benefit).
This value is real but is **UX / adoption / reliability**, *not* tokens or cents —
so if skills are promoted, the ADR must rest on *this* axis and explicitly record
that the token saving is marginal. Defending skills on cost would be a
mis-attribution.

## Options on the table

- **A — Drop.** The cost case is ~1% and net-negative after sync maintenance; the
  reliability/UX case, while real, may not clear the tool-agnosticism (ADR-0006) and
  transparency (promise #3) tensions. Record the finding and close the thread.
- **B — Promote on the reliability/UX axis only.** Frame the ADR around structured
  guidance for non-conversational users and more faithful procedure execution;
  state plainly that token savings are marginal. Keep skills an *optional, derived,
  tool-specific rendering* of canonical prose (the `AGENTS.md`↔`working-method.md`
  relationship, ADR-0014), home-repo tooling first, not shipped in `starter/`.
- **C — Park.** Keep as `seed`; revisit only if a concrete adopter demand for
  structured/guided operation appears, since that — not cost — is the deciding
  driver.

## Outcome: promoted

The promote-or-drop question was resolved in favour of **promotion** — so the
"decision against" (if that is where the weighing lands) is documented transparently
as a rejected ADR rather than buried in a dropped idea. The full picture above now
lives on in [ADR-0036](../decisions/0036-render-fixed-procedures-as-optional-skills.md),
whose proposal is to **adopt** skills (option B); the accept-vs-reject weighing
happens there.
