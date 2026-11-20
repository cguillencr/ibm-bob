# Role permissions and integration plan

Based on IBM Bob Custom Modes documentation provided on 2026-11-18. Tool groups are **capability grants**, not individual MCP server permissions. Configure MCP server access, credentials and authorization separately; verify behavior in your Bob version.

| Mode | read | edit | execute | mcp | skill | todo | subtask | workflow | subagent | mode |
|---|---|---|---|---|---|---|---|---|---|---|
| Analyst | Yes | Specs/architecture only | No | No (optional read-only design references) | Yes | Yes | Yes | No | No | No |
| Developer | Yes | Code + tests (unrestricted edit group) | Yes | Yes, conditional Git integration | Yes | Yes | Yes | No | No | No |
| QA | Yes | QA docs only | Yes | Yes, conditional test environment | Yes | Yes | No | No | No | No |
| SRE | Yes | SRE docs/spec contributions | No | Yes, conditional telemetry read-only | Yes | Yes | Yes | No | No | No |
| Support | Yes | Incident/support docs | No | Yes, conditional diagnostic read-only | Yes | Yes | No | No | No | No |

## Integration contracts (not automatically installed)

- **Developer Git MCP**: optional, for branches/PRs. Prefer least-privilege repository-scoped token; require explicit approval before commit, push, branch creation, PR creation or merge. Git CLI via `execute` is an alternative. Git provider MCP must be configured separately. Developer edit permission is broad because source/test paths vary across repositories; enforce scope by review and repo policy.
- **QA environment MCP**: optional, scoped to test/staging only, preferably read-only for discovery and narrowly authorized test actions. Store credentials in secret manager or local ignored `.env`; `.env` itself is not a permission boundary. Separate credentials for execution and observation. Evidence must include timestamps, environment, build, expected/actual results, artifact references.
- **SRE observability MCP**: optional, read-only access to metrics, traces, logs, dashboards and service inventory; define SLI/SLO in specs, propose instrumentation changes for Developer. Production alert/dashboard changes need approval.
- **Support diagnostics MCP**: optional, read-only environment diagnostics and trace/log collection. Do not grant shell, restart, deploy or secrets access by default. Support collects evidence; SRE owns RCA and reliability policy.
- **Analyst**: optionally use a read-only documentation/architecture MCP in a later version, only if source provenance and confidentiality are controlled.

## Permission caveats

1. `groups: [mcp]` enables MCP tools generally; the provided docs do not establish per-server allowlists in Custom Modes. Validate server-level access controls independently.
2. `fileRegex` restricts the **edit tool group** only; it does not restrict `read`, `execute`, or MCP access. The Developer and QA execute tools can write through shell commands; permissions must be enforced externally.
3. File path regex matching semantics must be tested in the actual extension. Suggested paths are repository-relative and may require adjustment.
4. No `allowedSubagents` configured because preset names are unknown; `subagent`, `workflow`, and `mode` are deliberately omitted until orchestration is tested.
5. Do not expose secrets, client data, internal IBM documentation, or internal service URLs in public articles.

## Recommended experiments

For each mode test: (a) authorized task succeeds, (b) unauthorized edit/tool attempt is blocked, (c) missing dependency is reported, (d) approvals are requested, (e) artifact handoff is machine-readable. Capture Bob version, effective YAML, observed behavior and redacted screenshots.

## Project MCP servers

See [`mcp-servers.md`](mcp-servers.md) for the marketplace workflow, Orchestrate example and the distinction between `mcp` group availability and server-side authorization.
