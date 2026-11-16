---
name: fix-a-bug
description: Engineering — reproduce, root-cause, and fix a bug on a branch with a regression test. Use for any reported defect in the agency platform.
---

# Playbook: fix-a-bug

## Owner
Aditya triages; the relevant specialist fixes. Domain-ambiguous bugs go to
Operations first to confirm the correct behaviour.

## Steps
1. **Confirm and reproduce.** Get exact steps, environment, tenant, timestamps.
   Reproduce locally or from a saved payload (module 08 replay). If you can't
   reproduce, say so — don't guess-fix.
2. **Classify.** Severity (outage / data-loss / security / degraded / cosmetic).
   Security, data-loss, or tenant-leak → escalate immediately (still fix on a
   branch, but flag now).
3. **Root cause** — not the symptom. Trace it (module 12). Is it correctness
   (money/time/state/tenancy), a supplier-resilience gap, or a logic error?
   Fix the cause (`feedback_approach` — root causes, not patches).
4. **Write the failing test first** — it reproduces the bug and fails on the
   current code (module 10).
5. **Fix on a short-lived branch.** Smallest change that addresses the cause.
6. **Test passes; run the full suite.** Check the fix didn't move the problem.
7. **Check for siblings** — the same bug pattern elsewhere in the codebase.
8. **Observability** — if this was hard to detect, add the metric/alert that
   would have caught it (module 12).
9. **PR** with: the reproduction, the root cause, the regression test, blast
   radius, rollback.

## Output
Branch · root-cause explanation · regression test · PR · any sibling bugs found
· Guardrail check · escalations.

## Stop / escalate
Security / data-loss / tenant-leak (flag now) · can't reproduce · the fix needs
a prod migration · the "bug" is actually correct behaviour the user
disagrees with → back to Operations/Product.

## Never
Merge or deploy the fix. Hotfix urgency doesn't change this — open the PR, flag
it urgent, a human ships it.
