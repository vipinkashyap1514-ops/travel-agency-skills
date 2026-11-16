---
name: compute-reissue
description: Operations: compute a voluntary change to a ticketed booking - revalidation vs reissue, fare difference/ADD COLLECT, penalty, tax delta, new TTL, endorsements. Use when a customer wants to change a ticketed flight and it is not airline-caused.
---

# Playbook: compute-reissue

## Owner
Operations

## When to use
A customer wants a **voluntary** change to a ticketed booking (date, routing,
class). (Airline-caused → `irrops-assessment` instead.)

## Inputs
- Original ticket: fare paid (base + taxes itemised), fare basis, routing,
  coupon status per segment, endorsements.
- The requested new itinerary.
- The fare rule (run `fare-rule-summary` first if not already attached).

## Steps
1. **Confirm it's voluntary** — check ticketed flights vs current airline
   schedule. If the airline changed something, stop and use
   `irrops-assessment` (`operations/10`).
2. **Revalidation or reissue?** (`operations/09`) — if only date/flight moves,
   same fare, within rule limits, same carrier → check if **revalidation** is
   permitted (no fare recalc, no Cat 16 penalty). If yes, prepare that and skip
   to step 6.
3. **Reissue calculation:**
   a. Price the **new itinerary** at today's fare, same class the customer
      wants, subject to RBD availability (`operations/24`).
   b. Identify **used vs unused** coupons — reissue math applies only to the
      unused portion.
   c. **Fare difference:**
      - new > old → **ADD COLLECT** = difference
      - new < old → residual normally **forfeited** unless the fare rule allows
        a residual/EMD credit — state explicitly (`operations/09` — the common
        expectation gap)
   d. **Cat 16 change penalty** — apply per rule (once / per direction).
   e. **Tax delta** — re-verify taxes for the new itinerary at current rates
      (`operations/05`); don't carry old taxes over.
4. **New TTL** for the reissued segments (`operations/08`).
5. **Endorsements** — update to reflect remaining restrictions + the exchange.
6. **Write the exact instruction** for a human to execute (revalidation entry,
   or reissue with ADD COLLECT amount, penalty, new fare calc line) — see
   `booking-brief-to-ticketing-instruction` format.

## Handoffs
→ Finance: the amount to collect from the customer (ADD COLLECT + penalty + tax
delta) for invoicing. → Care: the customer-facing explanation of cost + why.

## Output
```
Change type: revalidation | reissue
Fare difference (ADD COLLECT): <amount>   Residual forfeited: <yes/no + why>
Cat 16 change penalty: <amount, basis>
Tax delta: <amount>
TOTAL due from passenger: <amount>
New TTL: <date time tz>
New endorsements: <text>
Human action: <exact revalidation/reissue steps>
```

## Guardrail checks
- Operations does **not** reissue, revalidate, or collect payment
  (`GUARDRAILS §2, §4`) — it produces the calculation and the steps.
- Show every line of the math for human/audit verification (`operations/16`).

## Stop / escalate
- Revalidation vs reissue unclear from the rule → escalate.
- Required RBD not available at the requested fare → flag; the customer is
  pricing into a different bucket.
- Multiple pax on one PNR, only some changing → a split may be needed
  (`operations/06`) — flag.
- Residual-credit question with no clear rule answer → escalate.
