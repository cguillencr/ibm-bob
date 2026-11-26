# IBM Bob SDLC Lab

A **technology-agnostic foundation for any software project**, built with five experimental, project-scoped IBM Bob Custom Modes, persistent rules and seven optional task skills for VS Code. It offers reusable, machine-readable SDLC artifacts and separate Medium publication drafts. Add technology-specific skills, rules, integrations and tooling **only in the target project**.

## Design principle: generic foundation + optional project extensions

This repository is a reusable starting point, **not** a watsonx Orchestrate project and not a framework tied to a language, cloud, or vendor. Every project starts with the same Analyst, Developer, QA, SRE and Support responsibilities. Choose project-specific skills, MCP servers, build tools and operational connections after examining its technology and security requirements.

For example, in a watsonx Orchestrate project, install the [official IBM watsonx Orchestrate ADK skills](https://github.com/IBM/ibm-watsonx-orchestrate-adk/tree/main/skills) in that project (or initialize with the ADK extension); do not add them to this starter by default. See [docs/project-specialization.md](docs/project-specialization.md).

## Quick start

1. Open this directory in VS Code with IBM Bob.
2. Open Bob Settings > Modes > Edit Project Modes and load `.bob/custom_modes.yaml`.
3. Inspect mode-specific instructions in `.bob/rules-{slug}/`, and review the seven project skills under `.bob/skills/` in Bob Settings → Skills.
4. Read `docs/mcp-servers.md` and `docs/permissions-and-integrations.md`; configure any MCP servers **only in the target project**.
5. Test capabilities and boundaries before connecting real repositories or environments.
6. For a specific stack, follow `docs/project-specialization.md` to add optional skills and MCP integrations.

## Roles

Analyst (specifications and decisions) → Developer (implementation and unit tests) → QA (product verification) → SRE (reliability and RCA); Support collects diagnostic evidence and escalates to SRE. Every handoff uses approved, traceable artifacts.

## Layout

- `.bob/custom_modes.yaml`: IBM Bob project mode definitions
- `.bob/rules-*/`: mode-specific rules loaded alphabetically
- `docs/`: project documentation, including evaluation plans, experiments and project extension guidance
- `docs/permissions-and-integrations.md`: least-privilege permission matrix and MCP design
- `medium/`: public English article drafts and editorial notes
- `.bob/skills/`: seven **generic** task-specific Bob skills (`SKILL.md` plus `checklist.md`, and optional `templates/`, `schemas/` and `examples/`); technology/vendor skills are intentionally absent

## Skills and Rules vs. Skills

The starter now includes seven generic project skills: requirements specification, feature implementation, code review, QA test design, security review, incident triage and reliability review. Skills activate by description and, by default, require Bob approval; a skill is not a new permission boundary. Review [docs/skills.md](docs/skills.md) and [docs/rules-vs-skills.md](docs/rules-vs-skills.md) for the official configuration model, migration matrix and examples. For watsonx Orchestrate projects, add [IBM ADK skills](https://github.com/IBM/ibm-watsonx-orchestrate-adk/tree/main/skills) separately.

## Important caveats

The YAML and skill front matter follow the official IBM Bob documentation. The seven skills have been validated structurally but not activated in Bob. It has been parsed locally but **not loaded or executed inside IBM Bob**. MCP servers are not installed by these files. `fileRegex` controls Bob's edit tool group, not terminal/MCP writes. Never publish confidential IBM/client details or secrets. Explicit human approval is required for external writes and production actions.

## Custom rules
Shared workspace rules live in `.bob/rules/`; role-specific rules in `.bob/rules-{slug}/`. See `docs/custom-rules.md`. The Developer clean-code convention and QA test/defect contracts are implemented as rules. A portable security baseline and its proposed assessment experiment are documented in `docs/security-rule-experiment.md`.

## Developer clean-code extension

The generic Developer mode includes seven focused, language-agnostic rule files under `.bob/rules-developer/` (`03`–`09`). They cover named boolean conditions, guard clauses, meaningful naming, cohesive functions, error handling, design principles, testing, refactoring and code review. See the [`code-review` skill](.bob/skills/code-review/SKILL.md) and the draft [`medium/articles/11-teaching-bob-clean-code.md`](medium/articles/11-teaching-bob-clean-code.md). These are contextual guidelines, not guarantees or substitutes for tests and human review.

## MCP server extension model

The starter intentionally ships **without** `.bob/mcp.json` or preinstalled MCP servers. Project-specific connections are described in [`docs/mcp-servers.md`](docs/mcp-servers.md), including the two complementary watsonx Orchestrate ADK examples, global/project configuration, STDIO and Streamable HTTP, protocol negotiation, per-tool controls, approval boundaries and a validation checklist. See the draft [`medium/articles/12-mcp-servers-project-specific.md`](medium/articles/12-mcp-servers-project-specific.md).

## Advanced features — not yet explored

Lifecycle Hooks, Telemetry Data and Carbon Modes are **research backlog items**, not implemented or verified features of this starter. See [docs/advanced-features-backlog.md](docs/advanced-features-backlog.md) for official links, research questions and proposed safe experiments. Future Medium article briefs are in [medium/future-advanced-features.md](medium/future-advanced-features.md). Do not describe these as tested until evidence is collected.


### Field experiment: official ADK evaluator skill

An anonymized, real-world static evaluation of two agent definitions is documented in [`docs/experiments/agent-instructions-evaluator-case-study.md`](docs/experiments/agent-instructions-evaluator-case-study.md). The accompanying English Medium draft is [`medium/articles/17-field-notes-evaluating-agent-instructions.md`](medium/articles/17-field-notes-evaluating-agent-instructions.md). The case study is intentionally generalized to protect private project information; reported performance improvements are **not measured**.

### Field experiment: mode comparison

A three-run banking MCP prototype study comparing built-in Agent, Analyst and Developer is documented in [`docs/experiments/banking-mcp-mode-comparison.md`](docs/experiments/banking-mcp-mode-comparison.md). The English Medium draft is [`medium/articles/18-field-notes-agent-vs-analyst-vs-developer.md`](medium/articles/18-field-notes-agent-vs-analyst-vs-developer.md). Results are exploratory and not normalized benchmarks.
