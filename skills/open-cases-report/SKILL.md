---
name: open-cases-report
description: Daily report of every open travel request (came in, not came, sent to customer, pending), with follow-ups drafted for the owner. Use for "open cases", "status of requests", or the daily run.
---

# Open cases report ()

Output: `review-queue/open-cases-report.md`. Rewrite it each run and list what changed since last time.

## Sections
1. Came in from the supplier (reply received)
2. Asked of the supplier, no reply yet
3. Sent to the customer, waiting for yes/no
4. Customer said yes, needs sending to the supplier or ticketing
5. Pending on the agency / the owner
6. Gaps (what was not checked)

## Sources
- Mailbox: the supplier threads (`list_mails`, includeSent). Reply on the same thread, same subject and case number.
- `memory/trips-tracker.md`, `review-queue/`, `work-items/`.
- WhatsApp: only chats of named customers. Never sweep the chat list, it has personal and family chats.

## Follow-ups
- Do not cc anyone on supplier mail unless the owner says so.
- No reply from the supplier after 1 working day: draft a chaser on the same thread (supplier enquiry emails send directly).
- No reply from a customer after 2 days: DRAFT the follow-up for the owner. WhatsApp sends only when the owner asks for that message (automations are off).
- Customer says yes: send the supplier a confirmation request on the same thread with trip details only. Ticketing, payment and the final confirm stay with the owner.

## The wall
- Customer sell prices never go to the supplier.
- the supplier net or offered rates never go to the customer.
- Before any fare goes on WhatsApp: compare online fares, tell the owner the difference, wait for his fare.
