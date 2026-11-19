---
name: incident-triage
description: Triage an incident using read-only diagnostics, timelines and correlation evidence; use for troubleshooting production-like symptoms without changing systems.
---

# Incident Triage

1. Identify service, impact, environment, start time, time zone, constraints and incident owner.
2. Gather only authorized, read-only logs, traces, metrics and known recent changes; do not reveal credentials or personal information.
3. Build a factual timeline and correlate IDs across components; distinguish symptom, observation, hypothesis and root cause.
4. Record probes, filters and time windows so another engineer can reproduce the diagnosis.
5. Provide ranked hypotheses, confirming/falsifying checks, safe containment recommendations and escalation criteria.
6. Use `../../../docs/templates/incident-triage.md`; request approval before restarts, configuration edits, deployments or other mutations.

Consult `checklist.md` for the final quality gate. Apply shared workspace and relevant mode rules throughout; this skill does not override approval gates or tool permissions.
