
# CLAUDE.md

本文件为 Claude Code (claude.ai/code) 在处理本仓库代码时提供指导。

## 仓库概览

这是一个关于 Claude Code 配置的最佳实践仓库，演示了技能 (Skills)、子代理 (Subagents)、钩子 (Hooks) 和命令 (Commands) 的模式。它作为一个参考实现，而非实际的应用代码库。

## 核心组件

### 天气系统 (工作流演示)
通过 **命令 → 代理 → 技能 (Command → Agent → Skill)** 架构演示了两种不同的技能模式：
- `/weather-orchestrator` 命令 (`.claude/commands/weather-orchestrator.md`)：入口点 —— 询问用户摄氏度/华氏度，调用代理，然后调用 SVG 技能。
- `weather-agent` 代理 (`.claude/agents/weather-agent.md`)：使用其预加载的 `weather-fetcher` 技能获取温度（代理技能模式）。
- `weather-fetcher` 技能 (`.claude/skills/weather-fetcher/SKILL.md`)：预加载到代理中 —— 包含从 Open-Meteo 获取温度的指令。
- `weather-svg-creator` 技能 (`.claude/skills/weather-svg-creator/SKILL.md`)：技能 —— 创建 SVG 天气卡片，写入 `orchestration-workflow/weather.svg` 和 `orchestration-workflow/output.md`。

两种技能模式：代理技能 (通过 `skills:` 字段预加载) vs 普通技能 (通过 `Skill` 工具调用)。完整的流程图见 `orchestration-workflow/orchestration-workflow.md`。

### 技能定义结构
`.claude/skills/<name>/SKILL.md` 中的技能使用 YAML 前置元数据 (frontmatter)：
- `name`: 显示名称和 `/斜杠命令` (默认为目录名)。
- `description`: 何时调用 (建议用于自动发现)。
- `argument-hint`: 自动补全提示 (例如 `[issue-number]`)。
- `disable-model-invocation`: 设置为 `true` 以防止自动调用。
- `user-invocable`: 设置为 `false` 以从 `/` 菜单中隐藏 (仅作为背景知识)。
- `allowed-tools`: 技能激活时允许使用的工具，无需权限提示。
- `model`: 技能激活时使用的模型。
- `context`: 设置为 `fork` 以在隔离的子代理上下文中运行。
- `agent`: `context: fork` 时的子代理类型 (默认: `general-purpose`)。
- `hooks`: 作用域限于此技能的生命周期钩子。

### 演示系统 (Presentation System)
参见 `.claude/rules/presentation.md` —— 演示工作被委派给 `presentation-vibe-coding` (针对 `presentation/vibe-coding-to-agentic-engineering/`) 或 `presentation-learning-journey` (针对 `presentation/learning-journey/`)。

### 钩子系统 (Hooks System)
位于 `.claude/hooks/` 的跨平台声音通知系统：
- `scripts/hooks.py`: Claude Code 钩子事件的主处理器。
- `config/hooks-config.json`: 团队共享配置。
- `config/hooks-config.local.json`: 个人覆盖配置 (已加入 git-ignore)。
- `sounds/`: 按钩子事件组织的音频文件 (通过 ElevenLabs TTS 生成)。

在 `.claude/settings.json` 中配置的钩子事件：PreToolUse, PostToolUse, UserPromptSubmit, Notification, Stop, SubagentStart, SubagentStop, PreCompact, SessionStart, SessionEnd, Setup, PermissionRequest, TeammateIdle, TaskCompleted, ConfigChange。

特殊处理：git commit 会触发 `pretooluse-git-committing` 声音。

## 关键模式

### 子代理编排 (Subagent Orchestration)
子代理 **不能** 通过 bash 命令调用其他子代理。请使用 Agent 工具 (在 v2.1.63 中从 Task 更名为 Agent；`Task(...)` 仍作为别名可用)：
```
Agent(subagent_type="agent-name", description="...", prompt="...", model="haiku")
```

在子代理定义中要明确工具的使用。避免使用像 "launch" 这样可能被误解为 bash 命令的模糊术语。

