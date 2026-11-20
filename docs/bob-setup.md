# Install in VS Code

1. Open this repository as the workspace in VS Code with IBM Bob installed.
2. In Bob Settings > Modes > Edit Project Modes, inspect `.bob/custom_modes.yaml`.
3. Confirm Analyst, Developer, QA, SRE and Support appear in the mode picker; fix validation errors if any.
4. Inspect `.bob/rules-{mode-slug}/` instructions, loaded alphabetically per IBM documentation.
5. Configure optional MCP servers independently, with scoped credentials and appropriate approvals.
6. Run the permission tests in `docs/permissions-and-integrations.md` before relying on any restriction.

This is a **project-scoped** configuration. For global use, copy and adapt the YAML to `~/.bob/settings/custom_modes.yaml`; project overrides take precedence. Never copy credentials into this repo.

## Discovery: mode registration and project location

Bob's UI creates project-scoped custom modes in `.bob/custom_modes.yaml` under `customModes`, not in `.bob/modes/`. Global modes instead use `~/.bob/settings/custom_modes.yaml`. `docs/` holds reference documentation only, while `.bob/rules-{slug}/` holds instructions loaded automatically for the selected mode. Open the repository root in VS Code and inspect **Settings → Modes → Edit Project Modes**. The five supplied modes still require loading tests in the extension.


## Skills setup

Review `.bob/skills/` and open **Bob Settings → Skills**. The seven project skills should be discoverable from `SKILL.md` front matter. By default, Bob asks permission on activation; **Bob Settings → Auto-Approve → Skills** changes that behavior. The main workflow and security rules remain active even if a skill is not selected. See [skills.md](skills.md).
