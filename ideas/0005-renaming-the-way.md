# Idea 0005: The name "the-way" may be too pretentious to share

- Status: promoted
- Date: 2026-06-28
- Parent: (none)
- Promoted to: [ADR-0013](../decisions/0013-rename-the-way-to-decision-trail.md)

## Idea

The name "the-way" doesn't pass the "hey colleague, look what I made — try it"
test. It sounds grand/pretentious rather than inviting. A good name should be
plain, low-ego, and hint at what the method does: carry a thought through its
life in plain markdown. Candidates to weigh: `trail`, `throughline`, `cairn`,
`stepwise`, `ledger`, `paper-trail`.

## Why it matters

- **Borrow, don't invent (#8) / Genericity (#7):** the name is the first thing an
  adopter meets; a humble, descriptive name lowers the barrier to trying it.
- A rename touches the version citation (`Based on the-way vX.Y`), the
  `starter/` skeleton, repo name, and every doc — so it's a real, bounded cost
  worth deciding deliberately, not casually.

## Open questions (for the promoted ADR to settle)

- Which name, and does it survive a quick search for collisions?
- Is a rename worth the churn across docs, tags, and the citation string?
- How do already-adopted repos handle the provenance citation post-rename?
