# Clean code — developer operating principles

- Optimize for maintainability, correctness, and clarity rather than clever brevity. Follow the existing language and repository conventions unless a change is approved.
- Treat these practices as contextual heuristics, not arbitrary line-count or class-count quotas. Explain justified exceptions.
- Preserve observable behavior during refactoring. Do not silently combine behavior changes and structural cleanup.
- Before substantial refactoring, establish a relevant test baseline; afterward rerun tests and report evidence or gaps.
- Apply shared security requirements from `.bob/rules/` in addition to these developer-specific practices.
- Read the topical rules in this directory; avoid duplicating the same requirements in code or reports.
