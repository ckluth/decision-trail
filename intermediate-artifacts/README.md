# Intermediate artifacts

This folder is decision-trail's own **optional, informal scratch persistence layer
for the execution stage** (ADR-0020). When executing a plan, a step sometimes needs
to *gather* material first — pull data together, extract or transcribe findings,
capture intermediate outputs — and work on it later, across steps or sessions. Park
that material here.

**What this is not:** it is **not a source of truth.** The ideas, decisions, and
plans remain the only source of truth. Intermediate artifacts hold disposable
working material, sit outside the idea → proposal → decision → plan → execution
lifecycle, and carry no cross-link fields. They may drift or go stale harmlessly,
because nothing authoritative depends on them.

**How to use it:**

- **Guard-free.** Creating, populating, and deleting files here touches nothing
  authoritative — no ADR, no plan, and no confirmation guard.
- **Internally unstructured.** Organize the contents however suits the work; one
  subfolder per plan is a fine option, not a rule.
- **Committed by default.** These files are committed to git by default, so gathered
  material survives across machines and sessions. To keep purely-local scratch,
  gitignore this folder instead.
- **Left to rot harmlessly.** When a plan is done, its intermediate artifacts can be
  left in place; prune them if you like, but nothing requires cleanup.

This folder currently holds no live material — it stands ready for the next plan
that needs to park gathered work.
