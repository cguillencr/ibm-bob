# Rules vs. Skills: decision guide

See [skills.md](skills.md) for formal Bob discovery, scope and approval behavior. This guide is the policy behind the lab's refactoring.

**Rules** are continuously relevant expectations within the appropriate scope (e.g. safe handling of secrets and a Developer's clean-code practices). **Skills** are reusable recipes activated for tasks (e.g. a full code review). **Modes** describe the role and permitted tool groups, while **MCP servers** expose external tools.

A useful litmus test: *Would Bob still need to obey this while doing a different task?* If yes, prefer a rule. *Does this instruction have a beginning, ordered process, output artifact and supporting checklist?* If yes, prefer a skill. Split compound instructions into both layers when necessary.

| Previously bundled information | Decision | Rationale |
|---|---|---|
| Shared SDLC governance, security baseline | Keep shared rules | Applies across workflows |
| Role safety and approval restrictions | Keep mode rules | Must not depend on skill activation |
| Developer clean-code conventions, meaningful naming and named boolean variables | Keep Developer rules | Always-on quality expectations |
| Developer code-review checklist | Keep minimal review standards in rules; add `code-review` skill | Structured, request-triggered deliverable |
| Developer implementation sequence | Retain approval/test expectations in mode; add `feature-implementation` skill | Multi-step repeatable process |
| QA minimum test/defect field contracts | Keep QA rule | Invariant output requirement |
| QA test design and coverage workflow | Add `qa-test-design` skill | On-demand procedure |
| Analyst specification process | Add `requirements-specification` skill | On-demand process with template |
| Support incident triage | Keep read-only restrictions; add `incident-triage` skill | Case-specific investigation |
| SRE readiness and reliability assessment | Keep operational restrictions; add `reliability-review` skill | Structured review |
| Focused security assessment | Keep baseline rule; add `security-review` skill | Standards are universal; audit workflow is not |

Avoid duplicated long checklists in always-loaded rules; do not remove minimum contracts or safety requirements when extracting workflows. Do not claim skill execution proves compliance.
