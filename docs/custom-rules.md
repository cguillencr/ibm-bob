# IBM Bob custom rules — configuration and precedence

## Source of truth
Based on IBM Bob IDE Custom Rules documentation supplied during this project. Rules are **instructions**, not a deterministic security enforcement mechanism.

## Supported scopes
- Global: `~/.bob/rules/` (Linux/macOS) or `%USERPROFILE%\.bob\rules\` (Windows), applies to all projects.
- Workspace general: `.bob/rules/`, applies to all modes in the open workspace.
- Workspace mode-specific: `.bob/rules-{mode-slug}/`, applies to the matching mode.
- Mode `customInstructions` in `.bob/custom_modes.yaml` are combined with mode-specific rule files.
- Root `AGENTS.md` is automatically loaded by default; can be disabled with `bob-code.useAgentRules: false`.

## Precedence and loading
Documentation describes global rules followed by workspace rules, with workspace rules able to override global ones. Mode-specific rules load before general rules at each level. `AGENTS.md` is loaded after mode-specific rules but before general workspace rules. Avoid relying on ambiguous conflicts: make requirements consistent and test the behavior in Bob.

Rule directories are read recursively; files load alphabetically by filename; empty and common cache files are ignored. Symbolic links have a documented maximum depth of 5.

## Design
- `.bob/rules/01-sdlc-governance.md`: cross-role process, approvals and evidence.
- `.bob/rules/02-security-baseline.md`: portable security defaults.
- `.bob/rules-{slug}/`: role-specific behavior, including clean code and QA artifact contracts.
- `docs/`: human-readable reference and templates; not auto-loaded merely because they are in docs.

## Validation checklist
1. Open the repository root in VS Code.
2. Open Bob Settings → Modes → Edit Project Modes and confirm `.bob/custom_modes.yaml` is loaded.
3. Select each mode and request a task that exercises its specific rule.
4. Test an intentional rule conflict only in a disposable workspace; observe effective precedence.
5. Record actual behavior, model/version and evidence. Do not claim rule compliance solely from configuration.

## Developer clean-code rules

The generic Developer mode uses topical files `03-clean-code.md` through `09-code-review.md` in `.bob/rules-developer/`. Bob loads the directory alphabetically and combines it with the mode's `customInstructions`. These rules are language-agnostic; project-specific conventions can be added at workspace level. They emphasize intention-revealing named boolean expressions, guard clauses, meaningful naming, cohesive functions, explicit error handling, sensible abstractions, safe refactoring and review evidence.

See the [`code-review` skill](../.bob/skills/code-review/SKILL.md) and [the evaluation plan](experiments/evaluation-plan.md). Do not interpret guidance as absolute rules or proof of correctness.


## Workflows belong in skills

Keep durable policy and style expectations in rules; use `.bob/skills/<name>/SKILL.md` plus optional supporting files for task-triggered procedures. See [rules-vs-skills.md](rules-vs-skills.md) and [skills.md](skills.md).
