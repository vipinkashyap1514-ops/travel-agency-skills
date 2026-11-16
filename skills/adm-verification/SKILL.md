---
name: adm-verification
description: Finance & Accounts: verify an incoming ADM/ACM against the original booking and the Operations work-item log, determine an accept-or-dispute position, and assemble the evidence bundle for a human to action.
---

# Playbook: adm-verification

## Owner
Finance & Accounts (with Operations for the technical check)

## When to use
An ADM (Agency Debit Memo) or ACM appears in the HOT file / arrives from an
airline.

## Inputs
- The ADM: ticket number, stated reason code, amount, dispute deadline.
- The original booking + ticketing record.
- The Operations work-item log for that ticket (fare construction / reissue
  working — `operations/16`).

## Steps
1. **Log the ADM** with its reason category and the **dispute deadline** — this
   deadline governs everything; missing it forfeits a valid dispute.
2. **Pull the evidence**: original PNR/ticket, fare calc, the Operations log
   showing which rule/categories were applied and the working.
3. **Handoff → Operations**: "does the ADM's stated reason match what was
   actually done?" Operations re-checks the construction/rule application
   (`operations/16`, `04`, `08`, `09`).
4. **Determine position:**
   - Our record shows the error genuinely occurred → **valid** — prepare to
     accept and process.
   - Our record + working shows we applied it correctly → **disputable** —
     assemble the dispute: the ADM, our fare calc, the rule display, the
     Operations log, a short written rebuttal.
5. **Root-cause tag** — record the cause category (fare/RBD mismatch, rule
   misapplication, commission, reissue miscalc, out-of-sequence…). If a pattern
   emerges across ADMs, flag to Operations to fix the process, not just this
   memo.
6. **Package for a human**: the position (accept/dispute), the amount, and —
   for a dispute — the full evidence bundle and the deadline.

## Handoffs
→ Operations (technical verification). → GM/human (accept/pay or submit
dispute — Finance does not do either itself, `GUARDRAILS §1, §4`).

## Output
```
ADM: <ticket> · reason <code> · amount <x> · dispute deadline <date>
Operations check: matches / does not match what was done — <detail>
Position: ACCEPT | DISPUTE
[Dispute] Evidence bundle: <list>   Rebuttal: <text>
Root-cause category: <x>   Pattern? <y/n>
Human action: pay | submit dispute by <deadline>
```

## Guardrail checks
- Finance prepares; a **human pays or submits** (`GUARDRAILS §1, §4`).

## Stop / escalate
- Dispute deadline is near and the position isn't resolved → escalate now.
- ADM pattern points to a systemic Operations gap → escalate as a process fix.
- Amount large enough to need the owner's sign-off regardless of validity →
  escalate.
