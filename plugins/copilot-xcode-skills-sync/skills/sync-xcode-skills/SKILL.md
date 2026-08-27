---
name: sync-xcode-skills
description: Export the installed Xcode's embedded skills directly into GitHub Copilot CLI's global skills directory.
user-invocable: true
disable-model-invocation: true
---

# Sync Xcode Skills

Run `mkdir -p "$HOME/.copilot/skills" && xcrun agent skills export --output-dir "$HOME/.copilot/skills" --replace-existing`.

Report the names of the exported skills. If the command fails, report the error and stop. Do not edit a repository as part of this command.
