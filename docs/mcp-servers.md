# MCP servers: project-specific integrations

## Principle

The SDLC starter remains technology-agnostic. **Custom Modes** define responsibilities and available tool groups; **custom rules** define behavior; **skills** provide specialized procedural knowledge; **MCP servers** connect Bob to external systems and APIs. A mode's `mcp` group is not a fine-grained permission or authorization boundary. Real authorization must be enforced by server credentials, tool policies, environment controls, and human approvals.

Do **not** install watsonx Orchestrate MCP servers in this generic starter. Configure them in a particular project after reviewing its needs and trust boundaries. The project-local Bob MCP configuration is `.bob/mcp.json`, as observed in the example workspace. Actual connection commands, arguments, URLs and credentials vary by installation; this repository intentionally does not invent a working MCP configuration.

## Official IBM Bob MCP configuration

The primary reference is the IBM Bob **Understanding MCP** and **Using MCP in Bob** documentation, not the Marketplace page. Marketplace discovery is optional; Bob does not ship with preinstalled MCP servers.

MCP is a standardized client-server protocol using JSON-RPC 2.0. Bob can connect to local and remote servers, whose tools extend its capabilities without changing Bob's core.

| Scope | Configuration file | Behavior |
|---|---|---|
| Global | `~/.bob/settings/mcp.json` | Applies across workspaces |
| Project | `.bob/mcp.json` | Applies to the current workspace; project entries override global entries with the same server name |

In **Bob Settings → MCP**, use **Edit Global MCP** or **Edit Project MCP**. Both files use a JSON object named `mcpServers`. Team-shareable configuration must not contain secrets; use environment variables or secure credential stores and ignore any secret-bearing local configuration.

### Supported transports

- **STDIO**: local process launched using `command`, optional `args`, `cwd`, `env`, `alwaysAllow`, `disabled`, and `protocolNegotiation`. Default negotiation: `legacy`.
- **Streamable HTTP**: remote endpoint using `type: "streamable-http"`, `url`, optional `headers`, `alwaysAllow`, `disabled`, and `protocolNegotiation`. Default negotiation: `auto`.

A minimal *illustrative*, disabled local server entry (not a working Orchestrate recipe):

```json
{
  "mcpServers": {
    "example-local": {
      "command": "node",
      "args": ["server.js"],
      "disabled": true,
      "alwaysAllow": []
    }
  }
}
```

Do not paste API keys or bearer tokens into version-controlled JSON. Configure authentication through an approved secret mechanism appropriate to the server.

### Protocol negotiation and compatibility

- `auto`: probes discovery before initialization; default for HTTP.
- `legacy`: initializes without the discovery probe; default for STDIO and a documented troubleshooting option for HTTP discovery timeouts.
- `{ "pin": "2024-11-05" }`: requests a specific supported version.

The official IBM Bob documentation lists protocol versions `2025-11-25`, `2025-06-18`, `2025-03-26`, `2024-11-05`, and `2024-10-07` as supported, and says `2026-07-28` is not yet supported. Bob negotiates the highest mutually supported version unless configured otherwise. Verify this list against the installed Bob release before relying on it.

### Managing capabilities and context

In **Settings → MCP**:

1. Toggle **Use MCP Servers** to enable or disable all MCP use. Disabling removes MCP tool definitions and related instructions from the system prompt.
2. Toggle **Enable MCP Server Creation** separately. Turning it off removes MCP-server-authoring instructions while preserving the ability to use configured servers.
3. Expand a server to enable only the individual tools needed. Disabling unused tools reduces context-window consumption.
4. Manage each server's enable/disable state, restart, deletion, and response timeout (30 seconds to 5 minutes; default 1 minute).
5. Auto-approval is **off by default** and requires both the global **Use MCP servers** auto-approval setting and the per-tool **Always allow** setting. Avoid auto-approving mutations, credential changes, production operations, or destructive tools.

Bob detects available MCP tools and normally proposes their use for approval. When building your own server, provide clear tool names, descriptions, parameter types, prerequisites and expected outcomes.

### Optional marketplace discovery

