---
name: do-a-spike
description: Engineering — a timeboxed investigation to answer a technical question or de-risk a decision, ending in a written recommendation (and usually a throwaway prototype), not production code. Use before committing to a hard/uncertain change.
---

# Playbook: do-a-spike

## Owner
Aditya frames it; whoever has the context runs it.

## Steps
1. **Frame the question** precisely — one sentence. What decision does the
   answer unblock? What's the timebox?
2. **Define "done"** — the specific things you must be able to state at the end
   (feasibility, cost, risk, the recommended approach, what's still unknown).
3. **Investigate** — read the code / supplier docs / `training/` modules; build
   the smallest **throwaway** prototype that answers the question, on a
   clearly-labelled spike branch. It is not production code and won't be
   merged.
4. **Check it against the constraints** — does the approach respect the five
   invariants, tenancy, money/time correctness, supplier resilience? If it
   can't, that's a finding.
5. **Write the recommendation** — the answer, the approach, the main
   alternatives and why not, the risks, the effort estimate, what's still
   unknown. If it's reversal-expensive, this becomes the input to an ADR
   (module 05).

## Output
A written recommendation memo + the spike branch (labelled throwaway) + a
clear next step (proceed with approach X / needs an ADR / not feasible / need
another spike).

## Stop / escalate
The question turns out to be a product decision, not a technical one → back to
Product/Aditya. The timebox is hit without a confident answer → say so and
recommend the next spike rather than guessing.

## Never
Ship spike code to production. Extend the timebox silently.
