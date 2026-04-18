# 代理 vs 命令 vs 技能 — 何时使用哪个

Claude Code 三种扩展机制的比较：子代理、命令和技能。

[← 返回 Claude Code 最佳实践](../)

![斜杠菜单显示 time-skill、time-command 和 time-agent](assets/agent-command-skill-1.jpg)

---

## 概览

| | 代理 | 命令 | 技能 |
|---|---|---|---|
| **位置** | `.claude/agents/<name>.md` | `.claude/commands/<name>.md` | `.claude/skills/<name>/SKILL.md` |
| **上下文** | 独立的子代理进程 | 内联（主对话） | 内联（主对话） |
| **用户可调用** | 没有 `/` 菜单 — 由 Claude 或通过 Agent 工具调用 | 是 — `/command-name` | 是 — `/skill-name`（除非 `user-invocable: false`） |
| **Claude 自动调用** | 是 — 通过 `description` 字段 | 否 | 是 — 通过 `description` 字段（除非 `disable-model-invocation: true`） |
| **接受参数** | 通过 `prompt` 参数 | `$ARGUMENTS`、`$0`、`$1` | `$ARGUMENTS`、`$0`、`$1` |
| **动态上下文注入** | 否 | 是 — `` !`command` `` | 是 — `` !`command` `` |
| **独立上下文窗口** | 是 — 隔离的 | 否 — 共享主对话 | 否 — 共享主对话（除非 `context: fork`） |
| **模型覆盖** | `model:` 前置元数据 | `model:` 前置元数据 | `model:` 前置元数据 |
| **工具限制** | `tools:` / `disallowedTools:` | `allowed-tools:` | `allowed-tools:` |
| **钩子** | `hooks:` 前置元数据 | — | `hooks:` 前置元数据 |
| **记忆** | `memory:` 前置元数据（user/project/local） | — | — |
| **可预加载技能** | 是 — `skills:` 前置元数据 | — | — |
| **MCP 服务器** | `mcpServers:` 前置元数据 | — | — |

---

## 何时使用各机制

### 使用代理的场景：

- 任务是**自主的、多步骤的** — 代理需要自行探索、决策和行动，无需持续指导
- 你需要**上下文隔离** — 工作不应污染主对话窗口
- 代理需要跨会话的**持久化记忆**（例如，一个能学习模式的代码审查员）
- 你想通过技能**预加载领域知识**而不污染主上下文
- 任务适合**在后台运行**或在 **git 工作树**中运行
- 你需要**工具限制**或不同的**权限模式**（例如 `acceptEdits`、`plan`）

**示例**：`weather-agent` — 使用预加载的 `weather-fetcher` 技能自主获取天气数据，在独立上下文中运行并限制工具。

### 使用命令的场景：

- 你需要一个**用户发起的入口点** — 用户显式触发的工作流
- 工作流涉及**编排**其他代理或技能
- 你想**保持上下文精简** — 命令内容在用户触发之前不会注入到会话上下文中

**示例**：`weather-orchestrator` — 用户触发它，它询问摄氏/华氏偏好，调用代理，然后调用 SVG 技能。

### 使用技能的场景：

- 你想让 **Claude 基于用户意图自动调用** — 技能描述会注入到会话上下文中用于语义匹配
- 任务是一个**可复用的过程**，可以从多个地方调用（命令、代理或 Claude 自身）
- 你需要**代理预加载** — 在启动时将领域知识植入特定代理

**示例**：`weather-svg-creator` — 当用户要求天气卡片时 Claude 自动调用它；也可从命令中调用。

---

## 命令 → 代理 → 技能架构

本仓库演示了一种分层编排模式：

```
用户触发 /command
    ↓
命令编排工作流
    ↓
命令调用代理（独立上下文，自主执行）
    ↓
代理使用预加载的技能（领域知识）
    ↓
命令调用技能（内联，用于输出生成）
```

**具体示例** — 天气系统：

```
/weather-orchestrator（命令 — 入口点，询问摄氏/华氏）
    ↓
weather-agent（代理 — 自主获取温度）
    ├── weather-fetcher（代理技能 — 预加载的 API 指令）
    ↓
weather-svg-creator（技能 — 内联创建 SVG）
```

---

## 前置元数据比较

### 代理前置元数据

