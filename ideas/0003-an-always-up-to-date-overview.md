# 3. An always up-to-date `overview.md`

- Status: promoted
- Date: 2026-06-28
- Parent: (none)
- Promoted to: [ADR-0011](../decisions/0011-an-always-up-to-date-overview-as-a-derived-status-index.md)

## Idea

As more and more artifacts accumulate, the lifecycle directories alone stop
giving a quick sense of *what is open and what is done*. We want an
always-current `overview.md` that lists, in a table, every idea, decision, and
plan with:

- its **name**,
- its **creation date**, and — most importantly —
- its **state**.

The intention is a simple **to-do / what's-done** list that lets a human keep
track as the artifact set grows. It matters because:

- more and more ideas may sit at status `seed` — meaning *not now, but do not
  forget*;
- more and more decisions may sit at status `proposal` — *deferred for later
  processing*;
- plans accumulate across `draft` / `active` / `done` / `abandoned`.

The overview surfaces all of that at a glance.

## Responsibility

- **The agent** keeps the overview up to date — it refreshes it after doing
  work that changes any artifact's state.
- **The user** may also manually flip a state on their own behalf (e.g. move an
  idea from `seed` to `dropped`), and the overview should reflect that.

## Open questions (to be settled by the promoted ADR)

- Where does `overview.md` live, and does it ship in `starter/` for adopters?
- Is it generated/derived (and if so, by what), or hand-maintained the-way?
- Where does the "creation date" come from — a header field, git history, or
  the filename?
- How do we keep it from drifting out of date (the core risk of any derived
  index)?
