# A guide to working decision-trail

This is the gentle introduction. It tells you what the method is, why it is shaped
the way it is, and how to use it day to day. Once the ideas here are familiar, the
terse [`working-method.md`](working-method.md) is all you'll need as a quick
reference.

> Based on **decision-trail vX.Y** — https://github.com/ckluth/decision-trail

## The problem it solves

You sit down to work on a project. You think hard, weigh options, decide
something, and act. Then the session ends — and with it goes the context: *why*
you chose this over that, what you'd already ruled out, where a half-formed idea
was heading. Next time you (or a teammate, or an agent) start almost from scratch,
re-deriving reasoning that was once clear.

decision-trail is a way of working that makes that context cheap to leave behind
and cheap to pick back up. It does so with nothing more than plain markdown files
in your repo — no app, no database, no proprietary tool. Anything you can read in
a text editor, you can resume from.

## The eight promises

The method holds itself to eight promises. They're worth reading once as a whole,
because every mechanic later is just one of these promises made concrete:

1. **Continuity** — you can pick up cheaply after the session ends and the context
   in your head is gone.
2. **Economy** — leaving and resuming context is cheap; artifacts are cheap to
   write and cheap to read.
3. **Transparency** — everything is plain, human-readable markdown. Nothing is
   hidden inside a tool you must run.
4. **Lifecycle for thoughts** — a thought can travel a defined path: idea →
   proposal → decision → plan → execution.
5. **Agility** — any thread can be refined or overthrown at any time. Nothing is
   locked.
6. **Budding** — one idea can spawn another, and the parent–child link is kept, so
   you can trace where a thought came from.
7. **Genericity** — none of this is bound to a particular project; it works for
   any.
8. **Borrow, don't invent** — wherever a portable standard already exists (ADRs,
   spec-driven stages, agent hand-off files), the method leans on it instead of
   inventing something proprietary.

## The lifecycle: how a thought travels

The heart of the method is a single journey a thought can take. Not every thought
goes all the way — most ideas stay ideas — but the path is always the same, and
each stage has a home.

**Idea.** It starts as an *idea*: a cheap, small markdown file in `docs/ideas/`.
The whole point is that ideas are cheap to write, so you write them down instead
of losing them. An idea is just a seed; it carries a short note of the thought and
why it might matter. Most ideas wait here. Some get *dropped*. A few mature.

**Proposal.** When an idea has ripened enough to act on, you *promote* it. It
becomes a *proposal* — an [ADR](https://adr.github.io/) (Architecture Decision
Record) in `docs/decisions/`, opened with `Status: proposed`. The ADR is where you
lay out the context, weigh the options, and state what you propose to do.

**Decision.** A proposal doesn't move to a new file when you decide — it *becomes*
a decision in place. You flip its status to `accepted` (or `rejected`). The same
file now records both the proposal and its resolution, so the reasoning and the
outcome live together forever.

**Plan.** An accepted decision says *what* and *why*, but not *how*. That's a
*plan* in `docs/plans/`, which `Implements:` the decision and breaks it into
concrete tasks written as GitHub checkboxes (`- [ ]`).

**Execution.** Execution isn't a separate place — it's the plan in motion. You
move the plan from `draft` to `active` to `done`, ticking checkboxes as the work
lands. When the last box is checked, the thought has travelled its whole life, and
the trail of *idea → proposal → decision → plan → execution* is there to walk
later.

## The vocabulary of links

Artifacts don't just sit in folders; they point at each other, so you can follow a
trail from either end. The links are ordinary relative markdown links, but the
*field names* in the headers are fixed and greppable, so both humans and tools can
find them:

- **`Parent:`** (idea → idea) — this idea budded from another one.
- **`Promoted to:`** / **`Promoted from:`** (idea ↔ ADR) — the idea matured into a
  proposal. This link is *reciprocal*: both ends carry it, because each end is
  single and written once.
- **`Amends:`** / **`Amended by:`** (ADR ↔ ADR) — a later decision changed part of
  an earlier one. Also reciprocal.
- **`Supersedes:`** / **`Superseded by:`** (ADR ↔ ADR) — a later decision replaces
  an earlier one wholesale. Also reciprocal.
- **`Implements:`** (plan → ADR) — this plan carries out a decision.

A rule of thumb decides when a link is reciprocal: add the back-link only when
*both* ends are single and write-once. `Promoted`, `Amends`, and `Supersedes`
qualify. `Parent` and `Implements` don't get a back-link, because their reverse
side accumulates — one parent can have many children, one decision can be carried
out by many plans — and you don't want to keep editing an old file every time a
new child appears.

