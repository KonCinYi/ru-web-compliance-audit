# Report Templates and Acceptance Criteria

## 1. Default report layout

For a full audit, create a dated folder, unless the project already has a stable reporting convention:

```text
reports/legal-compliance/YYYY-MM-DD/
├── 00-executive-summary.md
├── 01-scope-and-owner-questions.md
├── 02-site-inventory-and-data-map.md
├── 03-legal-register-and-evidence.md
├── 04-findings-and-sanctions.md
├── 05-remediation-plan.md
├── 06-launch-checklist.md
├── 07-future-feature-gates.md
└── 08-source-log.md
```

Keep previous reports. For a re-audit, create a new dated run and cross-reference prior finding IDs. Do not overwrite history or claim a finding is fixed without testing.

## 2. Executive summary template

```md
# Executive Summary
- Audit date/timezone:
- Site / repository / environment:
- Audit mode and scope:
- Site/business model observed:
- Areas inspected:
- Areas not inspected and why:
- Confirmed non-compliances:
- Likely risks:
- Owner facts required:
- Future controls:
- Top pre-launch blockers:
- Overall status: HOLD / PROCEED WITH CONDITIONS / NO BLOCKER OBSERVED IN SCOPE
- Legal-review limitations:
```

The overall status is a scoped engineering aid, not a certification or guarantee.

## 3. Finding template

```md
## LEG-XXX — Short, factual title
- Status: CONFIRMED-NONCOMPLIANCE / LIKELY-RISK / OWNER-FACT-REQUIRED / NOT-APPLICABLE-NOW / FUTURE-CONTROL / NO-ISSUE-OBSERVED
- Priority: P0 / P1 / P2 / P3
- Evidence provenance: OBSERVED / OWNER-CONFIRMED / INFERRED / UNVERIFIED
- Location: URL, file, component, flow or business process
- Observation: what was directly seen; include reproducible steps
- Legal issue: exact question
- Rule: act, number/date, article/part/paragraph and applicable version/effective date
- Source ID and direct URL:
- Citation status: VERIFIED / SECONDARY-ONLY / NOT-ACCESSIBLE / NEEDS-RECHECK
- Applicability: how each required legal element maps to the facts
- Counter-analysis / exception:
- Missing owner facts:
- Potential sanction: exact current basis, subject and conditions, or SANCTION NOT VERIFIED
- Recommended action:
- Decision owner / specialist:
- Verification after remediation:
- Current state: open / in progress / fixed awaiting retest / fixed and verified / accepted risk (with approver)
```

## 4. Risk priority

Use priority as an operational triage, not a prediction of enforcement likelihood.

- **P0 — launch blocker / urgent:** credible major legal or safety issue, potentially severe sanction, ongoing unlawful collection/transfer, exposure of sensitive data or other urgent risk. Escalate immediately and stop the risky feature where authorised and proportionate.
- **P1 — high:** likely breach of a clear requirement, material missing disclosure/document, unsupported product conformity claim, or high-risk processing design. Fix or obtain counsel decision before launch.
- **P2 — medium:** substantive issue with limited scope or one requiring a known owner decision/process improvement. Set an accountable owner and date.
- **P3 — future control / improvement:** needed before a planned feature, evidence hygiene, or non-blocking improvement.

For each finding separately record (a) legal severity, (b) strength of evidence, (c) user/business impact, (d) remediation effort and (e) deadline. Do not fabricate a probability percentage.

## 5. Legal register template

| ID | Act / document | Provision | Subject/scope | Current version checked | Effective date relevant | Source ID | Status of applicability | Notes |
|---|---|---|---|---|---|---|---|---|

The “status of applicability” must include a reason, not only yes/no.

## 6. Source log template

| Source ID | Authority | Full title | Provision | Direct URL | Source tier | Published/effective dates | Accessed on | Claim supported | Verification status |
|---|---|---|---|---|---|---|---|---|---|

## 7. Data map template

| Data/event | Source/trigger | Purpose | Destination | Storage region | Recipients/processors | Claimed basis | Notice/consent | Retention/deletion | Evidence/provenance | Unknowns |
|---|---|---|---|---|---|---|---|---|---|---|

Do not place real personal data, credentials or unnecessary identifiers in reports.

## 8. Owner questions

Ask one consolidated, prioritised set. Before asking, search project docs and existing conversation/report files for answers. For each question include:

- why it matters;
- which findings depend on it;
- safe default until answered;
- who should answer (owner, accountant, counsel, certification specialist, infrastructure operator).

Examples: legal seller identity; B2B/B2C audience; who receives and fulfils phone orders; hosting/database/backup regions; analytics and third-party services; product conformity records; delivery and returns; actual payment/receipt process.

## 9. Remediation plan template

| Step | Finding IDs | Change/action | Type (code/process/document/vendor/counsel) | Owner | Dependencies | Acceptance test | Status |
|---|---|---|---|---|---|---|---|

Separate changes that can safely be made in code from decisions requiring confirmed facts, counsel approval, tax guidance or product-certification expertise.

## 10. Re-audit criteria

When checking a fix:

1. Restate the original finding and its acceptance test.
2. Inspect the actual new code/runtime/process, not only the commit message.
3. Re-check relevant legal source if the legal version/date changed.
4. Capture evidence and test outcome.
5. Mark “fixed and verified” only when the acceptance criteria passed.
6. If the fix solves a visible signal but not the underlying process, keep the finding open.
7. Record regressions and remaining unknowns.
