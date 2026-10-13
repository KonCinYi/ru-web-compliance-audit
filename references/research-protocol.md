# Research Protocol: Sources, Evidence and Verification

This reference defines how to support legal conclusions with source evidence. It adapts useful patterns such as an evidence registry, citation verification, a counter-analysis pass and clear provenance labels. It intentionally does not require a particular paid service, NotebookLM, or multi-agent runtime.

## 1. Research design

Before searching, convert the question into a checklist of legal propositions that can be individually verified. For each proposition, state:

- what fact triggers the rule;
- the legal elements and exceptions;
- the needed source;
- the evidence required from code, runtime, documents or the owner;
- what result would support or refute the proposition.

Avoid vague tasks such as “check every law”. Define an auditable scope and then explain what remains outside it.

## 2. Source priority

Use this ladder, adapted to the jurisdiction and issue:

1. **Official legal publication / official consolidated legal act** — law, presidential decree, government decree, regulator order, treaty or EAEU technical regulation. Prefer the official published text; use a consolidated legal database for navigation, but check amendments and effective dates against publication records for high-risk issues.
2. **Official competent authority** — regulator guidance, forms, official FAQs or explanatory material. It may explain enforcement practice but does not replace the legal provision.
3. **Court decisions and official judicial summaries** — useful for interpretation and application; check court, date, case/procedural posture and whether the ruling has relevant status.
4. **Professional commentary** — reputable law firm, professional association or specialist publication. Use to identify ambiguities or find sources, not as the sole support for a material legal claim.
5. **Search snippets, forums, social networks, unsourced summaries** — leads only. Never cite as the sole basis for a legal conclusion or fine.

For EAEU matters use official EAEU and national publication sources. For a foreign-law issue, identify the relevant jurisdiction and its official sources rather than forcing Russian law onto the question.

## 3. Evidence register

Give every source a stable ID (`SRC-001`, `SRC-002`...). Recommended fields:

| Field | Meaning |
|---|---|
| Source ID | Stable identifier used by findings |
| Authority / publisher | Who issued the source |
| Document | Full title, act number/date or official guidance title |
| Provision | Exact article, part, clause or paragraph |
| URL | Direct link, not just a homepage/search result |
| Source tier | Official act / authority / court / commentary / lead |
| Published / effective dates | Keep separate; note transition provisions |
| Accessed on | Date checked |
| Proposition supported | Exact claim this source supports |
| Verification status | VERIFIED / SECONDARY-ONLY / NOT-ACCESSIBLE / NEEDS-RECHECK |
| Notes | Version caveats, amendments, exceptions or access issue |

One source may not support every sentence in a finding. Link specific propositions to specific provisions.

## 4. Citation verification protocol

For each material claim:

1. Open the full source, not only a search snippet.
2. Confirm that the cited article/part exists and that its text matches the report's paraphrase.
3. Confirm whether it is currently in force on the audit date.
4. Check amendments, commencement dates, transition periods and relevant exceptions.
5. Confirm the responsible subject and territorial/material scope.
6. Confirm that all elements needed for the obligation or offense are supported by facts.
7. Record the source ID and verification status in the source register and finding.

If an official source is inaccessible, find an official duplicate/publication record or a reliable consolidated text and explicitly mark the primary source as unavailable. Do not silently downgrade evidence quality.

## 5. Legal analysis: IRAC/CRAC

Use a concise structure:

- **Issue:** what exact legal question is being answered?
- **Rule:** what current provision or authoritative interpretation applies?
- **Application:** which observed/confirmed facts satisfy each element?
- **Counter-analysis:** what is the strongest argument for non-applicability or another interpretation?
- **Conclusion:** finding status and confidence, with caveats.
- **Action:** what should be done, by whom, and how to retest?

Avoid conclusory phrases such as “this is illegal” if an essential fact has not been established. Prefer “potentially non-compliant if X is true; verify X before launch.”

## 6. Provenance and confidence

Keep separate two concepts: factual provenance and legal status.

### Evidence provenance labels

- `OBSERVED` — directly observed in code, browser, HTTP response, public document or authorized scan output.
- `OWNER-CONFIRMED` — explicitly confirmed by an accountable owner/operator.
- `INFERRED` — derived logically from evidence but not directly observed.
- `LEGAL-SOURCE-VERIFIED` — current authoritative text and cited provision checked.
- `UNVERIFIED` — not confirmed or only partially checked.

### Citation status

- `VERIFIED` — relevant current authoritative text opened and matched.
- `SECONDARY-ONLY` — supported only by commentary/consolidated non-primary material; primary verification remains open.
- `NOT-ACCESSIBLE` — source could not be accessed; document the fallback.
- `NEEDS-RECHECK` — source may be stale or an amendment/effective date is uncertain.

Do not use a single confidence score to hide the difference between an observed technical fact and an uncertain legal inference.

## 7. Adversarial review

Before finalising every P0/P1 finding, any high-stakes interpretation and every fine figure, review it as a skeptical second reviewer:

- Is this rule actually about this kind of site/person/transaction?
- Does the rule require access restriction, payment, consent, a specific purpose or some other trigger that has not been proved?
- Could an exception, transition period or special product classification apply?
- Is the cited provision current and exact?
- Does a source actually support the amount/range of the sanction?
- Is a public-facing element being confused with backend processing?
- Is an absent public signal being overinterpreted as proof that a process does not exist?

Record unresolved challenges rather than forcing a definite conclusion.

## 8. Handling sanctions

To report a sanction, verify all of the following:

1. exact legal provision and current wording;
2. responsible subject category (citizen, official, individual entrepreneur, legal entity, other);
3. elements and conditions of the offense;
4. base amount/range or formula;
5. whether turnover, revenue, repeat offense, multiple violations, confiscation, suspension or blocking is relevant;
6. any effective-date or transitional rule;
7. source and access date.

Never multiply the maximum fine by the number of records/users unless the law and procedural facts support that calculation. Do not invent prosecution probability. If one item cannot be confirmed, mark the sanction `NOT VERIFIED` and treat it as an open research issue.
