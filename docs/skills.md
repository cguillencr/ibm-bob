# IBM Bob Skills: official behavior and lab design

Primary source: IBM Bob Skills documentation (https://bob.ibm.com/docs/ide/features/skills). The technical details in this document come from the official IBM Bob documentation. Our project workflow mappings are design choices, not documented platform guarantees.

## What a Skill is

A skill is a reusable, task-specific instruction set. Bob chooses whether it is relevant using the required `description`; skills without descriptions are ignored. Bob loads the activated skill's instructions and can read supporting files in the directory. Skills load **once per conversation**, avoiding duplicated prompts. **By default, Bob asks permission before activating a skill.** To change this, open **Bob Settings → Auto-Approve → Skills**. Use the **Skills** settings tab to verify discovery and location.

## Storage and precedence

| Scope | Path | Priority |
|---|---|---|
| Workspace | `<project>/.bob/skills/<skill-name>/SKILL.md` | Wins on same-name conflict |
| Global | `~/.bob/skills/<skill-name>/SKILL.md` | Shared across workspaces |

Every `SKILL.md` begins with YAML front matter containing `name` and a meaningful `description`, followed by Markdown task instructions. Supporting checklists, examples, templates, and scripts are permitted in subfolders. Keep `SKILL.md` focused; use supporting files for long references. Scripts may require separate tool permissions and should not be assumed safe merely because a skill references them.

Example:

```markdown
---
name: code-review
description: Review changes for correctness, security and tests when requested to review code.
---
1. Inspect the diff and requirements.
2. Identify confirmed findings and potential risks separately.
3. Return severity, file location and recommended remediation.
```

## Rules vs. Skills: an operational decision

**Rule = a policy or default behavior that should apply whenever its scope is active.** **Skill = a procedure Bob should load only when a matching task occurs.** They complement rather than replace each other.

| Question | Put it in Rules | Put it in Skills |
|---|---|---|
| Should this apply to every relevant coding task? | Yes: descriptive names, meaningful booleans, error handling, baseline security | No |
| Does it describe ordered steps with a task-specific deliverable? | Only durable boundaries, not every step | Yes: feature implementation, code review, incident triage |
| Is the content long, with checklists and templates? | Only minimal mandatory contract | Yes: supporting files |
| Must it restrict external writes or production changes? | Yes: persistent approvals and constraints | Reinforce them, never treat skill activation as authorization |
| Is it a technology-specific procedure? | Only if necessary to that project | Usually a project skill, e.g. wxO builder |

**Examples:**
- Developer rule: *prefer a well-named boolean for a complex business condition when it improves clarity and preserves semantics*. Developer skill: *implement an approved feature with tests, run validation and report evidence*.
- QA rule: *every test case needs Description, Steps and Expected result; every defect needs Description, Steps to reproduce, Actual result and Expected result*. QA skill: *derive and document test coverage from a requirement spec*.
- Shared security rule: *do not leak secrets; require approval for production changes*. Security skill: *conduct a structured security assessment and report severity-backed findings*.

## Bundled reusable project skills in this lab

| Skill folder | Primary task | Likely mode (not enforced) |
|---|---|---|
| `requirements-specification` | Requirements and acceptance criteria | Analyst |
| `feature-implementation` | Approved implementation with unit/regression tests | Developer |
| `code-review` | Structured diff/code review | Developer / QA |
| `qa-test-design` | Test case and defect design | QA |
| `security-review` | Evidence-based defensive security review | Developer / QA |
| `incident-triage` | Read-only incident investigation | Support / SRE |
| `reliability-review` | SLIs, SLOs, observability and readiness | SRE |

Modes and skills are independent; these mappings describe how we expect to use them, not an enforced routing mechanism. Bob selects by descriptions and task context, subject to approval settings. Do not auto-enable global skill approval on behalf of a team.

## Specialization: IBM watsonx Orchestrate ADK

For a watsonx Orchestrate project, add relevant skills from the [IBM ADK skills repository](https://github.com/IBM/ibm-watsonx-orchestrate-adk/tree/main/skills) into that **project's** `.bob/skills/`, or use the official IBM extension's Initialize Workspace workflow. The upstream repository currently lists: `solution-architect`, `sop-builder`, `wxo-builder`, `wxo-analyzer`, `telemetry-analyzer`, `agent-instructions-evaluator`, `customercare-mcp-builder`, `agentic-workflow-advisor`. Their implementations and licenses remain upstream; this generic lab does not vendor copies. Check upstream versions, source, package requirements and skill permissions before use. An MCP server and an ADK skill are distinct capabilities; installing one does not imply the other is enabled.

## Validation plan (not yet executed in Bob)

1. Open the repository in IBM Bob and inspect **Settings → Skills**. Confirm seven local project skills are visible.
2. Try a clearly matching prompt with auto-approval disabled. Observe the approval prompt and activation.
3. Try an unrelated prompt and confirm no unnecessary skill activation.
4. Verify the expected supporting checklist becomes available and the proper output contract is followed.
5. Compare with a session that has no project skills using identical tasks and collect qualitative evidence.
6. Test project/global same-name precedence in a disposable workspace. Record observed behavior instead of claiming an unperformed test passed.

## Notes

Skills add instructions, not executable permission boundaries. Persistent role rules and human approvals still apply, and scripts or MCP actions need their own controls. No skill is claimed to have been tested live in IBM Bob; this repository is a starting configuration and test plan.
