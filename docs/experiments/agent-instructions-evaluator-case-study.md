# Field experiment: agent-instructions-evaluator on two agent definitions

**Status:** Static evaluation performed; recommendations not yet implemented or validated at runtime.  
**Privacy:** This is a deliberately anonymized and generalized account of a real project experiment. Names, organizations, paths, tool identifiers, model/provider details, repository identifiers, and exact inventory figures have been removed or generalized. Do not attempt to reconstruct the original system.

## Objective and method

A practitioner used the **official watsonx Orchestrate ADK `agent-instructions-evaluator` skill** to inspect two native agent YAML definitions in a development workspace:

- **Agent A — integration test harness:** a deliberately instruction-free agent exposing a broad collection of enterprise API tools.
- **Agent B — translation prototype:** a minimal agent without bound tools and without explicit behavioral instructions.

The evaluator's extraction script generated JSON inventories; the assistant produced a primary achievability report, a machine-readable evaluation artifact, and three supporting reports addressing token footprint, performance, and reliability. This was **static analysis**, not a live-agent benchmark, security penetration test, or trace-based performance measurement.

The reports included five dimensions: Task Understanding, Scope & Applicability, Execution & Tool Grounding, Instruction Followability, and State & Conflict Manageability. Scores are model judgments, not objective certification. The extraction reported unresolved tool definitions and parsing errors; this limits quantitative confidence.

## Findings: Agent A

| Area | Sanitized observation | Proposed response | Evidence status |
|---|---|---|---|
| Role and scope | The agent intentionally had no instructions, so tool descriptions carried much of the behavioral burden | Keep restricted to development use or define an explicit user-facing role, scope and output contract | Direct static observation; deployment suitability is a recommendation |
| Tool surface | Dozens of bound tools, with overlapping purposes; token footprint estimated in the five-figure range | Test domain partitioning or narrower agents; measure actual context cost | Estimate only; some schemas were unresolved and represented by placeholders |
| High-impact writes | Certain state-changing operations appeared to lack explicit confirmation in the inspected implementation | Verify backend controls, require server-side confirmation and auditability, then consider a deterministic workflow | Partial source inspection; no end-to-end authorization proof |
| Sensitive diagnostic output | A diagnostic helper appeared capable of returning credential material | Remove it from user-facing tools or return safe metadata only; verify exact deployed tool identity | Source-based risk hypothesis; no actual credential exposure demonstrated |
| Context provenance | Tools referenced authorization or localization context not declared in the agent YAML | Document injection contract and verify server-side authorization; never infer privileges from prompts | Static observation; external authorization component not reviewed |
| Multi-step transactions | Several write sequences relied on model-led orchestration | Evaluate deterministic flow orchestration with validation, confirmation and rollback paths | Sequence inferred partly from tool names, not observed traces |

**Important:** An empty instruction field can be intentional for a test harness. It does not prove that a production assistant lacks instructions, or that backend access control is absent. Do not treat the evaluator's severity labels as confirmed vulnerabilities.

## Findings: Agent B

The translation prototype had no bound tools and no explicit instructions. The evaluator identified ambiguous target-language selection, output formatting, and example prompts that did not align with its stated translation purpose. The proposed improvement was a short, explicit instruction block and aligned starter prompts. A zero estimated tool-schema footprint is **not** a zero total token cost.

## Lessons for reproducible experiments

1. Identify the actual agent definition and intended audience before interpreting scores.
2. Confirm extraction uses the deployed tool implementation, not similarly named code in unrelated directories.
3. Separate **observed counts**, **estimated token costs**, **inferred workflow paths**, and **unverified security hypotheses**.
4. Avoid publishing tool names, credential-handling source, customer identifiers, private paths, or sensitive action inventories.
5. Compare the original and revised agent with the same prompt set and model; capture actual tool-selection errors, input tokens, latency, failed operations, and confirmation behavior.
6. Treat agent instructions and skills as guidance, not security boundaries; enforce authorization, confirmation, and audit controls in backend services.
7. Preserve full evidence in an access-controlled internal location; publish only redacted or synthetic examples.

## Next experiment (not yet executed)

Create synthetic Agent A and Agent B fixtures with no enterprise identifiers. Run the evaluator on both, then apply targeted improvements and repeat. Independently verify authorization and confirmation using safe non-production tests. Report measured differences and uncertainty rather than repeating projected percentage savings as fact.

## References

- [IBM watsonx Orchestrate ADK skills](https://github.com/IBM/ibm-watsonx-orchestrate-adk/tree/main/skills)
- [agent-instructions-evaluator](https://github.com/IBM/ibm-watsonx-orchestrate-adk/tree/main/skills/agent-instructions-evaluator)
