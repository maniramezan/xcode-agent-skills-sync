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

Codex Agent Skills do not appear in the `/` picker. Use the terminal command:

```sh
codex-sync-xcode-skills
```

Or, in a Codex conversation, send: `Use the sync-xcode-skills skill to refresh my Xcode skills.`

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

### skills.sh

Install the portable `sync-xcode-skills` skill into every supported agent detected on your machine:

```sh
npx skills add maniramezan/xcode-agent-skills-sync --all --global
```

The installer uses symlinks by default, so one managed copy is shared across agents. Use `--copy` if your environment does not support symlinks. `--all --global` can report unsupported global-skill installation for other detected tools (currently Eve and PromptScript); those messages do not affect Codex, Claude Code, Gemini CLI, OpenCode, or GitHub Copilot CLI. In Codex, invoke it with a normal-language request to use the skill or run `codex-sync-xcode-skills`; in agents that register a native slash command, invoke `/sync-xcode-skills`. Refresh the installed skill when this repository changes with:

```sh
npx skills update
```

Because this repository is private, collaborators need GitHub access and a configured GitHub credential (for example, `GH_TOKEN`) before installing through skills.sh.

## What gets updated

| Agent | Skills destination |
| --- | --- |
| Codex | `~/.codex/skills` |
| Claude Code | `~/.claude/skills` |
| Gemini CLI | `~/.gemini/skills` |
| OpenCode | `~/.config/opencode/skills` |
| GitHub Copilot CLI | `~/.copilot/skills` |

The exported skills use the standard `SKILL.md` format. Their content remains owned by the installed Xcode; this repository only supplies installation and refresh adapters.

## Contributing with AI agents

The repository's shared agent contract is [AGENTS.md](AGENTS.md). Claude Code, Gemini CLI, OpenCode, and GitHub Copilot CLI each have a small native guidance entry point that refers to the same contract.

## License

MIT. Xcode-exported skills are not redistributed by this repository.
