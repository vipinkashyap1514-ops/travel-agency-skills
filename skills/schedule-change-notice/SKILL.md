---
name: schedule-change-notice
description: Customer Care: draft a proactive customer message for a confirmed disruption, using the Operations irrops-assessment output. Use after Operations has confirmed a schedule change/cancellation on an active booking.
---

# Playbook: schedule-change-notice

## Owner
Customer Care

## When to use
Operations (via `irrops-assessment`) has confirmed a disruption on an active
booking and the customer needs to be told.

## Inputs
- The `irrops-assessment` output: involuntary status, classification,
  entitlement, rebooking options, endorsement.
- The booking and customer contact record.

## Steps
1. **Confirm you have the Operations assessment** — do not draft a disruption
   message from the customer's framing alone (`customer-care/03`).
2. **Draft the message** with this structure:
   - **What happened** — old flight vs new flight/status, factually.
   - **What it means for them** — new arrival time, connection impact, any
     action needed.
   - **Their options** — exactly as Operations confirmed (rebook free /
     alternate routing / involuntary refund). Never add an option Operations
     didn't confirm.
   - **What we're doing** — proactively holding/booking the best option,
     monitoring.
   - **Next update** — when they'll hear from us again if not resolved.
3. **Tone** (`customer-care/03`): proactive and practical — lead with impact,
   not a heavy apology; it wasn't necessarily anyone's fault.
4. **Place the draft in the review queue.** Log the case.
5. If the customer will **miss something time-critical** (connecting cruise,
   event) → escalate for faster-than-SLA human attention.

## Handoffs
← Operations (`irrops-assessment`). → escalate compensation questions to the
rights-framework path (`customer-care/04`).

## Output
A drafted proactive disruption message in the review queue + case log entry.

## Guardrail checks
- Draft only (`GUARDRAILS §1`).
- Options limited to what Operations confirmed.
- No compensation amount stated (unless Operations flagged the rule as
  unambiguous).

## Stop / escalate
- No Operations assessment yet → get it first.
- Customer will miss a time-critical downstream booking → escalate.
- Group / high-value booking affected → escalate.
- Duty-of-care costs in play → escalate.
