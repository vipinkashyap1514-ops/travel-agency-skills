---
name: pricing-request-response
description: Product & Contracting: answer a pricing handoff from Sales or Marketing with 2-3 net+sell options and full conditions. Use when asked to source/price a routing, dates, or package.
---

# Playbook: pricing-request-response

## Owner
Product & Contracting

## When to use
A HANDOFF REQUEST from Sales or Marketing asking to price a routing / dates /
package.

## Inputs
- The routing, dates, pax mix, cabin, and any preference from the requester.
- Access to: contracted/nett fares + tour codes, consolidator rates, the
  hotel/land catalogue, live API rates (e.g. the supplier), the package catalogue.

## Steps
1. **Restate the ask** in one line to confirm scope (O&D, dates, pax, cabin).
2. **Gather candidate sources** for each component:
   - Air: direct contract (tour code), consolidator, API nett — compare, don't
     take the first result (`product-contracting/02`).
   - Hotel/land: static contracted rate (check age vs refresh cadence —
     `product-contracting/04/07`) and/or live API rate.
3. **For each viable option compute:** net cost → if any component is in a
   foreign currency (the supplier/other supplier in USD, MYR, AED, etc.), convert to
   INR first by verifying the **current live mid-market rate** (never
   assumed/remembered/stale) and adding a **flat [FX_BUFFER] markup per unit of
   foreign currency** as the working rate — this FX buffer is separate from
   and stacks with the markup, not counted toward it (`memory/policies.md` §
   "FX conversion") → apply markup per `memory/policies.md` on the
   already-buffered INR cost → **sell price**. If policy markup fields are
   blank, escalate rather than guessing. Working rate/source/date is
   INTERNAL, same as net cost.
4. **Assemble 2–3 options** at different value points. Per option record, for
   the requester:
   - **Sell price** (shareable downstream)
   - **Net cost + source + tour code** (marked INTERNAL — never flows to
     customer-facing text, `GUARDRAILS §3`)
   - Conditions: cancellation cutoff (exact date/time), inclusions/exclusions,
     validity/expiry, any source-specific quirk (earlier TTL, consolidator
     refund process — `operations` needs this).
5. **Write the HANDOFF RESPONSE** per `handoffs/protocol.md`, clearly marking
   which fields are shareable vs internal.
6. **Log** sources compared and why the recommended option was chosen.

## Handoffs
← Sales / Marketing (the request). May consult Operations to pre-confirm fare
rules on a contract fare.

## Output
A HANDOFF RESPONSE with 2–3 priced options, net marked internal, sell marked
shareable, full conditions, appended to the work item.

## Guardrail checks
- Net cost is labelled INTERNAL and never placed where it could reach a
  customer (§3).
- No contract commitment made (`agents/product-contracting.md`).

## Stop / escalate
- Policy markup/discount fields blank → escalate.
- Two sources quote materially different net for the same routing → investigate
  before choosing; note in the response.
- Only a stale static rate is available and it's needed for a live quote →
  escalate / refresh first.
- A foreign-currency net cost needs converting and the live FX rate can't be
  verified at quote time → do not use an assumed/remembered rate, escalate /
  get the current rate from the human first.
- The ask needs a new supplier or contract → escalate.
