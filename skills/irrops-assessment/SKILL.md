---
name: irrops-assessment
description: Operations: assess an airline-caused change (schedule change, cancellation, denied boarding, missed connection) - prove involuntary status, entitlement under Resolution 830, fee-free rebooking/refund options, endorsement text.
---

# Playbook: irrops-assessment

## Owner
Operations

## When to use
An airline-caused change to a booking: schedule change, cancellation, denied
boarding, missed connection due to airline delay.

## Inputs
- Original ticketed flights (numbers, times).
- The current airline schedule / notification.
- The fare rule and ticket details.

## Steps
1. **Prove involuntary status** — put ticketed flights next to the current
   airline schedule. Document the exact delta (time shift, cancellation,
   equipment-only change). An equipment swap with no schedule change is
   generally **not** involuntary for fare purposes (`operations/10`, scenario
   S10 in `operations/22`).
2. **Classify** — minor schedule change / significant schedule change /
   cancellation / denied boarding / missed connection.
3. **Determine entitlement** under the fare rule + **Resolution 830**
   (`operations/10`):
   - Rebook on next available (own carrier), fee-free, no less favourable
     class.
   - Reroute on another carrier where an interline agreement allows
     (`operations/14`).
   - **Involuntary refund** — full unused value, **no Cat 16 penalty**, taxes
     refunded.
4. **Compensation** (denied boarding, long delay) — identify which regime
   applies by flight jurisdiction (EU261 / UK261 / US DOT / India DGCA CAR).
   **Do not quote a compensation amount** unless the rule is unambiguous — flag
   to Care as a rights-framework question (`customer-care/04`).
5. **Build the rebooking options actually available** — real flights, correct
   class, with the "no less favourable" test applied.
6. **Endorsement text** — fee-free basis, e.g. "INVOL RRTE/REFUND PER RES 830".
7. **Write the assessment** for Care to communicate and a human to execute.

## Handoffs
→ Care: entitlement + options + endorsement, for the customer message
(`schedule-change-notice`). → Finance: if an involuntary refund is chosen, the
full-unused-value figure. → escalate compensation questions.

## Output
```
Involuntary: YES (delta: <describe>) | NO (reason)
Classification: <type>
Entitlement: rebook free | reroute other carrier | involuntary refund (full unused, no penalty)
Rebooking options: <list, with class>
Compensation regime: <EU261 / DOT / DGCA CAR / none> — see Care
Endorsement: <fee-free text>
Human action: <exact rebook/refund steps>
```

## Guardrail checks
- No Cat 16 penalty or change fee applied to an airline-caused change.
- Operations does not rebook or refund — prepares it (`GUARDRAILS §2, §4`).
- No compensation amount promised unless the rule is unambiguous.

## Stop / escalate
- Voluntary vs involuntary genuinely unclear → escalate.
- Denied-boarding / compensation claim → escalate (jurisdiction-specific).
- Duty-of-care costs (meals/hotel) requested → escalate for approval.
- Multi-carrier itinerary where fault is unclear → escalate.
