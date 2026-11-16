---
name: destination-training
description: Operations — work through a supplier's training academy destination course and turn it into the agency destination file the whole company can sell from. Use when training on a new destination, or when the daily destination rotation comes round.
---

# Destination training (Operations · Vikram)

Turns one supplier's training academy destination into a **destination file for the agency** — the thing
Sales quotes from, Marketing writes from, and Care answers from.

Owner: **Vikram** (Operations). Output feeds **Kavya** (Marketing) the same day.

## The copyright line — read this first, every time

a supplier's training courses are **the supplier's copyrighted material**. Their itineraries
are literally their product.

- **Facts are free. Phrasing is not.** Visa rules, flight times, best season,
  airport codes, opening hours, what a landmark is — these are facts, use them.
- **Never copy a sentence, a heading structure, or a day-by-day itinerary** out of
  a course and into the agency file or the agency post. If you find yourself
  reproducing their day 1 / day 2 / day 3 shape, stop and build your own from the
  underlying geography and opening hours.
- **Cite the source of record** in the file — the same rule the IATA training
  modules follow. If a claim came from a supplier's training academy, say so; if it came from a
  tourism board or an airline, cite that instead and prefer it.
- **Verify anything that can expire** — visa policy, fees, seasonal closures,
  flight frequency — against a primary source (embassy, tourism board, airline).
  A course page can be two years stale. Never restate a visa rule on a course's
  authority alone.

## Access reality

Supplier training sites often show a public syllabus but gate the lesson content behind a trade account, and may block automated fetching. Work with what is reachable and mark the gaps rather than guessing.

## Steps

1. **Pick the destination.** Either the one asked for, or the next in
   `training/operations/destinations/_rotation.md`. Prefer destinations the agency
   actually sells — the 11 live packages first, then demand-led.
2. **Read the course detail page** in the browser pane (not WebFetch — it 403s).
   Capture: the module list, the FAQ questions, the stated read time.
   The module list tells you what a competent agent is expected to know.
3. **Fill each module heading with your own researched answer.** This is the work.
   For each heading, find the fact from a primary source and write it in the agency's
   own words. Cite per fact.
4. **Add the three things the supplier won't tell you** — these are what make the file ours:
   - **What it costs us** — typical net ranges, seasons where net moves, which
     supplier we'd source from. (No customer-facing price; that is Priya's call.)
   - **What goes wrong** — the operational failure modes. Visa lead times, transfer
     traps, seasonal closures, the connection that misconnects.
   - **Who it suits** — the traveller profile, honestly, including who it does not suit.
5. **Write the file** to `training/operations/destinations/<slug>.md` using the
   shape below.
6. **Flag the gaps.** Anything you could not verify goes in an explicit
   "Not verified" section. Do not fill a gap with a plausible guess.
7. **Hand to Marketing.** Append a line to
   `review-queue/content/_queue.md` naming the destination file as ready, plus
   the two or three angles you think are genuinely interesting.

## Destination file shape

```markdown
# <Destination> — the agency destination file
Trained by Vikram · <date> · Sources listed per fact

## Sell in one line
## Who it suits / who it doesn't
## Best time to go        (and the shoulder season nobody asks for)
## Getting there from India   (carriers, realistic routings, typical duration)
## Visa for Indian passport holders   ← VERIFY against embassy, every time
## The itinerary we would actually build   (ours, not the supplier's)
## What goes wrong        (operational failure modes)
## Net cost picture       (ranges + season; no sell price)
## Not verified           (explicit gaps)
## Sources
```

## Guardrail checks

- No supplier's training academy sentence, heading structure, or itinerary reproduced. (§Copyright)
- No visa or entry claim stated without a primary source and a check date.
- No sell price in this file — sourcing and cost only. (GUARDRAILS §3)
- Nothing published anywhere; the file is internal until Marketing drafts from it
  and a human approves.

## Stop and escalate when

- The course claims a visa/entry rule that contradicts the embassy → escalate,
  don't average them.
- The destination has an active advisory, conflict, or outbreak → flag to GM
  before any content is built on it.
- You need signed-in course content to go deeper → say so plainly and stop;
  ask the owner to sign in rather than guessing the missing material.
