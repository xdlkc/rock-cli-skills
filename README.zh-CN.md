# rock-cli-skills

[English](./README.md) | 简体中文

面向 **ROCK** 沙箱命令行工具 `rockcli`（别名 `rc`）的独立精简技能包（仅包含 [`SKILL.md`](./SKILL.md) 与 [`references/sandbox.md`](./references/sandbox.md)）。

- **ROCK (Reinforcement Open Construction Kit)**：阿里巴巴开发的沙箱环境管理框架，专为 Agentic 强化学习与 Coding Agent 评测场景设计。
- **`rockcli` (`rc`)**：用于启停、连接、调试与管理 ROCK 沙箱的命令行客户端。

## ROCK Skill 生态对比

本仓库为单技能独立包。安装前可先对照 `xdlkc` 下三个 ROCK 技能仓库的定位差异：

| 仓库 | 定位与包含技能 | 分发与安装方式 | 适用人群 |
|---|---|---|---|
| [`rock-marketplace`](https://github.com/xdlkc/rock-marketplace) | 统一 `rock` 插件（`v1.4.7`）：`rock-cli`（v2.7）、`rock-debug`、`rock-agent-debug`（远程 + 沙箱内）、`rock-eval`、`rock-feedback` | `.claude-plugin/marketplace.json`（`/plugin install rock@rock-marketplace`）及顶层 `skills/` 软链（`npx skills add`） | 绝大多数用户：需要完整 ROCK CLI v2.7（`agent`/`expr`/`image`/`datasets`）、沙箱排查、Job 调试与 Harbor 回归评测 |
| [`rock-agents`](https://github.com/xdlkc/rock-agents) | 两个独立插件：`rock-agent-sdk`（`v1.0.0`：Python `rock.sdk.agent` 与 `rock_agent_config.yaml`）与 `rock-agent`（`v1.3.0`：沙箱内 `rock-agent-debug`） | `.claude-plugin/marketplace.json`（`/plugin install rock-agent-sdk@rock-agents` 与 `rock-agent@rock-agents`）及顶层 `skills/` 软链（`npx skills add`） | 需要编写 Python SDK / YAML 评测配置的开发者（`rock-agent-sdk`）或需单独安装 `rock-agent` 的场景 |
| **[`rock-cli-skills`](https://github.com/xdlkc/rock-cli-skills)** *(本仓库)* | 单技能独立包（`SKILL.md` + `references/sandbox.md`），聚焦 `rockcli` 核心沙箱生命周期、`exec`、上传下载、`attach`、`log`、`history`、`replay` | 根目录 `SKILL.md`（`npx skills add xdlkc/rock-cli-skills` 或手动复制；无 `.claude-plugin/` 包装） | 仅需 `rockcli` 沙箱核心操作、希望最小化单技能安装的用户 |

## 技能覆盖内容

- **安装与认证配置**（[`SKILL.md`](./SKILL.md)）：`rockcli` 安装与 `rockcli update` 升级、认证优先级（`ROCK_API_KEY`、`--api-key`、`~/.rock/setting.json`）与全局选项（`--verbose`、`--base-url`、`--cluster`、`-H`/`--extra-header`）。
- **七类核心沙箱场景**：
  1. 快速体验 / 一次性任务（`sandbox start --wait-for-alive`、`exec`、`stop`）
  2. 上传代码 → 执行 → 下载结果（`upload --recursive [-a]`、`download`）
  3. 交互式开发（`sandbox <id> attach` REPL，区分 `/exit` 与 `/close`）
  4. 排查问题 / 日志检索与实时追踪（`log search --log-file ...`、`log tail`）
  5. 回溯操作历史（`sandbox <id> history`）
  6. 请求回放复现（`sandbox <id> replay`）
  7. 查看沙箱状态与生命周期流转（`sandbox <id> status`：`pending` → `alive` → `stopping` → `stopped`）
- **详细参数手册**（[`references/sandbox.md`](./references/sandbox.md)）：`start`、`stop`、`exec`、`status`、`upload`、`download`、`attach` REPL 内置命令、`log search`（含 `--log-file` 与时间窗/字段过滤参数）、`log tail` 与 `history` 的完整参数表。

> 如需 `rockcli` v2.7 的进阶子命令（`agent run/view/fs`、`expr`、`image`、`datasets`、Windows 沙箱）以及排查/评测技能，请改用 [`rock-marketplace`](https://github.com/xdlkc/rock-marketplace)。

## 安装

本仓库将 `SKILL.md` 直接放在根目录，不包含 `.claude-plugin/` 或 `plugins/` 插件市场包装（若需通过 Claude Code `/plugin marketplace add` 安装，请使用 [`rock-marketplace`](https://github.com/xdlkc/rock-marketplace)）。

### 方式一：Skills CLI

```bash
# 全局安装到所有已检测到的 Agent 工具
npx skills add xdlkc/rock-cli-skills -g

# 或仅安装到当前项目
npx skills add xdlkc/rock-cli-skills
```

### 方式二：手动克隆并复制

将 `SKILL.md` 与 `references/` 一同复制到目标工具的技能目录：

```bash
git clone https://github.com/xdlkc/rock-cli-skills.git

# Claude Code 示例
mkdir -p ~/.claude/skills/rock-cli
cp -r rock-cli-skills/SKILL.md rock-cli-skills/references ~/.claude/skills/rock-cli/
```

（若用于 Cursor、Codex 或 OpenCode，可分别复制到 `~/.cursor/skills/rock-cli/`、`~/.codex/skills/rock-cli/` 或 `~/.opencode/skills/rock-cli/`。）

## 仓库结构

```text
rock-cli-skills/
├── SKILL.md                # `rock-cli` 技能主文件与核心使用场景
└── references/
    └── sandbox.md          # `rockcli sandbox` 子命令参数详表
```
