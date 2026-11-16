---
name: implement-a-feature
description: Engineering — take a feature request from spec to a reviewed PR on a branch. Use when Engineering is asked to build something new in the agency platform.
---

# Playbook: implement-a-feature

## Owner
Aditya scopes it; the relevant specialist (Karan / Isha /
Tara / Farhan) builds it.

## Steps
1. **Spec** (module 05). Write the design note: problem, approach, alternatives,
   what it touches (services / data / APIs / suppliers / **the 5 security
   invariants** / tenancy / money / time / booking state), test plan, rollout &
   rollback plan, open questions. Aditya reviews it before code.
2. **ADR** if any part is reversal-expensive (datastore, framework, auth model,
   public API shape) — `docs/adr/`, Aditya sign-off.
3. **Branch** — short-lived, off the main branch, one focused change.
4. **Build in small steps**, each leaving the system working:
   - Tenant-scope every new query by mechanism (module 06).
   - Money as integer minor units + currency; time in UTC / airport-local
     (module 07).
   - New booking-lifecycle behaviour → explicit guarded transition; committing
     transitions require a human actor (module 09).
   - Supplier calls → timeout / bounded retry / idempotency / breaker
     (module 08).
   - Behind a feature flag if not trivially safe (module 11).
5. **Tests** (module 10) — unit for the logic, integration for the slice,
   the tenant-isolation negative test, contract test if a supplier is involved.
6. **Observability** (module 12) — logs/metrics/trace on the new path's success
   and failure modes; correlation id through any async work.
7. **Docs / release note** — update API docs, the ADR if relevant, a one-line
   changelog entry.
8. **Self-review against the module 05 checklist**, then open the **PR** with:
   the spec link, what changed, tests added, how it's observed, how it rolls
   back. Zoya review if it touches auth/payments/PII/tenancy/suppliers.

## Output
Branch name · spec/ADR link · PR ready for human review · summary of tests,
telemetry, and rollback · Guardrail check · escalations.

## Stop / escalate
Spec review raises an unresolved risk · a reversal-expensive choice with no ADR
· the change needs a prod migration or a schema change · it can't be rolled
back · it would weaken an invariant.

## Never
Merge, deploy, run prod migrations, or touch prod data/secrets. Open the PR and
hand off.
