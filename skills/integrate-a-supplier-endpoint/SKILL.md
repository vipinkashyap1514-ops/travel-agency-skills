---
name: integrate-a-supplier-endpoint
description: Engineering — add or change a supplier API integration (the supplier, GDS, NDC) with the full resilience and contract-test package. Use for any work on a supplier connection.
---

# Playbook: integrate-a-supplier-endpoint

## Owner
Farhan.

## Inputs
- The supplier operation (search / price / seat map / hold / book / cancel /
  refund status), its sandbox and prod endpoints, the credential set and auth
  scheme (for the supplier: which of the 3 hosts / 2 auth schemes — module 03).
- The domain model the response must normalise into.

## Steps
1. **Read the systems context** — `training/operations/23–32` for how this
   supplier's model actually works (PSS / availability / NDC / messaging), and
   module 08 for the patterns.
2. **Classify the operation** — read/idempotent vs mutating. This decides retry
   and idempotency handling.
3. **Config, not code** — endpoints, ClientId (staging ≠ prod for the supplier air),
   credentials by name from the secret store. Never hard-coded, never a prod
   credential in a test.
4. **Wrap the call** with: connect + read timeouts tuned to the operation;
   bounded retry with backoff + jitter (idempotent only); an idempotency key
   for mutations; a circuit breaker per host; a bulkhead so it can't starve the
   app.
5. **Normalise at the boundary** — map the raw payload to our domain model in
   one place. Nothing downstream sees a raw supplier shape. **Strip / never
   propagate the net rate** past this layer (`GUARDRAILS §3`).
6. **Partial failure** — return what succeeded + an explicit "incomplete"
   signal; don't fail the whole request because one host timed out.
7. **Logging & tracing** (module 12) — supplier, host, operation, correlation
   id, latency, outcome. Never credentials, PII, or net rates.
8. **Contract test** — record real sandbox request/response fixtures; assert
   our parsing matches; run in CI so a supplier change breaks the build, not
   prod.
9. **Replay path** — persist enough of a sanitised failed interaction to
   reproduce it in a test.
10. **PR** with the spec, the fixtures, and a note on sandbox vs prod
    differences.

## Output
Branch · the wrapped + normalised client · contract tests + fixtures ·
config keys added (values set by a human) · PR · Guardrail check.

## Stop / escalate
No sandbox available to record fixtures · a credential/endpoint that would have
to be hard-coded · the supplier's behaviour contradicts its docs · a net rate
that can't be cleanly stripped at the boundary · anything needing prod
credentials.
