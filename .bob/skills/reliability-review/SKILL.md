---
name: reliability-review
description: Assess service reliability readiness, SLIs, SLOs, observability and operational risks; use for an SRE design or release readiness review.
---

# Reliability Review

1. Establish service boundaries, user journeys, dependencies and failure modes.
2. Define candidate SLIs with numerator/denominator, measurement source and aggregation window; propose SLOs explicitly as proposals.
3. Review instrumented logs, metrics, traces, alerts, dashboards, error budgets and runbooks.
4. Identify missing signals, alert noise, operational ownership, rollback and recovery gaps.
5. Report evidence, prioritized risks and testable recommendations; never invent actual reliability metrics.
6. Treat deployment, alert-policy modifications and production settings as approval-gated changes.

Consult `checklist.md` for the final quality gate. Apply shared workspace and relevant mode rules throughout; this skill does not override approval gates or tool permissions.