The Bob Marketplace, under **Settings → MCP**, is one possible way to discover and install community servers. You can also build an MCP server with an SDK or configure an approved server directly. Marketplace installation does not replace server vetting, tool selection or security review.

## Example specialization: watsonx Orchestrate

The following are **user-observed examples from a specific project**, not defaults of the starter or an exhaustive list of required integrations.

| Server | Observed version | Role | Example capabilities |
|---|---|---|---|
| `watsonx-orchestrate-adk-docs` | 1.0.0 | Documentation access | `search_ibm_watsonx_orchestrate_adk`, `query_docs_filesystem_ibm_watsonx_orchestrate_adk`, `submit_feedback`; `orchestrate` resource/skill |
| `watsonx-orchestrate-adk` | 2.14.5 | Orchestrate operations | List, import, create/update and remove agents and tools; manage connections, knowledge bases, models, channels, environments and skills |

Both were reported as connected with **workspace scope**, with configuration stored in `<project>/.bob/mcp.json`. The documentation server's query tool is described as read-only and limited to a virtualized documentation filesystem. The operational ADK server includes **mutating and destructive tools**, e.g. `create_or_update_agent`, `remove_agent`, `remove_tool`, `set_credentials_connection`, `reset_developer_edition_server`, and `activate_environment`. In the captured UI, tools were set to **Always allow**; this is an observed configuration, **not** our recommended security posture. The screenshots/text do not establish a complete, reproducible `mcp.json` connection recipe.

## Recommended access policy

| Mode | Typical MCP use | Recommended gate |
|---|---|---|
| Analyst | Search documentation, inspect requirements | Read-only; no deployments |
| Developer | Query docs, inspect tools; propose imports/updates | Human approval before creating/updating remote resources |
| QA | Read metadata and test results; run approved tests | Use non-production environments and test identities |
| SRE | Read telemetry, inspect health and deployments | Production read-only by default; incident changes via change process |
| Support | Search docs and collect diagnostics | Read-only; redact secrets and personal data |

A custom mode with `mcp` access can potentially see more than one MCP server. Do not assume that mode-specific rules can prevent a privileged tool call. Use per-environment credentials, server-side RBAC, separate read-only and write-capable connections, tool approval settings and auditing. Do not treat **Always allow** as suitable for destructive operations.

## Adoption checklist

1. Identify what information or action the project actually needs; avoid installing servers speculatively.
2. Verify server provenance, version, maintenance and transport/authentication model.
3. Document tool inventory and distinguish read, write, destructive and credential-changing actions.
4. Scope credentials and environments; avoid production access unless justified.
5. Disable unused tools to reduce context usage; review both global and per-tool auto-approval, and redact secrets, tokens, customer information and internal paths.
6. Validate connectivity with read-only tools first.
7. Test write workflows in a sandbox with explicit human approval and rollback plan.
8. Document configuration changes, owners, updates and removal process.

## Skills versus MCP tools

The IBM watsonx Orchestrate ADK [skills repository](https://github.com/IBM/ibm-watsonx-orchestrate-adk/tree/main/skills) is a separate optional layer. Installing a skill does not itself establish a remote connection or authorize deployment. An MCP server can also expose resources or tools for fetching skills; the ADK MCP example exposes `list_available_skills`, `fetch_skill`, and `fetch_all_skills`.

## Sources and verification

- Official IBM Bob MCP documentation: https://bob.ibm.com/docs/ide/configuration/mcp/understanding-mcp and https://bob.ibm.com/docs/ide/configuration/mcp/mcp-in-bob
- Optional Marketplace discovery: https://bob.ibm.com/docs/ide/configuration/marketplace
- User-provided Bob MCP settings inventory (two servers; versions and tools above)
- Public IBM watsonx Orchestrate ADK skills: https://github.com/IBM/ibm-watsonx-orchestrate-adk/tree/main/skills

**Status:** documentation of observed settings and proposed controls. No MCP server was installed, connected, or tested by this repository update.

## MCP threat model

Remote servers may receive sensitive prompts or code; verify data handling and retention. Local STDIO servers can access files, environment variables, and system resources with process permissions. Vet the publisher, inspect source and permissions, test in isolation, and maintain an approved-server inventory.
