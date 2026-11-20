# Field notes: banking MCP prototype across Bob modes

**Date:** 2026-11-19  
**Status:** Three runs observed; no controlled benchmark and no complete runtime validation supplied.  
**Environment:** IBM Bob SDLC Lab, local project workspace. Only synthetic/in-memory banking data is in scope.  
**Privacy:** Task identifiers and local workspace identifiers are intentionally omitted from public notes.

## Research question

Does choosing a Bob custom mode change the scope and type of work performed when requesting an in-memory banking MCP server (transfers, service payments, deposits) and a teller agent? Does the default Agent mode automatically route through Analyst?

## Run log (observed)

| Run | Starting mode | Prompt/input | Context length at observation | Window occupancy | Bobcoins shown | Known output |
|---|---|---|---:|---:|---:|---|
| A | Built-in Agent | Original broad project request | 8.8k / 270k | 3% | 1.64 | Output not supplied; no evidence of Analyst invocation was seen by the operator |
| B | Analyst custom mode | Original broad project request, separate run | 37.1k / 270k | 14% | 0.264 | Two draft YAML feature specifications; no implementation reported |
| C | Developer custom mode | Broad request plus explicit references to the two specifications; new thread, specs retained | 88.0k / 270k | 33% | 3.04 | Seven-item implementation task list; completed code, tests and execution results not supplied |

**Measurement caveat:** Context Length is the observed context occupancy, **not cumulative input/output token usage**. Bobcoins are UI-reported usage units, not a direct quality score or a normalized per-task cost. Values cannot establish which mode is intrinsically more efficient: tasks, inputs, histories and outcomes differ.

## Analyst deliverables

The Analyst generated two files under `docs/specs/`:

- `FEAT-001-banking-mcp-server.yaml`: an in-memory, synthetic-data MCP banking server, including transfer, payment and deposit mutations; read-only capabilities; structured errors; atomicity; logging; acceptance criteria; and blocking product decisions.
- `FEAT-002-teller-agent.yaml`: a conversational teller consuming the MCP tools, with parameter collection, explicit confirmation before mutations, error handling, test cases and open architectural questions.

Both specifications were marked **blocked**. FEAT-001 had unresolved decisions about language/SDK, transport, currency/limits, and identity/authorization. FEAT-002 had unresolved decisions about the teller's form factor and intended audience. Proposed defaults are not approvals. FEAT-002 explicitly listed `next_role: developer` but its handoff said **NOT VERIFIED**, with blockers still open.

## Developer task list (reported, not verified as completed)

1. Read both specifications and obtain approval for proposed TypeScript/defaults.
2. Inspect repository conventions and baseline tests.
3. Scaffold TypeScript, configuration and Vitest.
4. Write tests and implement in-memory banking logic, errors and idempotency.
5. Implement MCP tools, annotations, logging and structured errors.
6. Register the MCP server in project `.bob/mcp.json` without auto-approving mutations; document setup.
7. Add a Spanish teller Bob custom mode and its documentation.

**Do not infer that any task was completed** merely because it appears in the task list. The provided evidence does not establish tests passing, working MCP connectivity, or teller behavior.

## Interpretation and open hypotheses

- **Observed:** Explicitly selecting Analyst produced requirements artifacts only. Explicitly selecting Developer with those artifacts produced an implementation plan.
- **Not established:** That the default Agent mode attempted, skipped, or was capable of automatic mode switching. Its detailed trace was not supplied.
- **Hypothesis:** Mode selection influences the deliverable boundary, while cross-mode handoffs require explicit instructions, automation or manual coordination. Test this instead of assuming it.
- **Potential governance gap:** The Developer plan correctly lists approval as its first task, but the specifications are still blocked. Verify that no implementation proceeds before blocking decisions are resolved and approval is recorded.
- **Architecture choice:** The Analyst left open whether the teller is a Bob custom mode, an Orchestrate agent or a standalone application. The Developer task list proposes a Bob mode; that is not evidence that the decision was approved.

## Follow-up protocol

Use the same clean repository snapshot, same model/settings and a recorded Bob version. Repeat the same prompt with each starting mode. Preserve mode selection, timestamps, prompt text, artifact diffs, approvals, tool/skill invocations, and task completion state. Record both context occupancy and actual token totals **only if exposed**. Add a fourth controlled run that explicitly requires Analyst approval before Developer. Compare requirement coverage, blocker handling, tests, elapsed time, tool usage and Bobcoins; do not treat context length as cumulative token consumption.

### Banking safety checklist for follow-up

Use synthetic accounts only; do not expose a network service or real banking credentials. Verify server-side authorization if any real users are ever introduced. For mutations, require explicit user confirmation plus server-side validation and replay protection; never rely solely on agent text or tool-approval settings. A timeout after a write means the outcome may be **unknown**, not necessarily failed; check transaction status before any retry.

## Editorial use

This note supports Medium article 18. Avoid publishing task IDs, local workspace identifiers, private paths or full project source. The banking scenario is synthetic, and the observed Bob figures are from three non-equivalent executions.
