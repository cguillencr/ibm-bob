# Extending a Generic Bob SDLC Foundation for Specific Projects

## Objective

**The default repository is technology-agnostic.** It defines common software delivery roles and handoff contracts, not the tools for one technology. Reuse `.bob/custom_modes.yaml`, `.bob/rules-{slug}/`, and relevant `docs/` templates as the baseline in any software project. Add technology-specific capabilities to the **target project**, not to the generic baseline.

## Layers and responsibilities

| Layer | What belongs here | Example |
| --- | --- | --- |
| SDLC foundation | Analyst, Developer, QA, SRE, Support; common quality gates and specs | `.bob/custom_modes.yaml` and `.bob/rules-*` |
| Project specialization | Project/domain-specific skills, coding conventions, reference material | `.bob/skills/`, additional project rules |
| Environment access | MCP servers, source control, CI/CD, testing, observability | Configured separately, least privilege |
| Project artifacts | Requirements, tests, architecture, incidents, evidence | `docs/` or the project's preferred paths |

Bob custom modes identify **who** is performing a task and which tool groups may be used. Skills add **how-to domain expertise**. MCP connects a role to **external systems**. A skill is not automatically an MCP server, and neither a custom mode nor `skill` alone provisions infrastructure or credentials.

## Example: IBM watsonx Orchestrate

Use the official IBM repository as an **optional, separate extension**:

- Skills source: https://github.com/IBM/ibm-watsonx-orchestrate-adk/tree/main/skills
- Official instructions: https://github.com/IBM/ibm-watsonx-orchestrate-adk/blob/main/skills/README.md

As documented in the upstream README, IBM Bob can discover skills placed under `.bob/skills/<skill-name>/` in a project workspace, with each skill containing `SKILL.md`. Alternatively, the **watsonx Orchestrate ADK** extension's *Initialize Workspace* procedure installs the ADK, configures the MCP server and registers curated skills. Confirm behavior with your installed versions and avoid duplicating an existing skills installation.

Suggested skill mappings (our recommendations, **not** automatic IBM assignments):

| Generic Bob mode | Optional upstream skills | Purpose |
| --- | --- | --- |
| Analyst | `solution-architect`, `sop-builder` | Domain-specific architecture and SOPs |
| Developer | `wxo-builder` | Build agent/tool/flow solutions |
| QA | `agent-instructions-evaluator`, `wxo-analyzer` | Agent evaluations and implementation review |
| SRE | `telemetry-analyzer`, `agentic-workflow-advisor` | Observability and workflow design analysis |
| Support | `telemetry-analyzer`, `wxo-analyzer` | Evidence-based incident diagnosis |

Other upstream skills include `customercare-mcp-builder`; choose these only when the project actually needs them. Skill selection may vary by workflow, and one skill can support more than one mode.

### Option A — manual installation in a target project

Copy **selected complete skill directories**, including their `SKILL.md` and supporting references, from the upstream repository into the target project:

```text
my-wxo-project/
└── .bob/
    ├── custom_modes.yaml        # Shared generic SDLC roles
    ├── rules-analyst/
    ├── rules-developer/
    ├── rules-qa/
    ├── rules-sre/
    ├── rules-support/
    └── skills/                  # Optional, project-specific
        ├── solution-architect/
        │   └── SKILL.md
        ├── wxo-builder/
        │   └── SKILL.md
        └── telemetry-analyzer/
            └── SKILL.md
```

The `skill` group is already included in our five custom modes; verify that each skill is discovered and invoked in Bob. Do not assume mapping a skill to a role makes it load only for that role.

### Option B — IBM ADK extension

Follow IBM's [upstream skills README](https://github.com/IBM/ibm-watsonx-orchestrate-adk/blob/main/skills/README.md): install the watsonx Orchestrate ADK extension in Bob, open its panel, use **Initialize Workspace**, and check which skills and MCP integrations it registers. Review generated workspace changes before committing anything. Treat this as the preferred option if you want the full curated setup rather than a small manually curated subset.

## Guardrails for project specialization

1. Decide technology and business requirements before loading specialized assets.
2. Review version/license/trust of external skills and pin a known revision for reproducibility where possible.
3. Use environment-scoped, least-privilege MCP credentials; never commit tokens or `.env` secrets.
4. Record which skills and services were installed, and how they were validated.
5. Keep generic roles and acceptance gates intact. Add specialization without silently replacing the common foundation.
6. Verify the actual impact on Bob responses and record the experiment; do not present proposed workflows as validated features.

## Reproducibility checklist

- [ ] Baseline mode configuration loads in Bob
- [ ] Installed skills are present and discoverable
- [ ] Versions/commit SHAs and installation method recorded
- [ ] MCP permissions and environment boundaries checked
- [ ] Analyst → Developer → QA → SRE/Support handoffs still work
- [ ] Publication material contains no internal/client data or secrets

## MCP servers are project-specific

Add documentation and operational MCP servers only when the target project requires them. For an Orchestrate project, see [`mcp-servers.md`](mcp-servers.md) for the observed two-server pattern and recommended permission gates. The generic starter must not ship active Orchestrate connections.


MCP connections should follow the official Bob global/project scopes, transport and per-tool control guidance in [mcp-servers.md](mcp-servers.md). Never include live credentials in the starter.


The generic starter now contains seven **technology-agnostic** project skills. This does not conflict with the project-specific extension principle: only vendor/stack skills, such as watsonx Orchestrate ADK skills, are installed into specialized projects. Read [skills.md](skills.md) and [rules-vs-skills.md](rules-vs-skills.md). The upstream IBM skills are not bundled in this starter.


### Evaluated ADK skill: agent-instructions-evaluator

A real but anonymized static-evaluation case study is available in [experiments/agent-instructions-evaluator-case-study.md](experiments/agent-instructions-evaluator-case-study.md). The ADK skill is installed only in a project that needs it; it is **not bundled** with this generic SDLC lab. Treat estimated token costs, model-generated scores, and inferred workflow issues as hypotheses pending verification.
