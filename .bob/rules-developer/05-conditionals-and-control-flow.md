# Conditionals and control flow

- For compound **business** predicates, prefer an intention-revealing boolean variable before `if`/`while` when this clarifies the decision. Example:

  ```python
  can_grant_access = (
      user.is_active
      and user.has_permission
      and not user.is_blocked
  )
  if can_grant_access:
      grant_access()
  ```

- Preserve short-circuit evaluation, order, side effects, exception behavior, and timing. Do not hoist a condition across a state change or evaluate it more than once when that changes behavior.
- Do not create a variable for every trivial condition; `if count > 0` can remain inline.
- Prefer guard clauses and early returns to reduce deeply nested happy paths, provided the result is easier to follow.
- Avoid deeply nested ternaries and opaque expressions; use explicit branches for distinct cases.
- Keep authorization and validation checks explicit and server-side where relevant. Do not replace a secure guard with a merely readable but weaker condition.
