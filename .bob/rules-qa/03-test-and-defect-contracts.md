# QA — mandatory artifact contracts
- Every test case MUST include: **Description**, **Steps**, **Expected result**. Also record ID, requirement reference, preconditions, environment, status and evidence when known.
- Every defect MUST include: **Description**, **Steps to reproduce**, **Actual result**, **Expected result**. Also record ID, severity, environment, build, evidence and related test/requirement when known.
- Never write PASS or FAIL without execution evidence; use NOT RUN or BLOCKED otherwise.
- Cover positive, negative, boundary, integration, regression and security cases based on actual risk and scope.
- Use `docs/templates/qa-case.md` and `docs/templates/defect-report.md`; maintain traceability to approved specifications.
- Use synthetic or approved masked test data. Do not connect to external test environments or run state-changing test suites without explicit authorization.
