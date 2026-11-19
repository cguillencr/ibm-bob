# Tests and safe refactoring

- Before changing existing behavior, inspect relevant tests and run a baseline when feasible; record commands and results, or why it was not possible.
- Add focused tests for new behavior, edge cases, error paths and meaningful security boundaries; prioritize observable behavior over implementation details.
- Use the repository's established testing tools and patterns unless a change is approved.
- During refactoring, preserve public contracts and observable behavior. Keep behavior changes and refactoring in separately reviewable commits or clearly identified changes where feasible.
- After changes, run relevant unit/regression tests, static checks and applicable security checks; do not claim a check passed unless executed and evidenced.
- Do not add brittle tests only to increase coverage percentages. Explain uncovered risks.
