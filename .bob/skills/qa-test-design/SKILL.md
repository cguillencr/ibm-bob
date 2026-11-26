---
name: qa-test-design
description: Design traceable functional, negative, integration and regression test cases from approved requirements; use when asked for a QA test plan or cases.
---

# Qa Test Design

1. Identify the approved spec and trace each test case to requirement IDs.
2. Cover normal, negative, boundary, authorization, integration and regression behavior proportionately.
3. For every test case provide at minimum **Description**, **Steps**, and **Expected result**; use `templates/qa-case.md` (in this skill) when applicable.
4. Distinguish test design from execution and document preconditions, data and environment assumptions.
5. When recording a defect include at minimum **Description**, **Steps to reproduce**, **Actual result**, **Expected result**; use `templates/defect-report.md` (in this skill).
6. Return coverage gaps, blocking dependencies and a list of proposed cases. Never invent executed evidence.

Consult `checklist.md` for the final quality gate. Apply shared workspace and relevant mode rules throughout; this skill does not override approval gates or tool permissions.
