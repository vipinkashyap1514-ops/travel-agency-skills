---
name: security-review
description: Engineering/Security — deep security review of a change or feature touching auth, payments, PII, tenancy, or the supplier layer, including a threat note. Use in addition to review-a-pr for anything security-sensitive.
---

# Playbook: security-review

## Owner
Zoya.

## When
Any change touching authentication, authorisation, payments, PII (passport,
card, personal data), tenant boundaries, the supplier integration layer, file
upload, or a new external dependency — regardless of diff size.

## Steps
1. **Threat note** (module 17) — what could go wrong, what's the abuse case,
   who's the attacker. The five the agency invariants (module 02) are the baseline
   abuse cases to check against.
2. **Secrets** (module 17) — nothing sensitive in the code, tests, fixtures, or
   commit history. Secret scan clean. Credentials referenced by name from the
   store.
3. **Authn / authz** — every touched endpoint authenticates; object-level
   authorisation present (tenant + role + ownership — module 06); no identity
   or tenant from client input; rate-limiting on auth paths.
4. **Injection & output** — parameterised queries only; input parsed at the
   boundary into typed values; output encoded for context; framework escaping
   not bypassed.
5. **Sensitive data** — no PAN stored (tokenise); PII encrypted at rest,
   minimised, access-logged, never in logs/analytics/errors (module 12/17);
   uploads type/size-checked and stored out of web root.
6. **Supplier layer** (module 08) — no credentials/PII/net-rates in logs;
   TLS; response validated before trust.
7. **Dependencies** (module 17) — new deps justified, locked, audited; watch
   for typosquat/compromise advisories.
8. **Tenant isolation** (module 06) — the negative test exists and passes.

## Output
The threat note · findings ranked by severity with file:line and the fix ·
a verdict: **safe to proceed / must fix before merge / needs design change** ·
any finding that is itself an incident (e.g. a secret already committed →
rotate first).

## Stop / escalate
A secret in the repo or history (incident — rotate first) · PAN being stored ·
PII in logs · a missing object-level authz check on a live endpoint · a
dependency advisory match.
