---
name: handle-complaint
description: Customer Care: take an inbound complaint to a fast acknowledgement and an accurate, correctly-scoped resolution draft within SLA, escalating what needs a human.
---

# Playbook: handle-complaint

## Owner
Customer Care

## When to use
A work item of type "complaint", or any inbound where the customer is
dissatisfied.

## Inputs
- The complaint message.
- The booking record and any prior cases for this customer.

## Steps
1. **Acknowledge within 15 min** (`ORG.md` SLA) — draft a short receipt to the
   review queue confirming it's being looked at. Don't wait for the full
   answer.
2. **Check for signals** first (`customer-care/05`): safety / distress /
   medical / minor → escalate immediately, in parallel, before working the
   case.
3. **Understand** — read the full booking record and prior contacts before
   drafting anything substantive (`customer-care/01`). Never respond to a
   complaint without reading the record.
4. **Establish the facts** — what actually happened per our systems. If it
   involves fare/ticket detail → handoff to Operations. If money → handoff to
   Finance / `refund-assessment`.
5. **Draft the resolution** (`customer-care/02`):
   - Reflect the specific problem back (proves it was read).
   - Own our part plainly; be accurate about who caused what.
   - State the concrete fix + a real timeline (from Operations/Finance, not a
     guess).
   - One clear next step.
   - Separate apology from any monetary gesture — the latter is an escalation.
6. **Place the draft in the review queue.** Update the case log
   (`customer-care/08`).
7. **Set a follow-up** to confirm the resolution actually landed.

## Handoffs
→ Operations (fare/ticket facts, amendment feasibility) · → Finance (refund
eligibility/amount via `refund-assessment`).

## Output
A drafted acknowledgement (fast) and a drafted resolution (within SLA) in the
review queue, plus a complete case log entry.

## Guardrail checks
- Nothing sent — drafts only (`GUARDRAILS §1`).
- No compensation / refund / goodwill with monetary value promised — escalate
  (`agents/customer-care.md`).
- No booking change or money movement by Care (§2, §4).

## Stop / escalate
- Safety / distress / medical / minor → immediately, before working the case.
- Any monetary gesture.
- Legal threat or chargeback mention.
- Second failure on the same case.
- Operations/Finance can't answer within the SLA window → escalate rather than
  let the acknowledgement go stale.
