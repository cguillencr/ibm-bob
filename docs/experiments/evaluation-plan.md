# Baseline and evaluation plan

For each role, test the same task with default Bob and with the custom mode. Repeat multiple times with identical repo state and model/settings.

Track: requirement coverage, unanswered-question capture, invalid assumptions, adherence to approval gates, runnable tests, test pass/fail, evidence completeness, time to review, and manual corrections.

Do not publish unmeasured improvement claims. Log Bob version, model, prompt, repository commit, allowed tools, duration, outcomes and evaluator notes. Sanitize all records.


## Clean-code A/B experiment

Use the same model, codebase, task, prompt and available tools for two runs: A without the developer clean-code rules, B with `.bob/rules-developer/03-*.md` through `09-*.md`. Preserve prompts, code diffs, test commands and outputs. Assess: (1) named compound business predicates, (2) reduced nesting, (3) intention-revealing names, (4) cohesion, (5) error handling, (6) needless abstraction, (7) test evidence, and (8) semantic equivalence. Score each as observed / not observed / not applicable, and record counterexamples. Do not claim causality or guaranteed compliance from a single run.


## Experiment: Rules vs. Skills (planned)

Compare identical prompts in disposable copies with (A) Custom Modes + rules only and (B) Custom Modes + rules + seven generic skills. Record skill discovery and activation, default approval prompt, which checklist was used, answer completeness, verified test evidence, irrelevant instructions, and human approval compliance. Test project/global name collision separately. Do not infer improvements without baseline data.


## ADK agent-instructions-evaluator field study

See [agent-instructions-evaluator-case-study.md](agent-instructions-evaluator-case-study.md). The completed step was static extraction and report generation; proposed refactoring, live execution, performance comparison, and security verification remain pending. Use synthetic agent fixtures for public demonstrations.

## Mode comparison: synthetic banking MCP project

See [banking-mcp-mode-comparison.md](banking-mcp-mode-comparison.md) for three exploratory runs and a proposed controlled replication. Do not equate context occupancy with cumulative token consumption, or task-list creation with completed implementation.
