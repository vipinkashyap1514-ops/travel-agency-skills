---
name: handle-a-group-booking
description: Operations + Product — take a 10+ passenger air request from enquiry to a sourced, quoted group block. Covers why a group cannot be booked like a normal PNR, group-fare mechanics, deposit and name-deadline risk, and the split-PNR fallback. Use for any request of 10 or more passengers on one routing.
---

# Handle a group booking (Vikram sources · Priya prices · the owner commits)

**Ten passengers is a hard boundary, not a guideline.** Everything below exists
because a group behaves nothing like a larger normal booking.

## Why 9 is a wall

**Not for the reason usually given.** A PNR does *not* hold only 9 names —
Travelport documents **99** per booking file, and Amadeus permits 9 seated
passengers **plus 9 lap infants (18 humans)** in one record. If it were a
name-field limit, an infant would consume one.

The real 9 sits in **three other places at once**:

- **The shopping/sell transaction.** Amadeus: *"Number of seats bookable in a
  single request. Can not be higher than 9."* Travelport: *"A maximum of 9
  passengers can be included in each transaction."* You cannot **request** more
  than 9 seats at a time — a seat-request limit, not a name-storage limit.
- **Inventory.** Revenue management will not release 30 seats into a discount
  bucket. This is the constraint that actually binds, and no standards change
  touches it.
- **The tariff.** 10+ is a different fare product almost universally — deposit,
  deferred names, percentage allowances.

Nine is simply where a booking stops being a retail transaction and becomes a
negotiated one. See `training/operations/pnr-9-pax-limit-explainer.md`.
- Even if you could seat 33 names, **the inventory would not sell.** Under nested
  RBD control the authorisation level in a low class on a peak date is a handful
  of seats. 33 pax is ~17–18% of a narrowbody cabin. Revenue management declines
  that in a discount class.
- **Group inventory is a separate pool**, released manually by the airline's group
  desk against a quoted fare, outside the RBD nesting that governs normal sale.

## Route it correctly

Per `memory/supplier-contacts.md` — **carrier type first, then pax count**:

- **LCC group** (IndiGo, Akasa, Air India Express, SpiceJet) → `{{EMAIL}}`
- **GDS group** (full-service) → `{{EMAIL}}` (0900–1800 only)
- Or direct to the airline's own group desk where one exists.

Never send a group to the transactional desk. CC `{{EMAIL}}`.

## Group fare vs published fare — what actually differs

| | Published | Group |
|---|---|---|
| Price | Filed, auto-priced, live | **Manually quoted** against a released block |
| Guarantee | Until TTL | Quote valid a stated number of days |
| Inventory | Nested RBD | **Block outside the nesting** |
| Names | At booking | **Deferred** to a names-by deadline |
| Deposit | None | **Non-refundable**, to hold the block |
| Seat release | n/a | Unnamed/unpaid seats **auto-release** at milestones |
| Cancel | Per-ticket penalty | **% allowance**, then total loss |
| Name change | Usually prohibited | **% allowance**, by deadline |

## The two numbers that decide the commercial risk

Get these in writing before anyone pays anything, and put them to the customer
**at enquiry stage, not at deposit stage**:

1. **Free-cancellation allowance** — typically a % of the group, by a fixed date.
   On 33 pax a 10% allowance is 3 people. A leisure group routinely loses 4–6.
   Beyond the allowance the money is gone.
2. **Name-change allowance** — also a %, with its own deadline.

Compute the actual date and the actual head count, and state them. "10% at D-10"
means nothing to a customer; "3 people, free until 12 January" does.

## Steps

1. **Confirm the basics in writing** — year, exact adult/child/infant split,
   dates firm or flexible, all-Indian or any foreign nationals.
2. **Verify the flights exist.** Read the schedule display and the **days-of-
   operation string**, not the availability screen. A thin route may not operate
   on the requested dates at all.
3. **Assess capacity honestly.** Peak season, long weekends and thin routes make
   33-in-one-bucket unlikely. Say so before the customer forms an expectation.
4. **Raise the group request** to the correct desk with the full brief.
5. **Get the written quote** with deposit %, names-by date, TTL, release
   milestones and the two allowances above.
6. **Hand to Priya to price.** Package markup rules apply; the deposit exposure
   is the owner's decision, not Priya's.
7. **Track every milestone.** A missed names-by date releases seats silently.

## The split-PNR fallback — and why it is a fallback

Mechanically you can book 33 as 4×9 + 1×6. Consider it **only** if the group
quote is rejected *and* availability demonstrably shows the seats in one bucket.

Against it: names required up front; name change normally prohibited (correction
only); per-ticket penalties 33 times; mixed fares if buckets step up — different
prices for the same seat on one group; seats scatter; DCS treats them as
unrelated parties.

**And the hard one:** creating multiple PNRs speculatively to hold seats while the
customer decides is **churning**. It is a real ADM exposure. Do not do it.

## Stop and escalate when

- Any passenger is a foreign national on a restricted-permit route → stop, check
  entry rules before quoting.
- The customer's name-list date is later than the group desk's deadline → that is
  a dealbreaker; surface it before the deposit, not after.
- The deposit is non-refundable and the customer is not ready to commit → there is
  no point raising the request.
