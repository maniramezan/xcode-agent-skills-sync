---
description: Export the installed Xcode's embedded skills directly into Claude Code's global skills directory.
---

# Sync Xcode Skills

Run `mkdir -p "$HOME/.claude/skills" && xcrun agent skills export --output-dir "$HOME/.claude/skills" --replace-existing`.

Report the names of the exported skills. If the command fails, report the error and stop. Do not edit a repository as part of this command.
