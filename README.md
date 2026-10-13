# RU Web Compliance Audit

**Evidence-first legal and technical pre-audit for websites operating in or targeting Russia.** The skill helps an AI coding agent map real website behaviour, research applicable Russian/EAEU requirements, verify sources, classify risks and produce an actionable remediation plan.

> This is a research and engineering aid, not legal advice or a guarantee of compliance. High-impact conclusions should be reviewed by qualified Russian counsel and relevant specialists.

## What it does

- Audits website code, rendered pages, forms, cookies/analytics, third-party requests, authentication and transaction flows.
- Maps personal-data flows and distinguishes observed facts from inference and owner-supplied facts.
- Researches current law using official primary sources first; records enactment/effective dates and transitional provisions.
- Builds an evidence register and checks each material legal claim against the cited source.
- Uses an adversarial verification pass for high-risk findings and sanctions.
- Produces prioritised findings, questions for the owner, launch checks and future-feature gates.
- Supports four workflows: quick triage, feature gate, full audit and re-audit.
- Optionally uses a separate, locally run website scanner as supporting evidence; scanners do not decide legal applicability.

## Why this design

This skill uses a few strong process patterns found in existing open-source work, without requiring their runtimes:

- **Evidence register, source verification and adversarial review** — methodology informed by [Flosters/legal-research](https://github.com/Flosters/legal-research). This skill does not depend on NotebookLM, Google authentication or Claude Code subagents.
- **Technical pre-screening with evidence provenance** — optional tool reference to [LevaAverGit/pd-scanner-152fz-v2](https://github.com/LevaAverGit/pd-scanner-152fz-v2). The scanner is not bundled and must be reviewed/pinned before use.
- **Clear compliance output, risk areas and approvals** — inspired by the general workflow pattern in [Anthropic knowledge-work-plugins: compliance-check](https://github.com/anthropics/knowledge-work-plugins/tree/main/legal/skills/compliance-check), adapted to Russian legal research and website engineering.
- **Portable skill format and progressive disclosure** — follows the open [Agent Skills specification](https://github.com/agentskills/agentskills/blob/main/docs/specification.mdx).

These are methodology references. No external source code is bundled or copied into this skill.

## Install

The skill follows the standard Agent Skills directory layout:

```text
ru-web-compliance-audit/
├── SKILL.md
├── README.md
├── references/
│   ├── research-protocol.md
│   ├── russian-law-map.md
│   └── report-templates.md
└── templates/
    └── site-context-template.md
```

For a compatible agent, copy this directory into its supported skills folder. Exact paths depend on the agent (for example, `.agents/skills/`, `.claude/skills/`, or `.github/skills/`). Check your agent's documentation. If skills are not loaded automatically, tell the agent to read `SKILL.md` and the referenced files directly.

## Usage examples

- “Run a `full-site-audit` of this Russian e-commerce site. Read the skill and all references, inspect the actual code and flows, verify current primary sources, and produce all required reports. Audit only; do not change code.”
- “Use `feature-gate` to assess whether we can add Google OAuth, analytics, call tracking and a CRM to this site under current Russian law.”
- “Use `quick-triage` to review this consent form and privacy notice. Cite the exact current rules and separate confirmed issues from unknown facts.”
- “Use `re-audit` to verify these findings after the fixes and preserve the previous audit history.”

## Reports

For a full audit, the default output folder is:

```text
reports/legal-compliance/YYYY-MM-DD/
```

If the project already has a report convention, follow it without overwriting history. The references define minimum reports and finding formats.

## Security and safe use

- Do not submit real personal data into website forms during an audit.
- Do not run unknown scanners against production before reviewing their code, permissions and network behaviour.
- Do not scan domains without authorisation.
- Do not expose secrets, `.env` values, tokens or customer records in audit reports.
- Do not auto-publish privacy policies, consent wording, public offers, warranty/return terms or seller details based on invented information.

## Limitations

A code audit cannot fully establish facts about actual business conduct, contracts, server locations, supplier agreements, tax treatment, product certification or internal processes. Unknown facts must be assigned to the owner. Product-specific conformity questions require correct SKU classification; complex issues may require a certification specialist. Legal and tax conclusions should be escalated where appropriate.

The skill does not promise “zero fines” or certify that a site complies with every law. It reports the scope checked, evidence obtained, assumptions, unresolved issues and recommended actions.
