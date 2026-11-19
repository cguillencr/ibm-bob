# Design and abstractions

- Follow the single-responsibility principle: keep responsibilities that change for different reasons separate when there is a real design benefit.
- Remove duplication of business knowledge, but avoid extracting unrelated coincidental similarities (DRY is not a mandate for premature abstraction).
- Prefer simple composition and small interfaces over inheritance-heavy designs when they fit the problem.
- Introduce dependency injection for external services when it meaningfully improves testing, isolation or replaceability; do not introduce a container/framework for a trivial dependency.
- Follow existing architecture and conventions; propose architectural changes separately with tradeoffs, compatibility impacts and review gates.
- Apply YAGNI: implement current approved requirements, not speculative extensibility.
