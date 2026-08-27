---
description: Export the installed Xcode's embedded skills directly into Codex's global skills directory.
---

# Sync Xcode Skills

Run `mkdir -p "$HOME/.codex/skills" && xcrun agent skills export --output-dir "$HOME/.codex/skills" --replace-existing`.

Report the names of the exported skills. If the command fails, report the error and stop. Do not edit a repository as part of this command.
