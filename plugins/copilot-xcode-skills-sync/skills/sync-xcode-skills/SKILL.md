---
name: sync-xcode-skills
description: Export the installed Xcode's embedded skills into the current agent's global skills directory.
user-invocable: true
disable-model-invocation: true
---

# Sync Xcode Skills

Identify the current agent, then run exactly one corresponding command:

| Agent | Command |
| --- | --- |
| Codex | `mkdir -p "$HOME/.codex/skills" && xcrun agent skills export --output-dir "$HOME/.codex/skills" --replace-existing` |
| Claude Code | `mkdir -p "$HOME/.claude/skills" && xcrun agent skills export --output-dir "$HOME/.claude/skills" --replace-existing` |
| Gemini CLI | `mkdir -p "$HOME/.gemini/skills" && xcrun agent skills export --output-dir "$HOME/.gemini/skills" --replace-existing` |
| OpenCode | `mkdir -p "$HOME/.config/opencode/skills" && xcrun agent skills export --output-dir "$HOME/.config/opencode/skills" --replace-existing` |
| GitHub Copilot CLI | `mkdir -p "$HOME/.copilot/skills" && xcrun agent skills export --output-dir "$HOME/.copilot/skills" --replace-existing` |

If the agent cannot be identified, ask the user which destination they intend to update. Report the names of the exported skills. If the command fails, report the error and stop. Do not edit a repository as part of this command.
