# Xcode Agent Skills Sync

Portable integrations for refreshing the skills embedded in the installed Xcode:

```sh
xcrun agent skills export --output-dir <skills-directory> --replace-existing
```

The repository provides a native `/sync-xcode-skills` command for Codex, Claude Code, Gemini CLI, OpenCode, and GitHub Copilot CLI. Each command exports directly to that tool's personal skills directory; no Downloads staging directory is used.

## Requirements

- Xcode 27 or later with `xcrun agent skills export` available.
- The target agent CLI or app.

Confirm that Xcode provides the exporter:

```sh
xcrun agent skills export --help
```

## Install

### Codex

```sh
git clone https://github.com/maniramezan/xcode-agent-skills-sync.git ~/Developer/xcode-agent-skills-sync
codex plugin marketplace add ~/Developer/xcode-agent-skills-sync
codex plugin add xcode-skills-sync@xcode-agent-skills-sync
```

Start a new Codex thread, then use `/sync-xcode-skills`.

Codex marketplaces currently use a local marketplace path, so cloning the repository is the portable installation step.

### Claude Code

```sh
claude plugin marketplace add https://github.com/maniramezan/xcode-agent-skills-sync
claude plugin install xcode-skills-sync@xcode-agent-skills-sync
```

Restart Claude Code, then use `/sync-xcode-skills`.

### Gemini CLI

```sh
gemini extensions install https://github.com/maniramezan/xcode-agent-skills-sync
```

Restart Gemini CLI, then use `/sync-xcode-skills`. Update it after Xcode upgrades with `gemini extensions update xcode-agent-skills-sync`.

### OpenCode

Copy or symlink the included command into OpenCode's global commands directory:

```sh
mkdir -p ~/.config/opencode/commands
ln -s "$(pwd)/adapters/opencode/sync-xcode-skills.md" ~/.config/opencode/commands/sync-xcode-skills.md
```

Restart OpenCode, then use `/sync-xcode-skills`.

### GitHub Copilot CLI

```sh
copilot plugin marketplace add https://github.com/maniramezan/xcode-agent-skills-sync
copilot plugin install xcode-skills-sync@xcode-agent-skills-sync
```

Restart Copilot CLI, then use `/sync-xcode-skills`.

## What gets updated

| Agent | Skills destination |
| --- | --- |
| Codex | `~/.codex/skills` |
| Claude Code | `~/.claude/skills` |
| Gemini CLI | `~/.gemini/skills` |
| OpenCode | `~/.config/opencode/skills` |
| GitHub Copilot CLI | `~/.copilot/skills` |

The exported skills use the standard `SKILL.md` format. Their content remains owned by the installed Xcode; this repository only supplies installation and refresh adapters.

## License

MIT. Xcode-exported skills are not redistributed by this repository.
