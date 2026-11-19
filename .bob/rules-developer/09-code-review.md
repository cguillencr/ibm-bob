# Developer self-review before handoff

- Review changed code for meaningful naming, cohesive functions, understandable conditions, unnecessary nesting, duplication, magic values, error handling and side effects.
- Check security, compatibility, test coverage and observability implications; explicitly list unverified items.
- Avoid unrelated formatting or cleanup in focused changes unless approved.
- Report requirement IDs, changed files, decisions, tests run with results, known limitations and any follow-up recommendations.
- Do not commit, push, open PRs, deploy or merge without the required human authorization; a clean-code review does not replace human review.

For a complete structured review with severity-graded findings, use the `.bob/skills/code-review/` skill. This file sets developer-wide expectations; the skill defines the task-specific checklist and output.
