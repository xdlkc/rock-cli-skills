# rock-cli-skills

English | [简体中文](./README.zh-CN.md)

A standalone, minimal `rock-cli` skill package ([`SKILL.md`](./SKILL.md) + [`references/sandbox.md`](./references/sandbox.md)) teaching AI coding agents how to operate **ROCK** sandboxes via `rockcli` (`rc`).

- **ROCK (Reinforcement Open Construction Kit)** is Alibaba's sandbox environment management framework built for agentic reinforcement learning and coding-agent evaluation.
- **`rockcli` (`rc`)** is the command-line client for creating, inspecting, debugging, and managing ROCK sandboxes.

> **Language note**: [`SKILL.md`](./SKILL.md) and [`references/sandbox.md`](./references/sandbox.md) are written in Simplified Chinese alongside CLI examples and parameter tables.

## ROCK Skill Ecosystem

`rock-cli-skills` is the lightweight standalone `rock-cli` skill package. Compare the three `xdlkc` ROCK skill repositories before installing:

| Repository | Scope & Included Skills | Packaging & Install Path | Best For |
|---|---|---|---|
| [`rock-marketplace`](https://github.com/xdlkc/rock-marketplace) | Unified `rock` plugin (`v1.4.7`): `rock-cli` (v2.7), `rock-debug`, `rock-agent-debug` (remote + in-sandbox), `rock-eval`, `rock-feedback` | `.claude-plugin/marketplace.json` (`/plugin install rock@rock-marketplace`) & `skills/` symlinks (`npx skills add`) | Most users: full ROCK CLI v2.7 (`agent`, `expr`, `image`, `datasets`), sandbox diagnostics, job debugging, and Harbor regression eval |
| [`rock-agents`](https://github.com/xdlkc/rock-agents) | Two plugins: `rock-agent-sdk` (`v1.0.0`: Python `rock.sdk.agent` & `rock_agent_config.yaml`) and `rock-agent` (`v1.3.0`: in-sandbox `rock-agent-debug`) | `.claude-plugin/marketplace.json` (`/plugin install rock-agent-sdk@rock-agents` & `rock-agent@rock-agents`) & `skills/` symlinks (`npx skills add`) | Developers writing Python SDK / YAML benchmark integrations (`rock-agent-sdk`) or installing `rock-agent` standalone |
| **[`rock-cli-skills`](https://github.com/xdlkc/rock-cli-skills)** *(this repo)* | Standalone `rock-cli` skill (`SKILL.md` + `references/sandbox.md`) covering core sandbox lifecycle, `exec`, `upload`/`download`, `attach`, `log`, `history`, `replay` | Root `SKILL.md` (`npx skills add xdlkc/rock-cli-skills` or manual copy; no `.claude-plugin/` wrapper) | Minimal single-skill install focused solely on core `rockcli` sandbox commands |

## What This Skill Covers

- **Setup & authentication** ([`SKILL.md`](./SKILL.md)): `rockcli` installation/self-update (`rockcli update`), auth priority (`ROCK_API_KEY`, `--api-key`, `~/.rock/setting.json`), and global flags (`--verbose`, `--base-url`, `--cluster`, `-H`/`--extra-header`).
- **Seven core sandbox workflows**:
  1. One-off tasks (`sandbox start --wait-for-alive`, `exec`, `stop`)
  2. Project upload, execution, and result retrieval (`upload --recursive [-a]`, `download`)
  3. Interactive REPL (`sandbox <id> attach`, distinguishing `/exit` vs `/close`)
  4. Log searching and live tailing (`log search --log-file ...`, `log tail`)
  5. API operation history (`sandbox <id> history`)
  6. Request replay (`sandbox <id> replay`)
  7. Lifecycle state inspection (`sandbox <id> status`: `pending` → `alive` → `stopping` → `stopped`)
- **Parameter reference** ([`references/sandbox.md`](./references/sandbox.md)): Flag tables for `start`, `stop`, `exec`, `status`, `upload`, `download`, `attach` REPL slash commands, `log search` (including `--log-file` and time-window/field filters), `log tail`, and `history`.

> Looking for `rockcli` v2.7 subcommands (`agent run/view/fs`, `expr`, `image`, `datasets`, Windows sandboxes)? Install the expanded `rock-cli` skill from [`rock-marketplace`](https://github.com/xdlkc/rock-marketplace).

## Installation

Because this repository places `SKILL.md` directly at the root without a `.claude-plugin/` or `plugins/` marketplace wrapper, install via `skills` CLI or manual copy (use [`rock-marketplace`](https://github.com/xdlkc/rock-marketplace) if you want Claude Code `/plugin marketplace add`):

### Option 1: Vercel Labs `skills` CLI

```bash
# Install globally across detected agents
npx skills add xdlkc/rock-cli-skills -g

# Or install to the current project only
npx skills add xdlkc/rock-cli-skills
```

### Option 2: Manual Clone & Copy

Copy both `SKILL.md` and `references/` into your agent's skill directory:

```bash
git clone https://github.com/xdlkc/rock-cli-skills.git

# Example for Claude Code
mkdir -p ~/.claude/skills/rock-cli
cp -r rock-cli-skills/SKILL.md rock-cli-skills/references ~/.claude/skills/rock-cli/
```

(For Cursor, Codex, or OpenCode, copy into `~/.cursor/skills/rock-cli/`, `~/.codex/skills/rock-cli/`, or `~/.opencode/skills/rock-cli/` respectively.)

## Repository Layout

```text
rock-cli-skills/
├── SKILL.md                # Main `rock-cli` skill definition and workflow playbooks
└── references/
    └── sandbox.md          # Detailed parameter reference for `rockcli sandbox` subcommands
```
