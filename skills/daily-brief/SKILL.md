---
name: daily-brief
description: Revenue & Data: pull the day's numbers (enquiries, quotes, bookings, revenue, booked margin, refunds, funnel, incidents, credit risk) into a two-minute brief. Read-only. Runs when the shift is enabled.
---

# Playbook: daily-brief

## Owner
Revenue & Data (shift-based — `ORG.md`, 08:00 daily; OFF until switched on)

## When to use
On schedule at 08:00 local, when the shift is enabled.

## Inputs (all read-only)
- Booking platform, CRM/pipeline, accounting, analytics, error tracker.
- Yesterday's brief (for trend comparison).

## Steps
1. **Pull the numbers** for the period (yesterday, or since the last brief):
   - Enquiries received, quotes sent, bookings made, revenue, **booked margin**
     (accrual — not blended with cash-in, `revenue-data/02`).
   - Conversions and top loss reasons from the pipeline (`revenue-data/03`).
   - Refunds / ADMs that will retroactively affect reported margin.
   - Cash position / trust-account health from Finance (separate line).
   - Deploy health / open incidents from Platform/Tech.
   - Sub-agent credit risk from Finance (`finance-accounts/06`).
2. **Compare to the prior comparable period** — note direction, not just level.
3. **Identify flags** — anything needing a decision today: margin below floor,
   refund spike, conversion drop, cash-timing risk, credit risk, incident.
4. **Write the brief** (`revenue-data/05` structure): headline → numbers →
   flags → notable. Every line earns its place; detail goes in a linked
   report, not the brief.
5. **Place the brief in the report store** and notify the GM/human.
6. If a flag is **severe** (margin floor breach, refund spike, incident) →
   surface it immediately, don't wait for tomorrow's brief.

## Handoffs
Reads from all departments; routes specific insights to the owning department
(e.g. "lost to price on Bali x3 months" → Product).

## Output
```
DAILY BRIEF — <date>
Headline: <one line>
Numbers: enquiries <n> · quotes <n> · bookings <n> · revenue <x> · booked margin <x>
Flags: <decisions needed today, or "none">
Notable: <1–2 non-urgent items>
Full detail: <link>
```

## Guardrail checks
- Read-only — writes nowhere except the report store (`agents/revenue-data.md`).
- Runs only when the shift is on (`GUARDRAILS §6`).
- Recommends; does not set prices or policy.

## Stop / escalate
- Never blocks — but a severe flag goes to the GM/human immediately, outside
  the normal brief cycle.
- A number can't be sourced reliably → say so in the brief rather than
  reporting a guess.
