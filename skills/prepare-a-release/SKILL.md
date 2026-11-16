---
name: prepare-a-release
description: Engineering/QA — assemble and gate a release: confirm what's shipping, run the checks, write the notes and the rollout/rollback plan, and hand a human a go/no-go. Use before a deploy. Does not deploy.
---

# Playbook: prepare-a-release

## Owner
Sneha gates it; Gaurav owns the rollout/rollback plan; Aditya
signs the go/no-go recommendation.

## Steps
1. **Scope** — list every merged PR since the last release, each with its
   one-line note and blast radius. Flag anything touching invariants, tenancy,
   money, state, or a migration.
2. **Checks** (module 11) — full test suite green (unit / integration /
   contract), security checks (dependency audit, secret scan), CWV budget for
   the frontend, migration safety review.
3. **Migrations** — if any: confirm expand/contract, safe during rolling
   deploy, tested at volume. Sequenced correctly relative to the code.
4. **Feature flags** — what's shipping dark vs enabled; the enable plan
   (which tenants/traffic first).
5. **Rollout plan** — staged where possible; the metrics to watch (module 12)
   and the thresholds that mean "stop / roll back".
6. **Rollback plan** — for every change: revert-by-redeploy, or the flag to
   toggle, or (for a migration) the specific back-out steps.
7. **Release notes** — human-readable, who's affected, any action needed.
8. **Go / no-go recommendation** — with the residual risks stated.

## Output
The release manifest (PRs + notes) · check results · migration sequence ·
flag/enable plan · rollout + rollback plan · watch metrics & thresholds ·
a clear **go / no-go** recommendation for the human who deploys.

## Stop / escalate
Any check red · a destructive or unsequenced migration · a change with no
rollback path · a stop-ship review finding not yet resolved.

## Never
Deploy. Produce the plan and the recommendation; a human deploys and watches.
