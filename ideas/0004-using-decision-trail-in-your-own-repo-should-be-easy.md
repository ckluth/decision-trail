# Idea 0004: Using decision-trail in your own repo should be as easy as possible

- Status: promoted
- Date: 2026-06-28
- Promoted to: [ADR-0021](../decisions/0021-a-single-adopter-on-ramp-fresh-inject-update.md)

## Idea

The goal is simple to state: make it **as easy as can be** for someone to use
decision-trail in their own repo — from the very first adoption through every
later upgrade. Ideally the adopting agent has to do almost **nothing**; at most it
follows a small, clearly stated set of steps.

This whole concern rests on **two preconditions** — the only things an adopter
must bring:

1. **A git repo.** Local or hosted, it makes no difference; decision-trail is
   plain markdown under version control.
2. **An agentic setup.** You work with an agent and your preferred harness. Every
   agent knows how to handle an `AGENTS.md`, which is the method's entry point, so
   no harness-specific wiring is required.

Given those, three **scenarios** cover the full lifecycle of using the method, and
each should be a clean, bounded operation:

1. **Fresh repo.** "I want to set up a new repo directly with decision-trail." A
   near-empty repo becomes a decision-trail repo in one move.
2. **Inject into an existing repo.** "I want to add decision-trail to a repo that
   already has code and history." The method must drop in alongside existing
   content without disturbing it, and without inheriting this repo's construction
   ADRs.
3. **Update.** "I want to move from decision-trail `X.Y` to `X.Y+n`." Pulling a
   newer version into an already-adopting repo should be cheap and low-risk —
   ideally a no-op, otherwise a small, explicit migration.

The update scenario is the one with teeth: a release can carry *adopter-facing
migration work*. For example, going from 1.2.0 to 1.3.0 was **not** a no-op — it
made a `Date:` header field mandatory on ideas and plans, added `overview.md`, and
added the reciprocal `Promoted from:` link. An adopter already holding idea and
plan files would have to **backfill the `Date:` fields**, create a first
`overview.md`, and optionally add `Promoted from:` back-links — otherwise its
artifacts no longer match the method it cites. Right now nothing tells the adopter
what that work is.

The shape of the answer is likely **a mix**: mostly pure do-guidance (steps an
agent follows), possibly complemented by **lightweight tooling support** where
plain instructions are error-prone — but any tooling must stay true to
**Borrow, don't invent (#8)** and **Economy (#2)**, and must not turn a
plain-markdown method into something with a heavy runtime dependency.

## Why it matters

- **Economy (#2) / Continuity (#1):** adopting or upgrading decision-trail should
  be a clean, bounded operation, not an archaeology project across the adopter's
  files.
- **Genericity (#7):** the on-ramp must work for any repo — fresh or established —
  without assuming a particular project shape.
- The method is "settled, not frozen" — versions *will* keep coming, so both the
  initial on-ramp and the recurring upgrade path are costs worth minimizing once,
  for everyone who adopts.

## Relationship to existing decisions

ADR-0008 already decided *how* a repo adopts: by **copying the `starter/`
skeleton**, treating this repo as the versioned standard. This idea does not
re-open that; it sits on top of it as the **end-to-end onboarding & lifecycle**
concern — covering the inject-into-existing and update scenarios that ADR-0008
left open, and the guidance/tooling that makes all three scenarios turnkey.

## Open questions (for the promoted ADR to settle)

**Across all scenarios:**

- How much of the answer is pure do-guidance versus lightweight tooling, and where
  exactly does tooling earn its keep without violating Economy (#2) / Borrow (#8)?
- Where do adopter-facing instructions live so all three scenarios are discoverable
  from one place?

**Fresh + inject:**

- For the inject case, what is the minimal, non-disruptive drop-in procedure for a
  repo that already has an `AGENTS.md`, existing docs, or its own conventions?
- How does an established repo's existing history/decisions coexist with a fresh
  decision-trail ADR log starting at 0001?

**Update:**

- Where do per-version migration notes live — a `MIGRATING.md`, a section per
  release in `CHANGELOG.md`, or a `migrations/` family?
- Can/should the agent perform the migration automatically (e.g. "backfill all
  missing `Date:` fields, then regenerate `overview.md`"), and how is that
  triggered?
- How does an adopter know *which* version it is on and *which* steps apply
  between its version and the target (the version citation is the anchor)?
- What is the contract for a release author: must every release state its
  adopter-facing migration (even if "none")?
