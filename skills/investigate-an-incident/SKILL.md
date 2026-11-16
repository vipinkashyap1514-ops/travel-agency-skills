---
name: investigate-an-incident
description: Engineering/SRE — triage a production incident (outage, degradation, error spike), stabilise via a branch fix, and write it up. Use for "site is down/slow" or an alert firing.
---

# Playbook: investigate-an-incident

## Owner
Gaurav leads; pulls in the relevant specialist.

## Steps
1. **Confirm it's real** — logs, error tracker, metrics (module 12). Not one
   report — a signal.
2. **Scope** — which service (backend / frontend / mobile), which
   feature/endpoint, how many tenants/users, since when.
3. **Correlate with recent changes first** — did it start right after a deploy?
   Check the deploy timeline before chasing an external cause.
4. **Classify severity** — full outage / data-loss risk / security / degraded /
   isolated. Data-loss or security → escalate to the human **now**, in
   parallel.
5. **Stabilise** — the fastest safe mitigation:
   - Toggle a feature flag off (module 11) — no redeploy, fastest.
   - Prepare a revert PR (redeploy the previous build) for a human.
   - Prepare a forward-fix PR on a branch with a test.
   You do not merge/deploy/rollback — you prepare it and a human executes.
6. **Communicate** — a factual status for the GM/human: what's affected, impact,
   what's being done, next update time.
7. **Write-up** — update `SESSION_HANDOFF.md` / the runbook: timeline, cause,
   fix, and the follow-ups (the missing alert, the missing test, the fragile
   code) as tracked items.

## Output
Incident summary (scope, severity, cause, timeline) · the mitigation prepared
(flag toggle instruction / revert PR / forward-fix PR) · the write-up ·
follow-up items · escalations.

## Stop / escalate
Immediately for: full outage, data-loss risk, security. Also: the fix needs a
prod migration, or the cause is a supplier outage outside our control (then
it's a comms + degrade-gracefully job, not a code fix).

## Never
Merge, deploy, or roll back yourself. Prepare it; a human executes.
