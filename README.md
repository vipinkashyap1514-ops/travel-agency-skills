# Travel agency skills

A set of AI agent skills and role definitions for running a small travel agency: quoting, pricing, supplier requests, ticketing instructions, reissues, refunds, visa and document checks, group bookings, finance, legal, compliance, and case tracking.

These are working playbooks written from real agency operations. The company, supplier and customer details have been removed. Fill in your own in `company.example.yaml`.

## Safety first

- The skills **prepare** work. A human does every payment, ticket issue, merge and deploy.
- **Supplier net prices never go to customers.** Customer sell prices never go to suppliers. See `guardrails/GUARDRAILS.md`.
- Fares, fare rules, visa and tax rules change. Verify every fact against the current official source before using it with a customer.
- Nothing here is legal, tax or financial advice.
- Never put passwords, API keys, passport numbers or customer data into these files.

## Layout

```
skills/       one folder per playbook (SKILL.md)
agents/       role definitions (sales, operations, finance, legal, engineering)
guardrails/   the rules every role follows
company.example.yaml
```

## Set up

1. Copy `company.example.yaml` to `company.yaml` and fill it in.
2. Replace the `[PLACEHOLDERS]` in the skills with your policies (margins, fees, interest rates).
3. Copy the folders you want into your agent's skills directory.

## Notes on references

Some skills mention files such as `memory/policies.md`, `memory/company-profile.md`, `memory/supplier-contacts.md`, `ORG.md` (staffing, SLAs and which scheduled shifts are on) or `work-items/`, and placeholders such as `{{EMAIL}}` or `{{CITY}}`. These are your own private notes and details. Create them in your own workspace and keep them out of this repository.

## Status

Skills were extracted from live use. They have no automated tests yet, so check results by hand.

## License

MIT. See [LICENSE](LICENSE).

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md), [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) and [SECURITY.md](SECURITY.md). Changes are listed in [CHANGELOG.md](CHANGELOG.md).
