---
description: Export the installed Xcode's embedded skills directly into OpenCode's global skills directory.
---

Run `mkdir -p "$HOME/.config/opencode/skills" && xcrun agent skills export --output-dir "$HOME/.config/opencode/skills" --replace-existing`.

Report the names of the exported skills. If the command fails, report the error and stop. Do not edit a repository as part of this command.
