---
name: fare-rule-summary
description: Operations: translate a filed fare rule (or dynamic offer conditions) into a plain-language summary for Sales/Care/Finance - min/max stay, change/refund penalties, TTL, validity. Use when asked what are the rules on this fare.
---

# Playbook: fare-rule-summary

## Owner
Operations

## When to use
A HANDOFF REQUEST asking "what are the rules on this fare" — from Sales
(quoting), Care (amendment/refund question), or Finance (ADM check).

## Inputs
- The fare basis / offer reference, routing, dates, pax type.
- Access to the filed fare rule display (GDS `FN`/`RD`/`FQN`) or, for a
  dynamic offer, the offer's stored attributes.

## Steps
1. **Identify the fare type** (`operations/03`, `29`, `30`): filed fare,
   class-based dynamic, or dynamic/continuous offer. State which — it changes
   how much is knowable in advance.
2. **If filed:** read the rule categories and extract:
   - Cat 3 seasonality · Cat 5 advance purchase · Cat 6 min stay · Cat 7 max
     stay · Cat 8 stopovers · Cat 11 blackout
   - **Cat 16** — change fee (before/after departure), refund penalty
     (before/after departure), **no-show treatment**, per-direction vs
     per-transaction (`operations/08` — state all four dimensions)
   - Combinability (Cat 10) if the itinerary combines components
3. **If dynamic/offer:** capture the offer's stated change/refund conditions
   and expiry verbatim — take a snapshot now, it may be hard to retrieve later
   (`operations/29`).
4. **Determine the TTL** (`operations/08`): airline rule vs GDS default vs
   agency buffer — the earliest wins. State date/time **with timezone**.
5. **Confirm fare validity right now** — is it still on sale, is the required
   RBD actually open (`operations/24/25`)? Note if not.
6. **Write the HANDOFF RESPONSE** in the standard rule-summary block
   (`operations/08`).

## Handoffs
← the requester. No outward handoff normally.

## Output
```
Fare basis / offer: <ref>       Type: filed | class-dynamic | dynamic offer
Cat 6 min stay: <x>   Cat 7 max stay: <x>   Cat 5 adv purchase: <x>
Cat 3 season: <dates>   Cat 8 stopovers: <x>   Cat 11 blackout: <dates>
Cat 16 change: <fee, before/after dep>
Cat 16 refund: <fee, before/after dep, no-show>
Combinability: <notes>
TTL: <date time tz>     Fare guarantee: only once ticketed
Validity now: <on sale? RBD open?>
```

## Guardrail checks
- Advice only — no state change (`GUARDRAILS §2`).
- If any category text is ambiguous, say so — do not smooth over the gap.

## Stop / escalate
- Rule text ambiguous or self-contradictory → escalate.
- Required RBD closed / fare withdrawn → flag to requester, don't proceed as if
  available.