```yaml
---
name: my-agent
description: Use this agent PROACTIVELY when...
tools: Read, Write, Edit, Bash
model: sonnet
maxTurns: 10
permissionMode: acceptEdits
memory: user
skills:
  - my-skill
---
```

### 命令前置元数据

```yaml
---
description: Do something useful
argument-hint: [issue-number]
allowed-tools: Read, Edit, Bash(gh *)
model: sonnet
---
```

### 技能前置元数据

```yaml
---
name: my-skill
description: Do something when the user asks for...
argument-hint: [file-path]
disable-model-invocation: false
user-invocable: true
allowed-tools: Read, Grep, Glob
model: sonnet
context: fork
agent: general-purpose
---
```

---

## 关键区别

### 自动调用

| 机制 | Claude 能否自动调用？ | 如何阻止 |
|------|---------------------|----------|
| 代理 | 是 — 通过 `description`（使用 "PROACTIVELY" 来鼓励） | 移除或弱化描述 |
| 命令 | 否 — 始终由用户通过 `/` 发起 | 不适用 |
| 技能 | 是 — 通过 `description` | 设置 `disable-model-invocation: true` |

### 在 `/` 菜单中的可见性

| 机制 | 出现在 `/` 菜单中？ | 如何隐藏 |
|------|-------------------|----------|
| 代理 | 否 | 不适用 |
| 命令 | 是 — 始终显示 | 无法隐藏 |
| 技能 | 是 — 默认显示 | 设置 `user-invocable: false` |

### 上下文隔离

| 机制 | 在独立上下文中运行？ | 如何配置 |
|------|-------------------|----------|
| 代理 | 始终 | 内置行为 |
| 命令 | 从不 | 不适用 |
| 技能 | 可选 | 设置 `context: fork` |

---

## 实际案例："现在几点了？"

本仓库为同一任务定义了所有三种机制 — 显示 PKT 的当前时间。当用户输入 **"现在几点了？"** 而不显式调用任何 `/` 命令时，会发生什么：

| 机制 | 会触发吗？ | 原因 |
|------|----------|------|
| `time-command` | 否 | 命令**永远不会自动调用**。用户需要显式输入 `/time-command` 才能运行。命令没有自动发现路径 — 它们严格由用户发起。 |
| `time-agent` | **是**（可能） | 代理的 `description` 说 *"Use this agent to display the current time in Pakistan Standard Time"*。Claude 将其与用户意图匹配，可能通过 Agent 工具生成它。但代理在**独立上下文窗口**中运行，对于这个简单任务来说太重了。 |
| `time-skill` | **是**（最可能） | 技能的 `description` 说 *"Display the current time in Pakistan Standard Time (PKT, UTC+5). Use when the user asks for the current time, Pakistan time, or PKT."* Claude 匹配这个并通过 Skill 工具调用它。由于它**内联运行**且没有上下文开销，是最高效的匹配。 |

### 解析优先级

当多个机制匹配相同意图时，Claude 优先选择满足请求的**最轻量级选项**：

```
1. 技能（内联，无上下文开销）     ← 首选
2. 代理（独立上下文，自主执行）    ← 技能不可用或任务复杂时使用
3. 命令（永远不会 — 需要显式 /）   ← 仅当用户输入 /time-command 时
```

### 如果技能设置了 `disable-model-invocation: true` 会怎样？

那么 Claude **无法**自动调用技能。代理成为唯一可自动调用的选项，因此 Claude 会改为生成 `time-agent` — 代价是为一个单行 bash 命令创建一个独立的上下文窗口。

### 如果技能和代理都禁用了自动调用会怎样？

那么**没有任何机制会自动触发**。Claude 会回退到自己的通用知识，很可能直接运行 `TZ='Asia/Karachi' date` — 不涉及任何扩展机制。用户需要显式输入 `/time-command` 或 `/time-skill` 才能使用。

![当用户问"现在几点了？"时 Claude 自动调用 time-skill](assets/agent-command-skill-2.png)

---

## 来源

- [Claude Code 技能 — 文档](https://code.claude.com/docs/en/skills)
- [Claude Code 子代理 — 文档](https://code.claude.com/docs/en/sub-agents)
- [Claude Code 斜杠命令 — 文档](https://code.claude.com/docs/en/slash-commands)
- [技能最佳实践](../best-practice/claude-skills.md)
- [命令最佳实践](../best-practice/claude-commands.md)
- [子代理最佳实践](../best-practice/claude-subagents.md)
