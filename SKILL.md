---
name: ru-web-compliance-audit
description: >-
  Conduct evidence-based legal and technical compliance audits of websites,
  online catalogs, e-commerce flows, SaaS products, forms, analytics, personal-data
  processing and planned web features under Russian law and applicable EAEU rules.
  Use before launching a Russian-facing website, adding authentication, CRM,
  analytics, payments, advertising, forms or remote-sales features, or when checking
  possible legal violations, fines, policies and remediation priorities.
metadata:
  version: "1.0.0"
  language: "ru"
  focus: "Russian web and e-commerce compliance"
---

# RU Web Compliance Audit

A reusable, evidence-first workflow for auditing a website or planned web feature against the laws that may apply in the Russian Federation and, where relevant, the Eurasian Economic Union (EAEU). It combines legal research, code/runtime inspection, data-flow mapping, risk triage and a practical remediation plan.

> **Not a legal opinion.** This skill supports preliminary research and engineering work. It cannot guarantee compliance or zero fines and does not replace review by qualified Russian counsel, tax specialists, product-certification experts or other relevant professionals.

## 1. When to use this skill

Activate it when asked to review a Russian website, web application, online catalog, e-commerce flow, personal-data processing, login/authentication, privacy notice, cookies/analytics, online advertising, product information, remote sales, payment or cash-register flow, admin panel, CRM, or a possible violation/fine.

Use one of these modes:

- **`quick-triage`** — identify likely high-priority issues from a constrained question or small feature.
- **`feature-gate`** — assess a planned feature before implementation (for example, Google OAuth, analytics, call tracking, CRM, online payment or a recommendation engine).
- **`full-site-audit`** — inspect the codebase, public site and documented business process; produce the full report set.
- **`re-audit`** — verify specific findings after fixes and compare with the previous report.

If no mode is specified, infer it from the task. Do not delay useful work with repeated clarification questions. Record missing facts as open questions and give conditional conclusions.

## 2. Core rules — do not violate these

1. **Verify the law as of the audit date.** Record the exact date and timezone. Laws, sanctions, official guidance and effective dates change. Browse for current sources every run; do not trust stale knowledge or this file as a current statement of law.
2. **Prioritize primary/official sources.** Use the source hierarchy in `references/research-protocol.md`. Search snippets and third-party summaries are leads, not proof.
3. **Cite every material legal conclusion.** Name the act, date/number, exact article/part/paragraph, the version/effective date checked, and a direct source URL. Record access date.
4. **Separate technical observation from legal inference.** A network request or checkbox is an observation; whether it constitutes a legal violation is a separate analysis.
5. **Test applicability.** Explain why the rule applies to this owner, product, audience, transaction, data and territory. Do not assume every rule applies to every website.
6. **Challenge the first conclusion.** For every material finding, formulate the strongest plausible reason the rule might not apply or the evidence might be insufficient; resolve or document the uncertainty.
7. **Never invent business facts.** Do not fabricate the seller’s legal form, INN/OGRN, address, warranty, delivery terms, certificates/declarations, customer reviews, consent basis, server location or data-retention period.
8. **Do not equate absence of evidence with compliance.** Use “not observed”, “not verified” or “unknown” where appropriate.
9. **No automatic legal publication.** Do not publish or silently replace privacy policies, public offers, consent texts, returns/warranty terms or seller details using boilerplate without confirmed business facts and owner review.
10. **Protect production systems.** Do not submit real personal data, place orders, trigger real payments, send marketing, bypass access controls or run intrusive scans without explicit authorisation. Audit public pages and local code conservatively.
11. **No unsupported fine estimates.** Verify the current sanction, subject category, qualifying conditions, repeat-offense rules and calculation basis before reporting a number.
12. **Be explicit about limitations.** If browsing, repository access, runtime inspection, a scanner or a test is unavailable, name the limitation and continue with the best feasible alternative.

## 3. Start-up and safety

### 3.1 Establish scope

Determine what is being audited, jurisdiction, target URLs/repository, environment (local/staging/production), business model, public launch status, and whether the task is read-only or includes fixes. Read existing project instructions, legal reports, incident notes and handoff documents first. Do not ask again for facts already reliably documented.

### 3.2 Protect files before edits

For an audit-only run, do not change application code by default. Before any code/config/document edit:

- inspect Git status and existing local changes, if Git is present;
- create a new, non-overwriting backup using the project’s established procedure;
- verify the backup includes the relevant source/config/assets/docs and record its path;
- avoid copying secrets, `.env` values or personal data into reports/backups unless strictly necessary and explicitly permitted;
- never modify unrelated backend/repositories unless explicitly authorised.

If a backup cannot be created or verified, do not proceed with potentially destructive edits.

### 3.3 Build the factual inventory

Inspect what exists, not what someone assumes exists:

