---
name: quote-from-enquiry
description: Sales & Reservations: turn a customer travel enquiry into a tiered, compliant, ready-to-send quote. Use when a work item of type enquiry is routed to Sales.
---

# Playbook: quote-from-enquiry

## Owner
Sales & Reservations

## When to use
A work item of type "enquiry" has been routed to Sales.

## Inputs
- The enquiry text.
- `memory/company-profile.md`, `memory/policies.md`, `memory/tone-of-voice.md`.

## Steps
1. **Build the discovery brief** (`sales-reservations/01`). Required fields:
   pax + ages, dates (and flexibility), origin/destination (exact airports),
   budget signal, purpose, cabin preference, passport nationality, known
   constraints. **If any required field is missing, ask the customer — draft
   the question to the review queue — before proceeding.**
2. **Feasibility pre-check:** routing physically possible (MCT — `operations/02`)?
   Nationality/destination likely document issue (`operations/15`)?
   Special-category lead time needed (`operations/19`)? Flag any now.
3. **Handoff → Product** (`pricing-request-response`): request net+sell options
   for the routing/dates, 2–3 fare/product levels. For holiday or escorted
   package enquiries, include a check of relevant official fixed-departure
   operators in `memory/fixed-departure-operators.md`, alongside the supplier and the
   applicable regional supplier directory; compare only current, verified
   departures and mark any advertised price that is not a confirmed total or
   available option.
4. **Handoff → Operations** (`fare-rule-summary`): for each option Product
   returns, request the rule summary (Cat 6/7 stay, Cat 16 change/refund, TTL,
   whether filed or dynamic — `operations/29`).
5. **Handoff → Finance** (if payment terms non-standard, e.g. corporate/sub-agent):
   confirm terms.
6. **Assemble 2–3 tiers** (`sales-reservations/03`): value / balanced / premium.
   Per tier: sell price only (never net — `GUARDRAILS §3`), inclusions,
   exclusions, rule summary, explicit quote expiry, single next step.
7. **Draft the quote email** in house tone. End with what's held vs not held,
   the expiry date/time, and one next step. **If this is going out as a
   branded package document (a PDF), not just inline text, follow
   `brand-a-customer-package`** — a welcome message with the guest's actual
   name and destination imagery are both required, not optional polish.
8. **Place the draft in the review queue.** Update the work item.

## Handoffs
→ Product (pricing) · → Operations (fare rules) · → Finance (payment terms, if
non-standard).

## Output
A drafted, tiered quote email in the review queue + the work item updated with
all handoff responses attached.

## Guardrail checks
- No net rate or markup math anywhere in the draft (§3).
- No guarantee of price/availability before ticketing.
- No superlatives (`tone-of-voice`).
- Nothing sent — draft only (§1).

## Stop / escalate
- Discount requested/needed beyond policy authority → escalate.
- Cheapest viable option far above stated budget → say so in the draft, don't
  pad a quote you expect to disappoint.
- Operations flags an ambiguous rule → don't paraphrase around it; hold and
  escalate.
