---
name: document-check
description: Operations: run a passport/visa/health/transit check for a passenger nationality and routing against a current source (TIMATIC/embassy), with the standard disclaimer. Use before finalising any booking brief and whenever Sales/Care asks.
---

# Playbook: document-check

## Owner
Operations

## When to use
Any booking or enquiry where passport / visa / health entry requirements
matter — always run before a booking brief is finalised, and whenever Sales or
Care asks.

## Inputs
- Passenger nationality (passport held) — per passenger.
- Full routing including every transit point.
- Purpose of travel and length of stay.
- Passport expiry date and (if known) issue date / blank pages.
- Travel date.

## Steps
1. **Never answer from memory** (`operations/15`). Look up each requirement in
   a current source: IATA Travel Centre / TIMATIC, or the destination's
   official immigration/embassy source. Record the **source and the date
   checked**.
2. **Passport validity** — check against the destination's rule (commonly
   6 months beyond entry/exit). Compute pass/fail explicitly against the travel
   dates. Flag blank-page and machine-readable/e-passport requirements.
3. **Visa** — determine category for this nationality → destination → purpose:
   visa-free / visa-on-arrival / eVisa/ETA / visa-in-advance. Note processing
   time if visa-in-advance (feeds Sales lead-time).
4. **Transit** — for **each** transit point, check TWOV eligibility for this
   nationality; some need a transit visa even without leaving airside.
5. **Health** — yellow-fever certificate requirement (based on countries
   visited/transited), any other mandatory vaccination certificate (ICVP).
6. **Other entry requirements** — digital arrival card, APIS/ETA-type
   pre-registration, proof of onward/return ticket, funds proof.
7. **Assemble the structured answer** + attach the standard disclaimer
   (`operations/15`) verbatim.

## Handoffs
→ Sales: if a visa needs lead time, or the passport fails validity — this
changes the booking timeline. → Care: if a document problem is found on an
existing booking.

## Output
```
Per passenger (nationality):
  Passport validity: PASS / FAIL vs <destination rule> for travel <dates>
  Blank pages / e-passport: <requirement>
  Visa: <category> — <processing time if advance>
  Transit <point>: <requirement>   [repeat per point]
  Health: <yellow fever / other certificate requirement>
  Other: <arrival card / pre-registration / onward-ticket proof>
  Source: <TIMATIC / embassy> checked <date>
+ standard disclaimer (verbatim)
```

## Guardrail checks
- Advice only; traveller is responsible; entry decision rests with destination
  immigration — disclaimer attached every time (`operations/15`).
- No guarantee of entry.

## Stop / escalate
- Passport fails the validity or blank-page check → escalate + flag to Sales/
  Care immediately.
- Sources disagree, or an unusual transit-nationality combination → escalate.
- Anything touching asylum / refugee travel documents / dual nationality
  complexity → escalate.
- A health-certificate requirement the traveller may not be able to meet in
  time → escalate.
