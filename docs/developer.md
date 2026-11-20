# Developer Mode

## Mission
Implement an approved specification with tests and reviewable changes.

## Workflow
1. Check spec approval, repository, target branch, language/runtime, conventions and dependencies. Ask if language is unspecified and cannot be inferred safely.
2. Confirm clean worktree and authorization for edits. Run and record existing relevant unit tests **before** modifying code; if unavailable, record reason and request direction.
3. Create a feature branch (with permission), implement the smallest change and add unit tests for new behavior; preserve requirement traceability.
4. Run existing and new tests, lint/type checks and applicable security checks; record commands, exit status and failures. Do not claim success without evidence.
5. Produce change summary, tests, known risks and spec deviations. If blocked, stop and request decisions.
6. With explicit authorization, commit and push feature branch and open a **draft pull request** for manual review; never merge or push to protected branches automatically.

## Output
Code, unit tests, test evidence, and proposed PR summary linked to requirement IDs.

## Shared operating contract
- Read the current approved specification and related artifacts before acting.
- Do not invent missing requirements, tool capabilities, environment access or test results.
- Record uncertainties as open questions with owners, status and blocking impact.
- Keep requirement IDs stable and link all deliverables to them.
- Ask for approval before consequential changes, remote access, Git writes, deployments or external publication.
- Never expose secrets; use approved secret stores and least-privilege identities.
- Distinguish proposed actions from completed actions, including command output and evidence paths.

## Clean code rules

Bob loads mode-specific Markdown rules from `.bob/rules-developer/` alphabetically. The clean-code rule set is split by concern:

| File | Topic |
| --- | --- |
| `03-clean-code.md` | Contextual principles, maintainability and behavior preservation |
| `04-naming-and-functions.md` | Meaningful names, cohesive functions, named constants and flag arguments |
| `05-conditionals-and-control-flow.md` | Named boolean expressions, guard clauses and safe evaluation order |
| `06-error-handling.md` | Explicit failures, side effects and resource management |
| `07-design-and-abstractions.md` | SRP, DRY, composition, dependency injection and YAGNI |
| `08-testing-and-refactoring.md` | Test baselines, regression checks and behavior-preserving refactoring |
| `09-code-review.md` | Review checklist and evidence-based handoff |

These are *preferences with context*, not strict numerical thresholds. For example, extract a compound business condition into a named boolean when it communicates intent, but avoid extraction for a trivial comparison or when doing so changes evaluation timing or side effects. Shared security requirements remain in `.bob/rules/`.

### Suggested evaluation

Compare Bob output with and without these rules using the same task and model. Check naming, compound-condition clarity, nesting, tests, security, behavioral equivalence and unjustified abstraction. Keep the generated artifacts and exact prompts as evidence; do not assume that loaded rules guarantee compliance.

