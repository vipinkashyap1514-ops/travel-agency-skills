---
name: review-a-pr
description: Engineering — review a pull request against the agency standards and post findings. Use when asked to review a PR or a diff. Does not merge.
---

# Playbook: review-a-pr

## Owner
Aditya for the final review; Zoya in addition for anything
touching auth / payments / PII / tenancy / suppliers; any engineer for a peer
review.

## Steps
Work the module 05 checklist **in order** — stop-ship items first:

1. **Security invariants** (module 02) — does it touch auto-send, background
   polling, supplier-rate exposure, or booking-state advancement, even
   indirectly? Any weakening is stop-ship.
2. **Tenant isolation** (module 06) — every new tenant-data query scoped by
   mechanism? Every object-by-id returned with an ownership check? Caches
   tenant-keyed? Jobs carry tenant context? A gap here is sev-1.
3. **Correctness** (module 07/09) — money as integer minor units + currency;
   time UTC / airport-local, tz-safe; booking state changed only via a guarded
   transition; committing transitions require a human actor; edge cases (empty,
   concurrent, partial supplier failure).
4. **Supplier calls** (module 08) — timeout, bounded idempotent retry,
   idempotency key on mutations, breaker, no credentials/PII/net-rate in logs,
   normalised at the boundary.
5. **Tests** (module 10) — present, meaningful, matching the change; regression
   test for a bug fix; the tenant negative test; contract test if a supplier is
   touched.
6. **Observability** (module 12) — can we tell in prod if this works/breaks?
7. **Migrations** (module 11) — expand/contract, safe during a rolling deploy,
   tested at volume, not destructive.
8. **Reuse & simplicity** — existing code for this? Smallest thing that works?
9. **Rollback** — revertable, or the PR says how to back out.
10. **Secrets** (module 17) — nothing sensitive added to the repo/fixtures.

## Output
Findings ranked most-severe first, each with file:line, why it matters, and the
concrete fix. A clear verdict: **stop-ship issues / needs changes / looks good
to merge** — but you **do not merge**; a human does.

## Stop / escalate
Any stop-ship item (invariant weakened, tenant leak, secret, money-as-float,
state guard missing) → call it out prominently and flag to the human.
