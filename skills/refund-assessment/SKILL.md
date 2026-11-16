---
name: refund-assessment
description: Operations: compute an itemised refund breakdown from the fare rule - refundable base, refundable vs non-refundable taxes, penalty, used-value, mechanism and timeline. Use for any cancellation/refund request.
---

# Playbook: refund-assessment

## Owner
Operations (computation) → Finance (execution)

## When to use
A customer requests a cancellation/refund, or Care asks for a refund figure.

## Inputs
- Ticket: fare paid (base + each tax code + amount), fare basis, coupon status
  per segment, form of payment.
- The fare rule (`fare-rule-summary` first if not attached).
- Date of the request (pre- or post-departure).

## Steps
1. **Involuntary check** — is this airline-caused? If yes → `irrops-assessment`
   (penalty waived, full unused value, `operations/10`).
2. **Refundability:** is the base fare refundable at all? Separate **fare** vs
   **tax** — a non-refundable fare can still have refundable government taxes
   (`operations/05`, `11`). Never say "nothing is refundable" without checking
   taxes.
3. **Used vs unused:**
   - Fully unused → refund = fare paid − Cat 16 cancellation penalty − any
     non-refundable taxes.
   - Partially used → compute the **used value** as its own fare (not a
     per-sector proration — `operations/11`), then refund = (fare paid − used
     value) − penalty − non-refundable taxes.
4. **YQ/YR** — refundable only if the fare rule says so; check, don't assume
   parity with base fare.
5. **Penalty timing** — apply the pre- or post-departure Cat 16 figure per the
   request date; no-show is usually worst.
6. **Waiver check** — is there an active airline waiver (disruption, goodwill)
   overriding the standard penalty? (`operations/11`)
7. **Time-limit check** — is the request within the fare's refund window
   (often 12 months from issue/first-flown)? If past, flag.
8. **Mechanism** — BSP refund application vs direct/consolidator vs LCC portal
   (`operations/11`, `31`); state the airline's own stated processing timeline,
   not a generic one.
9. **Write the itemised breakdown** and hand to Finance.

## Handoffs
→ Finance: itemised breakdown to execute the refund (`invoice-from-booking`
sibling process). → Care: the figure and timeline to communicate.

## Output
```
Refund type: voluntary full | voluntary partial | no-show
Refundable base: <fare paid − penalty>
Refundable taxes: <list codes + amounts>
Non-refundable: <YQ / penalty / tax codes kept>
TOTAL refund: <amount>   To: original form of payment
Mechanism: <BSP application | direct | LCC portal>
Airline stated processing time: <x business days>
```

## Guardrail checks
- Operations computes; **Finance executes, a human authorises** (`GUARDRAILS §4`).
- Every line itemised for verification.
- Refund to original form of payment only (`memory/policies.md`).

## Stop / escalate
- Used-value method unclear from the rule → escalate.
- Possible active waiver, unconfirmed → escalate to confirm before quoting.
- Request past the refund time limit → escalate.
- Customer disputes the amount → escalate with the full breakdown.
