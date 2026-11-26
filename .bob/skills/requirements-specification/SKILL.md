---
name: requirements-specification
description: Turn stakeholder requests into traceable, reviewable software requirements and acceptance criteria; use when asked to analyze a feature or write a specification.
---

# Requirements Specification

1. Read stakeholder input and discover existing architecture, constraints, and relevant decisions.
2. Identify ambiguities, assumptions, interfaces, dependencies, privacy requirements, and business rules; ask or explicitly flag decisions rather than fabricate facts.
3. Assign stable requirement IDs, define measurable acceptance criteria (including negative paths), and propose nonfunctional requirements.
4. Write the specification under `docs/specs/` following `templates/spec-template.yaml` (in this skill) where suitable; validate it against `schemas/spec.schema.json` and use `examples/FEAT-001.yaml` as a reference example.
5. Check completeness and testability with `checklist.md`; report open questions and seek approval before handoff to Developer.

Consult `checklist.md` for the final quality gate. Apply shared workspace and relevant mode rules throughout; this skill does not override approval gates or tool permissions.
