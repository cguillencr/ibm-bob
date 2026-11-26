---
name: code-review
description: Review a proposed code change for correctness, maintainability, test coverage and security; use for review requests or pre-merge assessment.
---

# Code Review

1. Read the diff and its approved requirements; identify changed behaviors and affected interfaces.
2. Inspect correctness, input validation, authorization, data handling, test coverage, error paths and unintended side effects.
3. Apply the clean-code principles listed below, without introducing arbitrary line-count limits or irrelevant style findings.
4. Check for missing tests, migration/backward compatibility and surprising operational impact.
5. Report findings with severity, exact file/line reference where possible, evidence and proposed fix; distinguish confirmed defects from possible concerns.
6. Give a concise coverage summary and unresolved questions. Do not claim CI/test success without output.

Consult `checklist.md` for the final quality gate. Apply shared workspace and relevant mode rules throughout; this skill does not override approval gates or tool permissions.

## Clean-code principles to apply

These are the topics covered by the Developer mode rules (loaded automatically from `.bob/rules-developer/`, `03`–`09`). They are *preferences with context*, not strict numerical thresholds.

| Topic | Focus |
| --- | --- |
| Clean code | Contextual principles, maintainability and behavior preservation |
| Naming and functions | Meaningful names, cohesive functions, named constants and flag arguments |
| Conditionals and control flow | Named boolean expressions, guard clauses and safe evaluation order |
| Error handling | Explicit failures, side effects and resource management |
| Design and abstractions | SRP, DRY, composition, dependency injection and YAGNI |
| Testing and refactoring | Test baselines, regression checks and behavior-preserving refactoring |
| Code review | Review checklist and evidence-based handoff |

Example of context: extract a compound business condition into a named boolean when it communicates intent, but avoid extraction for a trivial comparison or when doing so changes evaluation timing or side effects. Shared security requirements remain in `.bob/rules/`.

## Evaluating rule effectiveness

When asked to assess whether the rules work, compare Bob output with and without them using the same task and model. Check naming, compound-condition clarity, nesting, tests, security, behavioral equivalence and unjustified abstraction. Keep the generated artifacts and exact prompts as evidence; do not assume that loaded rules guarantee compliance.
