# Agent Guide

This repository distributes integration metadata and slash-command adapters that refresh the agent skills embedded in the locally installed Xcode. It does not distribute the exported Xcode skills themselves.

## Sources of truth

1. The installed Xcode's `xcrun agent skills export` output defines the skills being refreshed.
2. `README.md` defines the supported agents and their user installation flows.
3. This file defines contributor expectations for every AI coding agent.

## Scope

- Keep native support for Codex, Claude Code, Gemini CLI, OpenCode, and GitHub Copilot CLI.
- Each `/sync-xcode-skills` adapter must export directly to that agent's personal skills directory using `xcrun agent skills export --replace-existing`.
- Do not stage exports in Downloads or another shared temporary location.
- Do not add Xcode-exported `SKILL.md` content to this repository. It is generated locally by each user's Xcode installation.
- Keep the command focused: it must not modify the current project or perform unrelated development work.

## Compatibility rules

- Preserve the plugin and marketplace identifiers: `xcode-agent-skills-sync` and `xcode-skills-sync`.
- When adding an agent, add its native package/command, installation instructions, target skills path, and validation coverage together.
- Use the target agent's documented extension format; do not make one agent depend on another agent's configuration directory.
- Keep all manifests valid JSON and use the same release version where the host requires one.

## Validation

Before committing adapter changes:

1. Parse every JSON manifest with `jq empty`.
2. Validate the Codex plugin with `python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/plugin-creator/scripts/validate_plugin.py" plugins/codex-xcode-skills-sync` when Codex is installed.
3. Validate the Claude plugin with `claude plugin validate plugins/claude-xcode-skills-sync` when Claude Code is installed.
4. Run `git diff --check`.
5. Update `README.md` whenever installation, compatibility, or destination paths change.

## Security

- Assume `xcrun agent skills export` may overwrite skills with matching names in its destination; state that behavior clearly in user-facing documentation.
- Never embed credentials, user data, or machine-specific absolute paths in a distributed manifest or command.
- Do not add hooks, MCP servers, or automatic execution beyond the user-invoked sync command without explicit approval.

## Tool-specific entry points

`CLAUDE.md`, `GEMINI.md`, `.github/copilot-instructions.md`, and `.opencode/AGENTS.md` deliberately refer back to this guide. Update them only when the canonical filename or the shared contributor contract changes.
