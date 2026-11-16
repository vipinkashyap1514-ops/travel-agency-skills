---
name: booking-brief-to-ticketing-instruction
description: Operations: convert an accepted booking brief into the exact, GDS-agnostic steps a human executes to book and ticket - segments, SSRs, ticketing arrangement, expected price, do-not-issue-until conditions.
---

# Playbook: booking-brief-to-ticketing-instruction

## Owner
Operations

## When to use
Sales has handed over an accepted booking brief and it needs to become the
exact steps a human executes to book/ticket.

## Inputs
- The booking brief (`sales-reservations/08` format).
- Fare rules / reissue calc as applicable (from `fare-rule-summary` /
  `compute-reissue`).
- Passenger document data (SSR DOCS).

## Steps
1. **Verify the brief is complete** — every field in the
   `sales-reservations/08` template filled. If not, bounce it back; do not
   proceed on assumptions.
2. **Re-validate the fare** right now — still on sale, required RBD open
   (`operations/24/25`). If it moved, flag to Sales before continuing.
3. **Confirm interline / e-ticketing feasibility** end to end if multi-carrier
   (`operations/07/14`); flag if any sector isn't e-ticketable together.
4. **Confirm document data** is present for SSR DOCS / APIS (`operations/26`)
   so it won't fail at the DCS later.
5. **Write the instruction** — unambiguous, GDS-agnostic (`operations/17`):
   - Segments to sell (flight, date, class), in what order.
   - SSRs to add (DOCS, meals, WCHR, FQTV — `operations/19`).
   - Ticketing arrangement / TTL to set.
   - Expected price: base fare basis + expected total + the module-05 tax
     breakdown attached.
   - For a reissue: the exchange details, ADD COLLECT amount, penalty, new fare
     calc line, new endorsements.
   - Explicit **"do not end / do not issue until <condition>"** where payment
     or a customer confirmation must land first.
6. **Place the instruction in the review queue** for a human to execute.

## Handoffs
→ Finance: the amount to invoice/collect. → Sales: any fare re-validation
issue.

## Output
```
Booking: <ref / work item>
Sell: <segment | flight | date | class | order>
SSR: <codes + free text>
Ticketing arrangement: <TTL date time tz>
Expected price: <fare basis> → <total> (tax breakdown attached)
[Reissue only] Exchange: <old ticket> · ADD COLLECT <amt> · penalty <amt> · new FCL <...> · endorsements <...>
DO NOT issue until: <condition>
```

## Guardrail checks
- Operations writes the instruction; a **human sells and issues**
  (`GUARDRAILS §2`).
- No net rate in anything customer-facing derived from this (§3).
- Price shown with full working for ADM prevention (`operations/16`).

## Stop / escalate
- Brief incomplete → bounce, don't proceed.
- Fare moved / RBD closed since quote → flag to Sales, hold.
- Not interline-eticketable end to end → escalate.
