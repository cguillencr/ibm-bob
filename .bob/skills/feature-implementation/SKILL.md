---
name: feature-implementation
description: Implement an approved software feature using a test-first, evidence-backed workflow; use when asked to build or modify behavior.
---

# Feature Implementation

1. Locate the approved specification and match requirement IDs to existing code; stop or flag missing approval or scope.
2. Inspect existing project conventions and run baseline tests if available; record evidence.
3. Create or update focused unit tests for intended behavior before or alongside implementation; keep tests for edge and error paths.
4. Implement the smallest coherent change following Developer rules; extract meaningful boolean conditions only when doing so improves readability without altering evaluation behavior.
5. Run relevant tests and regression checks, collect exit status and failures; update related documentation.
6. Summarize changed files, requirement IDs, test evidence, limitations and needed approvals. Never commit, push, create PRs or deploy without explicit authorization.

Consult `checklist.md` for the final quality gate. Apply shared workspace and relevant mode rules throughout; this skill does not override approval gates or tool permissions.
