---
name: collect-passenger-documents
description: Customer Care + Operations — collect and verify passenger details for ticketing from IDs shared over WhatsApp or email, with the PII handling rules. Use whenever a customer sends passenger documents or a name list.
---

# Collect passenger documents

Customers send ID photos over WhatsApp. This is how we turn that into a clean,
ticketable manifest without creating a data-protection problem.

## What ticketing actually needs

| Sector | Needs |
|---|---|
| **Domestic India** | Title, full name **exactly as on the ID used to travel**, DOB, gender. The ID *number* is generally **not** required for issuance. |
| **International** | The above plus passport number, nationality, date of issue, **date of expiry**, and issuing country. |

**Therefore: do not transcribe or forward an Aadhaar number for a domestic
ticket.** It is not needed to issue. Collecting and circulating it creates
exposure under the DPDP Act, 2023 for no operational benefit.

## The name rule — the one that costs money

The ticketed name must match the ID presented at the airport. Not the name on a
different family member's card, not a shortened version, not the one on the
booking request.

Watch for:
- **The same person named differently across documents.** One card says "Vijay
  Kumar", a relative's card names him "Vijay Patel". Use **his own** ID.
- **Surname-first vs given-name-first** on Indian IDs.
- **Initials expanded** on one document and not another.

A name change after ticketing is usually prohibited — only a *correction* is
permitted. Getting it right at collection is far cheaper than a reissue.

## Incomplete data — do not fill the gap

Aadhaar cards often show **year of birth only**, not a full date. When that
happens:
- Record it as year-only and **say so**.
- Ask the customer for the exact date if the booking needs it.
- **Never invent a day and month.** A fabricated DOB on a manifest is a
  fabricated record. (GUARDRAILS §10)

## Steps

1. List every passenger from the chat, in order, against the documents received.
2. Extract **Title, Name as per ID, DOB, Gender** — and passport fields if
   international.
3. Reconcile the count. "8 members" and 8 documents should match; if not, say
   which are missing rather than assuming.
4. Flag: name mismatches, incomplete DOBs, expired or near-expiry passports
   (check the 6-month rule for the destination), minors, and anyone needing
   special assistance.
5. Produce the manifest. Hand to Operations for the booking brief.

## PII handling

- Keep documents in the working area for the booking only. Do not copy them into
  the repo, a training file, or a commit.
- Share with a supplier **only the fields that supplier needs to issue** — name,
  DOB, gender; passport details where the sector requires them.
- Do not paste ID numbers into email when they are not required.
- Do not retain documents longer than the booking and its statutory record
  requirement.

## Stop and escalate when

- A passport expires within 6 months of travel.
- A passenger's nationality triggers a permit or prior-approval requirement.
- A document looks altered — do not proceed, and do not accuse; escalate to the owner.
