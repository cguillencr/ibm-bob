# Errors, state and side effects

- Catch errors at a layer that can meaningfully handle them. Catch specific exceptions; never silently swallow failures or return a success-shaped result after failure.
- Preserve useful diagnostic context without logging secrets, credentials, personal information or sensitive payloads.
- Use typed errors or documented error contracts where supported. Distinguish recoverable errors from programming defects.
- Make side effects visible in names, APIs and documentation. Prefer pure transformations when practical; isolate I/O and external dependencies to improve testability.
- Separate queries from state-changing commands where doing so clarifies behavior; avoid surprising mutations in getters.
- Ensure resources are closed and partial failures handled appropriately; use transactions or compensating actions where required by the project.