### 子代理定义结构
`.claude/agents/*.md` 中的子代理使用 YAML 前置元数据：
- `name`: 子代理标识符。
- `description`: 何时调用 (使用 "PROACTIVELY" 表示自动调用)。
- `tools`: 工具白名单，用逗号分隔 (省略则继承全部)。支持 `Agent(agent_type)` 语法。
- `disallowedTools`: 要禁用的工具，从继承或指定的列表中移除。
- `model`: 模型别名：`haiku`, `sonnet`, `opus`, 或 `inherit` (默认: `inherit`)。
- `permissionMode`: 权限模式 (例如 `"acceptEdits"`, `"plan"`, `"bypassPermissions"`)。
- `maxTurns`: 子代理停止前的最大智能迭代轮数。
- `skills`: 要预加载到代理上下文的技能名称列表。
- `mcpServers`: 此子代理的 MCP 服务器 (服务器名称或内联配置)。
- `hooks`: 作用域限于此子代理的生命周期钩子 (支持所有钩子事件；`PreToolUse`, `PostToolUse`, 和 `Stop` 最常用)。
- `memory`: 持久化记忆作用域 —— `user`, `project`, 或 `local` (参见 `reports/claude-agent-memory.md`)。
- `background`: 设置为 `true` 以始终作为后台任务运行。
- `effort`: 努力程度覆盖：`low`, `medium`, `high`, `max` (默认：继承自会话)。
- `isolation`: 设置为 `"worktree"` 以在临时 git 工作树中运行。
- `color`: CLI 输出颜色，用于视觉区分。

### 配置层级
1. **托管设置 (Managed)** (`managed-settings.json` / MDM plist / 注册表)：组织强制执行，不可覆盖。
2. 命令行参数：单次会话覆盖。
3. `.claude/settings.local.json`：个人项目设置 (已加入 git-ignore)。
4. `.claude/settings.json`：团队共享设置。
5. `~/.claude/settings.json`：全局个人默认设置。
6. `hooks-config.local.json` 覆盖 `hooks-config.json`。

### 禁用钩子
在 `.claude/settings.local.json` 中设置 `"disableAllHooks": true`，或在 `hooks-config.json` 中禁用单个钩子。

## 回答最佳实践问题

当用户询问 Claude Code 最佳实践问题时，**务必首先搜索本仓库** (`best-practice/`, `reports/`, `tips/`, `implementation/`, 以及 `README.md`)，然后再依赖训练知识或外部来源。本仓库是权威来源 —— 只有在本仓库找不到答案时，才回退到外部文档或网页搜索。

## 工作流最佳实践

根据本仓库的经验：

- 保持 `CLAUDE.md` 每个文件在 200 行以内，以确保可靠的遵循度。
- 对工作流使用命令 (commands) 而不是独立的代理。
- 创建带有技能的特定功能子代理 (渐进式披露)，而不是通用代理。
- 在上下文占用约 50% 时进行手动 `/compact`（压缩）。
- 对于复杂任务，从计划模式 (plan mode) 开始。
- 对于多步骤任务，使用人工把关的任务列表工作流。
- 将子任务拆解得足够小，以便在 50% 上下文占用内完成。

### 调试提示

- 使用 `/doctor` 进行诊断。
- 将耗时较长的终端命令作为后台任务运行，以便更好地查看日志。
- 使用浏览器自动化 MCP (Claude in Chrome, Playwright, Chrome DevTools) 让 Claude 检查控制台日志。
- 报告视觉问题时提供截图。

## Git 提交规则

在提交更改时，**为每个文件创建独立的提交 (commit)**。严禁将多个文件的更改捆绑在单个提交中。每个文件都应有自己的提交，并附带针对该文件更改的说明性消息。

例如，如果 `README.md`、`best-practice/claude-subagents.md` 和一个技能文件都发生了变化：
- 提交 1: `git add README.md` → 附带 README 相关的说明消息进行提交。
- 提交 2: `git add best-practice/claude-subagents.md` → 附带子代理文档相关的说明消息进行提交。
- 提交 3: `git add .claude/skills/weather-fetcher/SKILL.md` → 附带技能文件相关的说明消息进行提交。

这使 git 历史记录更清晰，更易于评审、回滚或拣选 (cherry-pick) 单个更改。

## 文档

文档标准参见 `.claude/rules/markdown-docs.md`。关键文档：
- `best-practice/claude-subagents.md`: 子代理元数据、钩子和仓库代理。
- `best-practice/claude-commands.md`: 斜杠命令模式和内置命令参考。
- `orchestration-workflow/orchestration-workflow.md`: 天气系统流程图。