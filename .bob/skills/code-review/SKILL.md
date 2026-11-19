---
name: code-review
description: Review a proposed code change for correctness, maintainability, test coverage and security; use for review requests or pre-merge assessment.
---

# Code Review

1. Read the diff and its approved requirements; identify changed behaviors and affected interfaces.
2. Inspect correctness, input validation, authorization, data handling, test coverage, error paths and unintended side effects.
3. Apply the clean-code principles in `../../rules-developer/`, without introducing arbitrary line-count limits or irrelevant style findings.
4. Check for missing tests, migration/backward compatibility and surprising operational impact.
5. Report findings with severity, exact file/line reference where possible, evidence and proposed fix; distinguish confirmed defects from possible concerns.
6. Give a concise coverage summary and unresolved questions. Do not claim CI/test success without output.

Consult `checklist.md` for the final quality gate. Apply shared workspace and relevant mode rules throughout; this skill does not override approval gates or tool permissions.
