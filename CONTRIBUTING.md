# Contributing

Thanks for helping make these playbooks better for small travel agencies.

## Ways to contribute
- Fix a wrong or outdated rule (cite the official source).
- Add a skill for a task agencies do often.
- Improve clarity, examples or structure.
- Report a place where a skill could cause a customer or money mistake.

## Ground rules
1. **No real data.** No names, phone numbers, emails, booking references, passport details, prices tied to a real customer, passwords or API keys. Use placeholders such as `[YOUR_MARGIN]%`.
2. **No supplier or company names tied to a real business** unless it is a public, generic example (an airline, a GDS).
3. **Keep the wall.** Supplier net prices never go to customers; customer sell prices never go to suppliers.
4. **Prepare, don't execute.** A skill drafts work; a human pays, ticketises, merges and deploys.
5. **Cite sources** for fare, visa, tax and legal facts, and say when they were checked.

## Skill format
Each skill is `skills/<name>/SKILL.md` with front matter:

```markdown
---
name: skill-name
description: One line on what it does and when to use it.
---
```

Then: purpose, inputs, steps, guardrail checks, and when to stop and escalate.

## Pull requests
Fork, branch, make one focused change, and fill in the PR template. Maintainers review for accuracy and safety before merging.
