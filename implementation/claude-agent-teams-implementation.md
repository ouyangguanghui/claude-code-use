# 代理团队实现

![Last Updated](https://img.shields.io/badge/Last_Updated-Mar_12%2C_2026-white?style=flat&labelColor=555)

[← 返回 Claude Code 最佳实践](../)

---

**✅ 已实现**

<p align="center">
  <img src="assets/impl-agent-teams.png" alt="代理团队实战 — 使用 tmux 的分屏模式" width="100%">
</p>

代理团队生成**多个独立的 Claude Code 会话**，通过共享任务列表进行协调。与子代理（单个会话内的隔离上下文分叉）不同，每个队友都获得自己的完整上下文窗口，自动加载 CLAUDE.md、MCP 服务器和技能。

---

## 如何使用

时间编排工作流完全由代理团队构建。运行最终产品：

```bash
cd agent-teams
claude
/time-orchestrator
```

这调用了 **命令 → 代理 → 技能** 管道：代理获取迪拜当前时间，技能将 SVG 时间卡片渲染到 `agent-teams/output/dubai-time.svg`。

---

## 如何实现

你可以使用代理团队创建天气编排工作流的副本 — 在这个示例中，时间编排工作流完全由代理团队构建。

### 1. 安装 [iTerm2](https://iterm2.com/) 和 tmux

```bash
brew install --cask iterm2
brew install tmux
```

### 2. 启动 iTerm2 → tmux → Claude

```bash
tmux new -s dev
CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1 claude
```

### 3. 使用团队结构提示

<a id="time-orchestration"></a>

将以下提示粘贴到 Claude 中，使用代理团队引导完整的时间编排工作流：

主提示：**[agent-teams-prompt.md](../agent-teams/agent-teams-prompt.md)**

### 团队协调流程

```
┌──────────────────────────────────────────────────────────────┐
│                       领导者 (你)                             │
│      "创建一个代理团队来构建时间编排"                           │
└──────────────────────────┬───────────────────────────────────┘
                           │ 生成团队 (全部并行)
              ┌────────────┼────────────┐
              ▼            ▼            ▼
   ┌────────────────┐ ┌──────────┐ ┌──────────────┐
   │ 命令           │ │ 代理     │ │ 技能         │
   │ 架构师         │ │ 工程师   │ │ 设计师       │
   │                │ │          │ │              │
   │ agent-teams/   │ │ agent-   │ │ agent-teams/ │
   │ .claude/       │ │ teams/   │ │ .claude/     │
   │ commands/      │ │ .claude/ │ │ skills/      │
   │ time-          │ │ agents/  │ │ time-svg-    │
   │ orchestrator.md│ │ time-    │ │ creator/     │
   │                │ │ agent.md │ │              │
   └───────┬────────┘ └────┬─────┘ └──────┬───────┘
           │               │              │
           ▼               ▼              ▼
   ┌──────────────────────────────────────────────────┐
   │            共享任务列表                            │
   │  ☐ 约定数据契约: {time, tz, formatted}            │
   │  ☐ 命令使用 Agent 工具 (不是 bash)                │
   │  ☐ 代理预加载 time-fetcher 技能                   │
   │  ☐ 技能从上下文读取时间 (不重新获取)               │
   │  ☐ 所有文件在 agent-teams/.claude/ 内             │
   └──────────────────────────────────────────────────┘
                       │
                       ▼
          ┌──────────────────────────────┐
          │  cd agent-teams && claude    │
          │    /time-orchestrator        │
          │   命令 → 代理 → 技能         │
          └──────────────────────────────┘
```
