---
name: settlement-reconciliation
description: Finance & Accounts: reconcile a BSP HOT file line by line against our records before the remittance date; flag and resolve discrepancies; compute the verified net remittance for a human to pay.
---

# Playbook: settlement-reconciliation

## Owner
Finance & Accounts

## When to use
A BSP billing period has closed and the HOT file is available; run before the
remittance date.

## Inputs
- The HOT file for the period.
- Our booking/ticketing records for the period.
- Product's commission/contract data (`product-contracting/01`).
- Approved refunds for the period (`refund-assessment` outputs, executed).
- Bank statement lines for the period.

## Steps
1. **Line-by-line match** — every HOT file transaction (ticket, refund, EMD,
   ADM/ACM) to a real record in our system (`finance-accounts/01`).
2. **For each ticket:** amount matches the booking; commission matches the
   filed/contracted rate (cross-check Product's data).
3. **For each refund:** matches an approved, executed `refund-assessment`.
4. **Flag every unmatched or mismatched line.** Classify the likely cause
   first (`finance-accounts/07`): timing difference, FX, refund/reissue not yet
   reflected, or genuine error.
5. **Resolve each discrepancy** to matched / corrected / escalated — never
   leave one open silently.
6. **Handle ADMs** in the file via `adm-verification`.
7. **Compute the net remittance** (sales − commission − refunds) and verify it
   against expectation.
8. **Three-way tie-out** — booking platform ↔ HOT file ↔ bank (for what has
   cleared).
9. **Package for the human** who executes the remittance payment: the verified
   net amount, the discrepancy log with resolutions, the deadline.

## Handoffs
→ Operations (any transaction that needs a "what was actually booked" check).
→ GM/human (execute the remittance payment — Finance does not, `GUARDRAILS §4`).

## Output
```
Period: <dates>   HOT file lines: <N>   Matched: <N>   Flagged: <N>
Discrepancies: <list — cause, resolution>
ADMs/ACMs: <list — position per adm-verification>
Net remittance due: <amount>   Remittance deadline: <date>
Trust-account check: cash held vs obligation — <status> (finance-accounts/03)
Human action: execute remittance payment of <amount> by <deadline>
```

## Guardrail checks
- Finance verifies and prepares; a **human pays** (`GUARDRAILS §4`).
- No self-approved reconciliation adjustments (`agents/finance-accounts.md`).

## Stop / escalate
- A HOT file line can't be matched to any booking → escalate.
- Net remittance materially different from expectation → escalate.
- Trust-account balance looks insufficient for the obligation → escalate
  immediately (`finance-accounts/03`).
- Remittance deadline at risk → escalate.
