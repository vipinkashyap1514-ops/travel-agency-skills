---
name: price-a-request
description: Product & Contracting: set the actual sell price for a flight, hotel, package, visa, or dummy reservation using the benchmark-vs-B2C-portals concept (flights), [YOUR_PACKAGE_MIN_MARGIN]% minimum (packages), or flat pricing (dummy reservations).
---

# Playbook: price-a-request

## Owner
Product & Contracting (pricing function). In the initial single-operator test
phase, the same session running Sales/Operations runs this too.

## When to use
Any request that needs a sell price: a flight, a hotel, a package, a visa, or a
dummy reservation. Called via handoff from `quote-from-enquiry`, or directly.

## Inputs
- The specific request: exact flight/hotel/package, dates, cabin/room, pax mix.
- **Our cost `C`** — from the supplier / the platform (net, incl. unavoidable fees).
- **Market reference `M`** — the price for the *same thing* on MakeMyTrip and
  other consumer apps. *Until the browsing connector exists, the human supplies
  `M`.*
- `memory/policies.md`, `memory/operating-style.md`.

## FX conversion (foreign-currency net costs — check first)
If `C` (or any component of it) is quoted in a foreign currency — the supplier land
content in MYR, hotel content in USD/AED, etc. — convert it to INR **before**
applying any of the steps below: verify the **current live mid-market rate**
(never assumed/remembered/stale), add a **flat [FX_BUFFER] markup per unit of foreign
currency** on top as the working conversion rate, and use that INR figure as
`C`. This buffer is separate from and stacks with the margin rules below — it
is not counted toward the package margin floor or the benchmark band. Full rule:
`memory/policies.md` § "FX conversion". The working rate and its source/date
are **INTERNAL** (`GUARDRAILS §3`), same as `C`. Can't verify a live rate at
quote time → don't convert off a stale figure, flag it for the human.

## Steps

### A. Flights

**The concept:** quote where the customer saves a bit vs the B2C portals and we
still make money. Everything below is just how to apply that.

1. **Match preferences first.** The flight the customer actually wants — time
   window, non-stop vs connecting, cabin, airline, baggage. Only compare
   against that, never a cheaper option they'd reject.
2. **Our cost `C`** — all-in, from our own portal. Our price doesn't rise at
   checkout; note that as a selling point.
3. **What they'd really pay elsewhere `M`** — the same flight on **MakeMyTrip**
   / other B2C portals, **at checkout** (first-page fare + the convenience fee
   the portal adds by the payment page — a few hundred rupees domestic, more on
   international; our fare stays flat).
   *Until a browsing connector exists, the human supplies the portal fare / `M`.*
4. **Quote `S` between `C` and `M`** — clearly below `M` so the customer saves,
   above `C` so we margin. Round to a clean figure. Example: C 1500,
   M ~1900 → S ~1700–1750 (illustrative).
5. **`C` ≈ `M` (prices close):** take the **minimum margin** — [MIN_MARGIN_DOMESTIC] domestic /
   [MIN_MARGIN_INTL] international (floor, not a visible fee).
6. **Can't beat `M`:** quote at `C` + minimum margin and be upfront, or lead
   with a better-value option — judgement.
7. Record `C`, `M` (with source), `S`, margin. `C` and margin are **INTERNAL**
   (`GUARDRAILS §3`); `S` and "you save ~₹(M−S) vs MakeMyTrip at checkout" are
   shareable.

### B. Packages — cost-plus
1. Sum the net cost of all components — convert any foreign-currency
   component to INR first per "FX conversion" above (live rate + [FX_BUFFER] buffer).
2. Apply **≥ [YOUR_PACKAGE_MIN_MARGIN]%** markup (floor; go higher where the value justifies it) on
   the already-buffered INR cost.
3. No benchmark step required.
4. Net component costs are INTERNAL; only the package sell price is shareable.

### C. Hotels
Same concept as flights: quote below what the customer would pay on MMT /
Booking / Agoda for the same property, room and dates, keeping a margin;
minimum-margin floor if prices are close. (Method to be refined with the owner
after flight pricing is proven.)

### C2. Visa
Markup applies (not pass-through). Treat as a service charge per applicant on
top of the consular/processing cost until the owner sets the exact method — flag
the figure for the human.

### D. Dummy reservations (visa product)
- Dummy flight reservation: **flat [FLAT_FEE_FLIGHT] per passenger per ticket.**
- Hotel itinerary: **flat [FLAT_FEE_HOTEL]** per booking.
- **Integrity check (hard):** what we supply must be a *genuine held booking*
  (real PNR, real TTL, verifiable) or a *clearly-labelled itinerary/quotation*.
  Never a fabricated e-ticket number or a false "confirmed/paid" status
  (`policies.md` integrity rule, `GUARDRAILS` — no fabricated records). If the
  request is for something that would function as a fake document, refuse and
  escalate.

## Handoffs
← Sales (`quote-from-enquiry`). → Operations to confirm fare rules / that the
class is actually available at `C` before the price is trusted.

## Output
```
Item: <flight / hotel / package / visa / dummy>
Our cost C: <amount>            [INTERNAL]
Market ref M (source): <amount, MMT/other>    [M is public]
Sell price S: <amount>
Margin: <S − C or package floor>         [INTERNAL]
Customer saving vs market: <M − S>   [shareable]
Judgement note: <why S sits where it does in the band>
```

## Guardrail checks
- `C`, supplier/nett rate, and the markup amount never reach customer-facing
  text (`GUARDRAILS §3`). The public market comparison may.
- No fabricated reservation documents (§ no fabricated records).
- Pricing is prepared; a human confirms the final sell price and sends.

## Stop / escalate
- Can't establish `M` like-for-like → ask the human for the portal price.
- Price would fall below the minimum margin / below the margin floor on a package →
  escalate.
- Visa/hotel method not yet set → produce the number and flag for the human.
- Any dummy-reservation request that looks like it wants a fake document →
  refuse, escalate.
