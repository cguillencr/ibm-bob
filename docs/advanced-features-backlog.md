# Advanced IBM Bob Features — Exploration Backlog

**Status: Not yet explored or validated in this lab.** The maintainer has not used these capabilities extensively. This document records research questions and proposed experiments, **not** confirmed behavior or configuration instructions.

The three links below point to the official IBM Bob documentation. Their contents were not independently reviewed when this backlog was prepared. Follow the official documentation before attempting setup.

| Feature | Official documentation | Lab status | Research goal |
| --- | --- | --- | --- |
| Lifecycle Hooks | [Lifecycle Hooks](https://bob.ibm.com/docs/ide/configuration/lifecycle-hooks) | Research pending | Understand supported events, execution order, configuration, and failure handling |
| Telemetry Data | [Telemetry Data](https://bob.ibm.com/docs/ide/configuration/telemetry-data) | Research pending | Identify available signals, collection controls, privacy boundaries, and export options |
| Carbon Modes | [Carbon Modes Overview](https://bob.ibm.com/docs/ide/configuration/carbon-modes/overview) | Research pending | Understand the product's definition of Carbon Modes, supported configuration, and how it relates to the existing five custom SDLC modes |

## Proposed experiments (not executed)

### Lifecycle Hooks

1. Read the official page and record Bob version, supported hook events, exact configuration format and permissions.
2. Set up a harmless hook in an isolated demo workspace, with no external writes or secrets.
3. Exercise an event, capture invocation order and outcome; repeat with a deliberate failure.
4. Check whether hooks can support automated quality checks without bypassing approval gates.

### Telemetry Data

1. Review the official page to determine exactly what Bob collects and which settings control it.
2. Use synthetic code and prompts only; identify any privacy, retention or opt-in considerations.
3. Record which measurements can actually be accessed and how to export them, if supported.
4. Evaluate whether they help compare the SDLC modes and rules. Do not assume telemetry includes token usage, traces, or performance metrics until verified.

### Carbon Modes

1. Read the official overview and identify its terminology and relationship, if any, to custom modes.
2. Reproduce a minimal documented example in a disposable workspace.
3. Compare configuration, behavior and restrictions with the lab's custom Analyst/Developer/QA/SRE/Support modes.
4. Record whether the feature is useful for the generic starter or should remain optional.

## Evidence required before claiming support

For each experiment capture: date, Bob version, source documentation revision or access date, isolated setup, exact configuration (sanitized), prompts, expected behavior, observed behavior, screenshots or logs without sensitive information, limitations and a rollback procedure.

**Publication gate:** Do not publish a tutorial with commands, screenshots, results or claims of successful implementation until the corresponding experiment has been completed and reviewed. Keep proprietary/internal documentation content out of public articles; use permitted public descriptions and links where appropriate.
