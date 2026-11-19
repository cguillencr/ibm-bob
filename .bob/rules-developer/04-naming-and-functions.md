# Naming and cohesive functions

- Choose intention-revealing names that reflect domain meaning, units, and purpose; avoid ambiguous abbreviations, misleading names and unnecessary encoding of types.
- Name booleans as predicates such as `is_ready`, `has_permission`, or `can_publish`; keep naming idiomatic for the language.
- Make each function perform one cohesive task at one level of abstraction. Extract distinct responsibilities when that improves comprehension or testability; do not enforce arbitrary line limits.
- Keep argument lists comprehensible. When several related values travel together, consider a small typed value object rather than a long positional parameter list.
- Avoid boolean flag arguments that select unrelated behaviors when separate intention-revealing operations would be clearer (e.g. `generate_detailed_report()` vs `generate_report(True)`).
- Replace unexplained domain literals with named constants or configuration; do not extract universally obvious values without a reason.
- Prefer comments that explain *why*, constraints and tradeoffs. Remove stale or redundant comments that merely restate the code; document public APIs according to repository conventions.
