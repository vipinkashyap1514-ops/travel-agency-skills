---
name: invoice-from-booking
description: Finance & Accounts: draft a customer invoice or receipt from a booking brief or reissue computation, with correct revenue classification and tax treatment. Draft only - a human issues it.
---

# Playbook: invoice-from-booking

## Owner
Finance & Accounts

## When to use
A booking brief is accepted / a reissue amount is computed and the customer
needs an invoice or receipt.

## Inputs
- The booking brief (or `compute-reissue` / `refund-assessment` output).
- `memory/policies.md` (service fee, payment terms), `memory/company-profile.md`
  (tax registration, invoicing entity).
- The revenue model for the booking: commissionable vs nett
  (`finance-accounts/04`).

## Steps
1. **Confirm the amounts** from the source document — sell price, service fee,
   any add-ons, any ADD COLLECT/penalty for a reissue.
2. **Classify the revenue** (`finance-accounts/04`): commissionable
   (pass-through fare + our commission/fee) vs nett (sell price, margin =
   sell − nett). Record which.
3. **Tax treatment** (`finance-accounts/05`): apply GST on the service
   fee/margin per current classification. **Flag if the booking looks
   TCS-in-scope** (outbound package) for confirmation — do not compute TCS on a
   guessed rate.
4. **Build the draft invoice**: invoicing entity, customer, line items
   (transparent about what's fare vs service fee), currency, tax lines,
   total, payment terms and due date, accepted payment methods.
   - **No supplier net rate anywhere on the invoice** (`GUARDRAILS §3`).
5. **Trust-accounting note** (`finance-accounts/03`): mark the customer receipt
   as held-for-remittance until ticketed/settled — not recognised revenue yet.
6. **Place the draft invoice in the review queue** for a human to issue.

## Handoffs
← Sales (booking brief) / ← Operations (`compute-reissue`). → escalate
TCS-in-scope confirmation.

## Output
A draft invoice/receipt in the review queue with revenue model and tax
treatment recorded on the work item.

## Guardrail checks
- Finance drafts; a **human issues** the invoice and **executes** any
  collection (`GUARDRAILS §1, §4`).
- No net rate on customer-facing documents (§3).
- No card details handled (§7).

## Stop / escalate
- TCS-in-scope status unclear → escalate, don't apply a guessed rate.
- Revenue model ambiguous / undocumented → escalate.
- Amount on the brief doesn't reconcile with Operations' figures → resolve
  before drafting.