- routes/pages, rendered HTML and user flows;
- forms, validation, submissions, APIs and server actions;
- phone, email, messenger, order, payment, delivery, returns and warranty flows;
- authentication, roles, user accounts and gated content;
- cookies, localStorage/sessionStorage, pixels, analytics, call tracking, fonts, maps, CAPTCHA, chat, error monitoring and third-party SDKs;
- outbound hosts and dependencies that may receive data;
- hosting/deployment region, databases, logs, backups and admin access, to the extent information is available;
- seller/operator identity, intended audience (B2B/B2C), goods/service categories and actual transaction flow;
- public policies and documents, their links and whether their text matches actual behavior.

When inspecting code, note exact file paths and the relevant component/function. When inspecting a live site, record the URL, date, viewport/browser and observable result. Do not infer backend behaviour solely from frontend code.

## 4. Research and analysis workflow

Follow the phases in order. You may preview later phases to understand dependencies, but do not mark work complete before evidence is gathered.

### Phase A — Scope and hypotheses

Create a checklist of legal questions based on the actual feature/site. List facts that are known, inferred and missing. Separate current functionality from roadmap items. Do not spend tokens analysing future features as if they already exist; record them in a future-readiness checklist.

### Phase B — Data and transaction map

For each data field/event/transaction, record: source, purpose, trigger, destination, storage location, recipients/processors, retention/deletion, legal basis claimed, user-facing notice/consent, and confidence in the evidence. Include indirect data such as IP addresses, identifiers, analytics IDs, call logs and support tickets where relevant, but do not automatically classify every technical identifier as personal data without analysis.

### Phase C — Research the current law

1. Break the issue into verifiable legal propositions.
2. Search official Russian legal publication resources, competent regulators and relevant EAEU sources first.
3. Use consolidated legal databases for navigation and current wording, then cross-check high-impact/new provisions against official publication records.
4. Verify enactment date, publication date, effective date, amendments, transitional rules, scope and exceptions.
5. Distinguish binding statute/regulation, court interpretation, official agency guidance, draft bill and commentary.
6. Add every material proposition to the evidence register described in `references/research-protocol.md`.

### Phase D — Analyse applicability (IRAC/CRAC)

For each issue write, in concise form:
- **Issue:** exact question;
- **Rule:** verified current legal provision;
- **Application:** observed facts mapped to each legal element;
- **Counter-analysis:** why the provision may not apply or why evidence is incomplete;
- **Conclusion:** one of the status labels below;
- **Action:** concrete next step and responsible decision-maker.

If scope depends on facts (seller identity, B2B/B2C, hosting, data recipients, contract formation or product classification), do not pretend it is settled. Provide conditional branches.

### Phase E — Verify claims adversarially

Before finalising, review every P0/P1 finding and every fine figure as a skeptical second reviewer:
- Does the cited text actually say what the report claims?
- Is the quoted article/part current and in force on the audit date?
- Is the addressee/subject within scope?
- Are all elements of the offense/obligation supported?
- Is there an exception or transition period?
- Is the source primary or secondary?
- Would the finding change if an unknown owner fact had a different value?

Mark citations `VERIFIED`, `SECONDARY-ONLY`, `NOT-ACCESSIBLE` or `NEEDS-RECHECK`. Never present a secondary-only source as verified primary evidence.

### Phase F — Risk and remediation

Use the risk model in `references/report-templates.md`. Rank issues by obligation, potential harm/sanction, exposure, exploitability/visibility, uncertainty and cost to fix. Do not invent a numerical probability of prosecution. Distinguish legal severity from likelihood of detection and from engineering priority.

### Phase G — Report and re-audit

Use the deliverables defined in `references/report-templates.md`. Save reports in a dated folder such as `reports/legal-compliance/YYYY-MM-DD/`, or use the project’s existing report convention if one exists. Preserve earlier reports; add a new dated run or append a clearly labelled section rather than overwriting history. Include a concise executive summary and exact next actions.

## 5. Russian and EAEU legal-domain coverage

For a full audit, review each domain below for applicability; “not applicable now” still needs a short factual reason. Load `references/russian-law-map.md` for prompts and likely primary sources.

- Personal data and privacy: operator status, processing purposes, notices/policies, consents, Roskomnadzor notification, localisation, cross-border transfer, processors, retention/deletion, breach response and security.
- User authentication and information access: determine whether the resource actually requires authentication and whether a special statutory method applies; assess foreign OAuth only after checking scope and current law.
- Consumer information and remote sales: seller identification, accurate price/discount/availability/specifications, order formation, delivery/payment/returns/warranty, pre-contract information and goods-specific duties.
- Advertising and marketing: distinguish ordinary information about own goods from advertising based on facts; check internet-ad marking/reporting when applicable, substantiation of claims, actual discounts and consent for promotional communications.
- Payments, tax and cash-register duties: trace who receives funds, when payment occurs, who issues receipts and which payment mechanisms are planned. A phone-originated sale is not automatically outside cash-register rules.
- Product conformity and labelling: classify each actual product/SKU first, then identify applicable EAEU technical regulations, conformity documents, labels, manuals and registry information. Do not apply every regulation to every product.
- Intellectual property: rights to photos, logos, fonts, trademarks, product descriptions, reviews and downloaded assets.
- Security and infrastructure: admin roles, secrets, authentication, access logs, backups, hosting location, incident handling and third-party suppliers; distinguish legal requirements from good practice.
- Language and accessibility of mandatory consumer information: check current Russian-language requirements and exceptions.
- Future features: online payment, customer accounts, CRM, profiling/recommendations, analytics, call tracking, email/SMS marketing, delivery integrations and file uploads each trigger a fresh feature-gate review.

