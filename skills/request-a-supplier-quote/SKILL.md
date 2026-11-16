---
name: request-a-supplier-quote
description: Sales/Product — send a supplier (usually the supplier) a quote request that comes back complete the first time. Covers desk routing, what the request must contain, and the five things to demand back. Use when sourcing a package, hotel, transfer or land arrangement from a supplier.
---

# Request a supplier quote

A bad request costs a week. The supplier answers what you asked; if you did not
ask about triple occupancy, you find out at check-in.

## Route it

`memory/supplier-contacts.md` is the routing table. Pick the desk by **product**, never
by whatever address was on the last thread. CC `{{EMAIL}}`.

Land packages by region go to the supplier's destination desks (for example
outbound, regional, Europe, domestic). Air goes to the air desks. Hotels-only reconfirmation
goes to the supplier's operations desk or extranet — extranet if the booking shows a
status code instead of a confirmation number.

## The request must contain

- **Pax count and composition** — adults / children with ages / infants.
- **Exact dates**, city by city, with nights per city.
- **Named hotels with a star rating, plus "or similar"** — naming a property gets
  a real rate; naming only a category gets their cheapest.
- **Room configuration** — number of rooms and occupancy per room, stated explicitly.
- **Meal plan** per hotel.
- **Every activity**, with the transfer type (private vs shared) for each.
- **Transfers** — airport↔hotel, private or shared, per city.
- **Visa and insurance** — ask whether they handle it and what they need from us.
- **Land-only or with air** — say which, and why.

## Demand these five back, every time

1. **Rate with the named hotels**, plus an alternative in each city if unavailable.
2. **Occupancy confirmation** — can the hotel genuinely take the stated occupancy
   on those dates, or is it twin + single? Triple occupancy is the classic failure.
3. **Inclusions and exclusions per component**, and **which areas the shared
   transfers pick up from** — pickup zones are hotel-area specific.
4. **Quote validity** and the cancellation/amendment policy.
5. **Seasonal supplements, blackout dates and surcharges** — now, not later.

## Cross-checks before sending

- **Does the transfer match the hotel's location?** A transfer priced "from
  <Area> hotels" does not apply to a hotel in a different district.
- **Is a flight number actually operated by the marketing carrier?** A codeshare
  flown by a low-cost operator has different baggage and service.
- **Is anything in the itinerary closed?** Attractions close for renovation for
  years. Check before quoting, not after selling.

## Multiple suppliers covering the same region

Check your full supplier directory, not just your main supplier, before assuming there is only
one place to ask. When more than one supplier covers the destination in the quote (e.g. the supplier
destination desk plus one or more private DMCs), send each one its **own separate email** —
never one bundled email to multiple recipients — so replies, negotiation and any
supplier-specific detail stay independent. When there is more than one supplier to contact,
dispatch the drafting/sending as parallel subagent tasks rather than working through them one
at a time.

## Fixed-departure and escorted-tour alternatives

For a holiday/package enquiry, also consult `memory/fixed-departure-operators.md`.
Check the official operator sites that plausibly cover the requested destination
and date window, alongside the supplier and the full regional supplier directory. Use the
brochure links only to identify products; a brochure or headline listing does
not prove a departure is operating, space is available, or the displayed price
is current or complete. Verify exact dates, traveller mix, occupancy,
inclusions, taxes/fees, and payable total from a current official page or written
confirmation. Record the source URL and check time, price currency/basis,
availability evidence, and terms. Keep public operator prices, supplier costs,
and the agency sell prices distinct. Apply the agency's pricing rules before presenting
the agency offer; show sell price only. Never book, hold, sign in, or pay while
researching these alternatives.

## Hard rules

- **Never mention what the client has been quoted elsewhere**, or a target price.
  It anchors the supplier against you.
- **Withhold the client's name** at enquiry stage — names go over at booking.
- **Send per your own rule.** Decide deliberately whether supplier *enquiries* may be emailed directly or must be drafted for a human. Confirming or ticketing a supplier arrangement always needs the owner (GUARDRAILS §2).