A quiet but important rule: **you never edit a decision away.** When a decision
changes, you write a *new* ADR that amends or supersedes the old one and link them.
The old reasoning stays readable. The trail is a history, not a current-state
snapshot you overwrite.

## The overview

Because the real state lives scattered across many artifact files, there's one
derived convenience: `docs/overview.md`. It's a single dated snapshot listing every
idea, decision, and plan with its creation date and current state — a plain
*to-do / what's-done* board.

Two things to know about it. First, it's **derived**: it is regenerated wholesale
from the artifact headers, never hand-patched, and stamped "as of <date>". The
artifacts are the truth; the overview is just a convenient mirror. Second, keeping
it current is the **agent's** job, not yours. If you flip a state directly in an
artifact, the next regeneration reconciles the overview. You can ask the agent to
regenerate it at any time.

Artifacts may also carry an optional `Tags:` header line — comma-separated theme
words that re-slice the work along a shared-theme axis, so cross-cutting threads
stay findable. Tags show up as a `Tags` column in the overview. The vocabulary is
recommended, not enforced, and curated per repo; a repo with no need simply uses
no tags.

Alongside the overview sits an optional, human-facing companion: the **travel
diary** (`docs/travel-diary.md`). Where the overview is a terse, derived status
board, the diary is loose prose — a growing, newest-first logbook you can skim
after a break to catch up on *where we are, what changed, what's left, and what's
next*. It touches no artifact and is never a source of truth; adding a chapter is a
guard-free, informal task. A repo that doesn't want one simply has none.

For the *execution* stage there's a second optional companion: an
**intermediate-artifacts** folder (`docs/intermediate-artifacts/`) — a scratch
space where a plan can park material it gathers along the way (data, findings,
intermediate outputs) to work on later. Like the diary it's informal, guard-free,
and never a source of truth; it's committed by default so the material survives a
break, and a repo that doesn't need one simply has none.

## How to start

1. Capture a thought as an idea in `docs/ideas/`.
2. When it matures, open an ADR in `docs/decisions/` with `Status: proposed`.
3. Accept or reject it; an accepted ADR is a decision.
4. Write a `docs/plans/` file that `Implements:` the decision and lists tasks.
5. Execute by moving the plan `active` → `done`, ticking checkboxes.

Your repo's `docs/decisions/0001-adopt-decision-trail.md` already records the
decision to adopt the method. Everything else grows from there.

## Working with an agent: a "yes" has a scope

When an AI agent does the work, one rule protects you above all others: the
**confirmation guard** — the agent discusses and proposes freely, but does not
*act* (write, edit, implement) until you give an explicit green light. It is the
seam between thinking and doing.

Here is the uncomfortable truth worth internalizing: **that guard is never
perfectly safe, and cannot be.** The rule is sound; the weak point is the *word you
answer with*. A bare "yes", "ok", or "go on" carries an unavoidable ambiguity of
**scope** — did you approve *just this one next step*, or the whole logical batch
that step obviously *implies*? You and the agent can each hold a different, silent
answer. The words matched; the intended scope did not. That is exactly how a
narrow "yes" to one design choice can be read as blanket approval to draft an idea,
write the decision, *accept* it, plan it, and implement the lot in a single sweep.

It is tempting to think decision-trail's **step-by-step** nature makes this
impossible. It does help — small artifacts and explicit stages give many natural
places to pause. But do not let it lull you into a false sense of safety: the guard
only truly binds when *both sides share the same picture of what a given
confirmation covers*. A step-by-step method with ambiguous "yes"es still lets a
whole batch slip through on one word.

So treat scope as a **shared responsibility**, negotiated in the confirmation
itself:

- **The agent** should, before acting, take a short look at *what it thinks it is
  confirming* against *what you might think you confirmed* — and when those could
  diverge, state its intended scope plainly instead of assuming the larger batch.
- **You**, when the scope is at all unclear, should bound the approval in words
  rather than answering with a bare "yes". A few extra words —
  *"yes, but only this single next step [...]"* — are far cheaper than a rollback.

## Where to go next

- [`working-method.md`](working-method.md) — the terse reference: the same
  contract, lifecycle, layout, and vocabulary, condensed into tables for quick
  lookup once you know your way around.
- `AGENTS.md` (repo root) — points an AI agent at the method and carries the
  **agent operating guidance** (how an agent should behave when working this repo:
  the confirmation guard, keeping the overview current, treating the method as
  settled).
- To **update or (re)adopt** decision-trail, see `adopting.md` in the standard
  repo: https://github.com/ckluth/decision-trail/blob/main/adopting.md — it covers
  starting fresh, injecting into an existing repo, and moving to a newer version.
