---
name: brand-a-customer-package
description: Sales & Marketing — turn a priced itinerary into a branded, personalized PDF package for a named customer, with destination imagery and a welcome message. Use whenever a quote or proposal is going out as a document, not just an email.
---

# Playbook: brand-a-customer-package

## Owner
Sales (assembles and sends) with Marketing (imagery/copy on request). 

## Standard — non-negotiable for any branded package
1. **A welcome message, addressed to the guest by name**, on the cover or
   opening page. Not "Dear Guest" — the actual name(s) given for the booking.
   If no name has been given yet, ask before building the document rather than
   guessing or leaving a placeholder that could ship by accident.
2. **Destination imagery — real photography only, of the actual recognizable
   landmark, not illustrated/painted art.**
   - Use a **real photo of the destination's iconic, instantly-recognizable
     landmark** — the Eiffel Tower for Paris, Tower Bridge for London, the
     Petronas Towers or KL Tower for Kuala Lumpur, Dal Lake's houseboats for
     Srinagar, and so on. Pick the single most recognizable shot for that
     city, not a generic street or hotel photo.
   - Source from a **free-to-use/commercially-licensed stock source**
     (Unsplash, Pexels, Pixabay, or similar) via the browser — verify the
     license allows commercial use before embedding. Never scrape an
     arbitrary web image (a random blog, a hotel's own marketing photo, a
     search-engine image result of unclear origin); that's a real copyright
     exposure on a document with the company's name on it.
   - **Style the photo Apple-Inc-classy**, not a raw stock-photo drop-in: a
     full-bleed hero crop, a dark gradient scrim for text legibility, clean
     minimal typography over it (Fraunces/Archivo per the design system
     below), generous negative space, one clear price/CTA — not a busy
     collage or a stock-photo-with-a-sticker-on-it look.
   - One strong photo per destination/city covered, placed near that
     destination's itinerary section (packages) or as the single hero
     (banners) — not a generic stock image on the cover only.
   - Applies to **both** customer-facing packages (PDF) and marketing banners
     — same rule, same sourcing method, no exceptions by document type.
3. **Check the travel dates against notable occasions before building the
   itinerary, and reflect any that fall inside the trip.** Public holidays,
   major festivals (Christmas, New Year, Diwali, Eid, Chinese New Year —
   whatever's relevant to the destination and the likely traveller), and any
   date the customer has flagged as significant (an anniversary, a birthday
   mentioned in the enquiry). When one falls inside the travel window:
   - Give that date its **own day entry**, not folded into a generic
     multi-day "at leisure" block — a customer who's spending Christmas or
     New Year's Eve on the trip should see that day named as such.
   - Give it a **small, distinct illustration** (a day-icon, not a full
     destination banner) that reflects the occasion specifically — a
     Christmas motif for 25 Dec, fireworks for New Year's Eve, and so on —
     not a generic day marker recoloured.
   - This is a "check first" step, not a "only if convenient" one — read the
     travel dates against a calendar before building the day-by-day, the
     same way pricing checks dates against seasonal surcharges.
4. **Small, day-specific illustrations belong throughout the itinerary, not
   only on occasion days.** Each day's icon should be genuinely tied to that
   day's actual activity (a boat for a river cruise day, a cable car for a
   cable-car day, an aquarium motif for an aquarium day) — not a repeated
   generic icon or a full-size image squeezed small. The standard is
   "meaningful and personalised per day," not "decorative."


5. **Practical detail on every package.** Include a
   "Before you go" section: typical weather for the travel dates, whether the dates
   are peak or festival season and prices/ferries/rooms may rise or sell out, what to
   carry, and a nudge to confirm early. Facts from a cited source, not guessed.
6. **Hard gate: never send a package without its photos.** If photos are missing,
   stop and tell the owner before sending, even if he said "send it".

## When to use
Any time a priced itinerary is being delivered as a standalone document
(PDF) rather than only inline in an email — a formal proposal, a package
sent to a customer for review, anything with "package" in the ask.

## Inputs
- A priced itinerary (from `quote-from-enquiry` / `pricing-request-response`)
  — sell price only, GUARDRAILS §3.
- The guest's name — required before starting; see standard #1.
- `memory/company-profile.md` for the agency entity details (CIN, address,
  contact) that go in every package's footer/closing page.

## The design system (reuse, don't reinvent per package)
Keep using one design system so
the agency's documents read as one company, not a new template each time:
- **Typefaces:** Fraunces (display serif, headings/prices) + Archivo (body/UI
  sans), loaded from Google Fonts.
- **Structure:** cover page (gradient background, logo, title, guest welcome,
  trip meta) → at-a-glance + day-by-day itinerary pages, one section per
  destination, each with its image → where-you'll-stay → pricing (in a
  bordered `pricebox`, sell price only, tiered if there's more than one
  option) → inclusions/exclusions → things-to-know terms → closing page with
  the agency contact block (CIN included).
- **Colour:** pick an accent gradient/palette that suits the destination
  (for example deep purple for a city break, teal for a mountain trip, ocean teal for a beach trip) but keep the
  neutral ink/sand/hairline tokens consistent across all of them.
- **Render:** built as HTML/CSS, printed to PDF via headless Chrome
  (`--print-to-pdf`). Always look at the rendered PDF once before sending —
  don't ship a design unseen.

## Steps
1. Confirm you have: guest name(s), the priced itinerary (sell price only),
   and travel dates.
2. **Check the travel dates against notable occasions** (standard #3) before
   laying out the day-by-day — know which days, if any, need their own entry
   and icon before you start building, not as an afterthought pass.
3. Source or build the destination imagery per the standard above — one per
   destination/city.
4. Design the day-by-day with a small icon per day (standard #4), tied to
   that day's actual activity, with any occasion day visually distinct.
5. Write the welcome message: short, warm, names the guest, one line on what
   the package is and why it fits them if anything specific is known (an
   occasion, a request they made) — matches `memory/tone-of-voice.md`, not a
   form letter.
6. Build the document following the design system above.
7. Render to PDF, look at it once, fix anything visibly broken.
8. Place in the review queue / deliver per however this task's output is
   meant to reach the customer — **a human sends it**, same as any other
   customer-facing artefact (GUARDRAILS §1).

## Guardrail checks
- Sell price only, no net rate or margin visible anywhere in the document
  (§3).
- No image used without a confirmed usable license — real photo of the
  actual landmark, sourced from Unsplash/Pexels/Pixabay or equivalent, never
  scraped from an arbitrary site.
- Guest name is real and confirmed, never a placeholder left in by accident.
- Nothing sent directly to the customer without human approval (§1).

## Stop / escalate
- No guest name available yet → ask, don't guess or placeholder it.
- Can't find/verify a licensable real photo of the destination's landmark →
  don't substitute an unlicensed image or fall back to illustrated art
  silently; flag it to the owner and ask before proceeding.
- Pricing isn't finalized yet → don't brand and send a package around a
  number that's about to change; flag and wait.
