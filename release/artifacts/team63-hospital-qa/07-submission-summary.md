# 07 - Submission Summary

## Scope Tested
This submission now includes:
- Documentation pack (inventory, stories, strategy, traceability, execution, API inventory)
- Expanded test-case catalog (57 high-value cases)
- Structured UI/API test data sets
- Playwright TypeScript automation scaffold
- Extended executed automation suites (UI + API, including module suites)
- Defect/enhancement registers

## Environment
- Target: `https://team63.qaaglobal.com`
- Credentials source: local env vars only (`TEAM63_*`)
- Secrets handling: no hardcoded credentials in tracked code/config/docs

## Coverage Summary
- Planned test cases: 57
- Test cases marked PASS: 19
- Test cases marked NOT_RUN: 38
- Latest consolidated automation run: 21 tests, 21 passed, 0 failed, 0 errors

## Execution Summary
Latest executed automation set:
- `tests/api/session.api.spec.ts`
- `tests/ui/login.spec.ts`
- `tests/ui/dashboard.smoke.spec.ts`
- `tests/ui/module-navigation.spec.ts`
- `tests/ui/edge-cases.spec.ts`
- `tests/ui/patients.spec.ts`
- `tests/ui/appointments.spec.ts`
- `tests/ui/lab.spec.ts`
- `tests/ui/ipd-bed.spec.ts`
- `tests/ui/billing.spec.ts`
- `tests/ui/cross-module.spec.ts`

Evidence:
- `reports/ui/junit.xml`
- `reports/ui/html-report/index.html`

## Defects by Severity
- S1 Critical: 1
- S2 High: 2
- S3 Medium: 4
- S4 Low: 5
- Total logged: 12 (8 Reproduced, 4 Blocked, 0 Not Reproduced — source: `defects/defects.csv`)

**Correction:** the 21/21 result above covers the Playwright UI automation suite only. Defect retesting (`docs/08-defect-retest-results.md`) was performed separately via targeted model/API-layer checks and reproduced 8 real defects, including one Critical (DEF-001, negative billing total reaching invoiced state) and two High (DEF-002, DEF-003). The correct framing for this submission is: automation run was green; defect retest found real validation and security issues.

## Automation Summary
- Framework: Playwright + TypeScript
- Execution mode: serial worker (`workers: 1`) for shared environment safety
- Failure diagnostics: trace/video/screenshot on failure
- Reporting: HTML + JUnit
- Env contract: `TEAM63_BASE_URL`, `TEAM63_USERNAME`, `TEAM63_PASSWORD`, optional route/API vars

## Important Risks Still Open
1. Mutation-heavy domain workflows not yet executed end-to-end for all modules (create/update/cancel/discharge/payment transitions).
2. Multi-role authorization matrix remains incomplete without additional role credentials.
3. Full cross-module numerical reconciliation (dashboard totals vs source entities) remains partial.
4. Official API collection/spec still unavailable; deeper API contract coverage constrained.

## Known Limitations
- No invented endpoints, fields, or business rules were used.
- NOT_RUN cases are explicitly retained where evidence does not exist.
- Remaining NOT_RUN items are due to pending high-impact mutation/role workflows, not hidden failures.

## Secret-Safety Validation
- `.env.example` contains placeholders only.
- `.gitignore` includes `.env*` (except `.env.example`), auth state, HAR, cookie/state artifacts, temp outputs.
- No usernames/passwords/tokens/cookies in tracked source files.

## Release Signal
- Current signal: **Amber (Conditional Go)**
- Reason: implemented UI automation is fully green, but 8 reproduced defects (1 Critical, 2 High, 4 Medium, 5 Low logged) and unresolved NOT_RUN high-risk workflows both prevent Green sign-off.