For a narrow `quick-triage` or `feature-gate`, do not exhaustively expand unrelated domains. Document scope and excluded domains.

## 6. Status labels

Assign exactly one primary status to each finding:

- **CONFIRMED-NONCOMPLIANCE** — verified facts and current applicable rule support a mismatch.
- **LIKELY-RISK** — strong signal exists but one or more legal/factual elements need verification.
- **OWNER-FACT-REQUIRED** — outcome depends on a business/technical fact not available.
- **NOT-APPLICABLE-NOW** — reasoned conclusion for the current scope; record what would make it applicable later.
- **FUTURE-CONTROL** — a planned feature/process will need review before launch.
- **NO-ISSUE-OBSERVED** — scoped checks did not reveal an issue; not a guarantee of compliance.

Keep evidence labels separate from legal status:
- `OBSERVED` — directly seen in the code/runtime/document;
- `OWNER-CONFIRMED` — explicitly confirmed by a responsible person;
- `INFERRED` — reasoned inference, not directly observed;
- `LEGAL-SOURCE-VERIFIED` — legal source and relevant text checked;
- `UNVERIFIED` — evidence could not be confirmed.

## 7. Findings and fines

For every material finding record:
- finding ID, status and priority;
- location/function/flow and reproducible observation;
- applicable act, article/part/paragraph, current wording/version and effective date;
- direct source URL and citation-verification status;
- explanation of applicability and strongest counterargument;
- unknown facts and owner questions;
- potential sanction only after checking the current provision, liable person category, elements, repeat-offense rules and calculation basis;
- practical remediation, dependencies, owner/approver and retest criteria.

Never state “the maximum fine is X” without saying **for whom**, **for which exact offense**, **under what conditions**, and whether X is an individual cap, turnover-based formula or other measure. If the sanction source cannot be verified, write `SANCTION NOT VERIFIED` and make source checking a blocking action.

## 8. Technical scanners and external tools

A scanner is supporting evidence, not a legal decision. If an optional tool such as [PD Scanner for 152-FZ pre-screening](https://github.com/LevaAverGit/pd-scanner-152fz-v2) is available:

1. Check its repository, license, last update, dependencies, security notes and what it sends/stores before installation or execution.
2. Prefer a pinned release/commit and local execution. Do not run unknown scripts directly against production.
3. Scan only a domain/environment the user owns or is authorised to assess. Do not submit forms, enter real personal data, trigger purchases/payments or crawl off-scope hosts.
4. Preserve output and map findings to observed evidence. Treat `observed`, `inferred` and owner-supplied facts separately.
5. Manually verify false positives/negatives and applicable law. A clean scan does not prove compliance; a flagged signal does not prove a violation.

Do not install dependencies or external MCP tools automatically unless the user/environment permits it. If a tool is unavailable, continue with source/code review and state the limitation.

## 9. Remediation guardrails

Default mode is **audit-only**. If user explicitly authorises fixes:

- create and verify a backup before edits;
- fix confirmed technical issues in small batches;
- do not write legal texts with invented operator facts, product information, contract terms or consent purposes;
- use clearly labelled placeholders and block public release until the owner fills them;
- do not add login, consent banners, cookies or data collection merely to satisfy a generic checklist;
- do not alter the backend or production settings without explicit scope and access permission;
- after each batch, run relevant lint/type/build/tests and verify the user flow;
- update reports with changed files and before/after evidence;
- keep unrelated user changes intact.

## 10. Completion criteria

Do not call an audit “complete” merely because the checklist was read. For the defined scope, completion requires:

- factual site/code/flow inventory with limitations;
- data map where processing is relevant;
- current-law research and source log;
- material claims citation-checked;
- applicability and counter-analysis for material findings;
- prioritized findings and action plan;
- owner questions and counsel/specialist escalations;
- launch checklist and future feature gates;
- status of every check (`passed`, `failed`, `unknown`, `not applicable`, `not run`);
- a handoff note with the exact next step.

Final wording must be scoped, e.g. “No confirmed issue was found in the checks listed; the following unknowns remain.” Never promise that the site is entirely lawful or free from fines.

## 11. References to load on demand

- For source ranking, legal-claim verification and adversarial review: `references/research-protocol.md`.
- For Russian/EAEU domain checklist and starting points: `references/russian-law-map.md`.
- For report schemas, risk ranking and output templates: `references/report-templates.md`.
- For project facts and a reusable intake questionnaire: `templates/site-context-template.md`.

Read only the reference needed for the current phase; load all of them for `full-site-audit`.
