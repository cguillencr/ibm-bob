---
name: security-review
description: Perform an evidence-driven defensive security review of code and configuration against a portable security baseline; use for a focused security assessment.
---

# Security Review

1. Confirm scope and authorized repository; do not access unrelated or external targets.
2. Examine authentication, authorization, secrets, logging, dependency maintenance, input validation, injection risks, data handling, error behavior and deployment defaults.
3. Read `../../rules/02-security-baseline.md` and the checklist; apply only checks relevant to the project context.
4. Record concrete evidence, affected file/line, impact, exploit prerequisites when established, mitigation and severity rationale.
5. Keep risk hypotheses separate from confirmed findings; avoid claiming scanner results unless tools ran and returned output.
6. Suggest focused tests and secure fixes; no secret extraction, credential rotation, live changes or production testing without approval.

Consult `checklist.md` for the final quality gate. Apply shared workspace and relevant mode rules throughout; this skill does not override approval gates or tool permissions.
