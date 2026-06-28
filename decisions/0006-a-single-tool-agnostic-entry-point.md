# 6. A single tool-agnostic entry point (AGENTS.md)

- Status: accepted
- Date: 2026-06-28

## Context

ADR-0001 to ADR-0005 made the method structurally complete: five lifecycle
stages across three artifact families (`ideas/`, `decisions/`, `plans/`), a
fixed layout, and a cross-link vocabulary. But there is no single place that
*teaches* the method. A fresh session, or a host project adopting the-way, would
have to reconstruct the whole picture by reading five ADRs in order.

That conflicts with the promises:

- **Continuity** (#1): picking up after context is gone should be cheap — ideally
  one file to read first.
- **Genericity** (#7): the entry point must not be bound to a single tool. The
  contract presently lives in `.github/copilot-instructions.md`, which is
  Copilot-specific.
- **Borrow, don't invent** (#8): promise #8 names agent hand-off files —
  `AGENTS.md` / `copilot-instructions.md` — as the standard to borrow. `AGENTS.md`
  is the emerging cross-tool convention that many agents read by default.

## Decision

The method's canonical entry point is a top-level **`AGENTS.md`**.

- `AGENTS.md` is a concise teaching index. It states what the method is, maps the
  five lifecycle stages to the three artifact families, lists the artifact
  statuses and the cross-link vocabulary (ADR-0005), and points a reader to the
  decision log and the contract.
- It is **tool-agnostic** — the file any agent or human reads first, regardless
  of which assistant is in use (Genericity #7, Borrow #8).
- **Single source of truth for the contract:** the eight promises keep their one
  home in `.github/copilot-instructions.md` for now. `AGENTS.md` *links* to that
  file for the full contract rather than copying it, so the two never diverge
  (Economy #2). Migrating the contract into `AGENTS.md` and reducing tool files
  to thin pointers is left as a future decision.
- `AGENTS.md` is itself a borrowed hand-off artifact, not a lifecycle artifact;
  like the contract file, it lives outside the `ideas/` / `decisions/` / `plans/`
  families (consistent with ADR-0005).

## Consequences

- A returning session or a new adopter reads **one** file first and can navigate
  everything else from it (Continuity #1).
- The entry point is now tool-neutral, even though the contract text still lives
  in a Copilot-specific file; the link keeps a single source of truth while
  deferring the larger migration (Economy #2, Genericity #7).
- `AGENTS.md` must be kept in step with future ADRs that change the lifecycle or
  layout. Because it only *summarizes and links*, that upkeep is small.
- With an entry point in place, the method is now both structurally complete and
  approachable. Remaining work shifts from defining mechanics to *using* them —
  e.g. recording the next real idea, or writing the first plan.
