---
name: ticketing-time-limit-watch
description: Operations: scheduled sweep of open unticketed work items for ticketing time limits near or past expiry; flag to Sales/Care/GM. Runs only when the shift is enabled.
---

# Playbook: ticketing-time-limit-watch

## Owner
Operations (shift-based — see `ORG.md`; OFF until switched on)

## When to use
On schedule, every 2 hours during business hours, when the shift is enabled.

## Inputs
- All open work items with a held/unticketed booking.
- Each booking's TTL (date/time/timezone).
- The warning window (default: 24 hours before TTL).

## Steps
1. **Enumerate** every open work item with an unticketed booking.
2. For each, **read the current TTL** — re-check it against the airline/GDS,
   don't trust a stale value; airlines can shorten a TTL
   (`operations/08`, `24`).
3. **Flag anything inside the warning window** (TTL − 24h or sooner):
   - Note the work item, customer, TTL, and what's outstanding (payment?
     customer decision? document?).
   - Route the flag to the owning department (Sales or Care) **and** the GM.
4. **Flag anything already past TTL** as urgent — the fare may already be
   gone; Operations re-checks fare validity and states whether it still holds
   (`fare-rule-summary` step 5).
5. **Log** the sweep result (count checked, count flagged) even if nothing
   flagged — a clean sweep is a recorded result.

## Handoffs
→ Sales / Care: each flagged item, with what's outstanding. → GM: the summary.

## Output
```
Sweep <timestamp>: <N> unticketed items checked.
Within 24h of TTL: <list — work item, customer, TTL, outstanding>
Past TTL: <list — work item, fare-still-valid? y/n>
```

## Guardrail checks
- This is a read/flag activity only — no ticketing, no state change
  (`GUARDRAILS §2`).
- Runs only when the shift is switched on (`GUARDRAILS §6` — no background
  polling otherwise).

## Stop / escalate
- Any item past TTL where the fare is now gone → escalate immediately; a
  customer may need re-quoting.
- A pattern of items reaching the warning window with payment still
  outstanding → flag to the GM as a process issue, not just individual items.
