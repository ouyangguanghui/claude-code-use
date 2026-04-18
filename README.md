# Claude Code 最佳实践

一个关于 Claude Code 配置的最佳实践仓库，演示了技能 (Skills)、子代理 (Subagents)、钩子 (Hooks)、命令 (Commands) 和编排工作流的模式。作为参考实现，帮助你快速掌握 Claude Code 的核心概念和高级用法。

---

## 核心概念

Claude Code 的配置体系由以下核心组件构成：

| 概念 | 说明 | 最佳实践 | 实现示例 |
|------|------|----------|----------|
| **Settings** | 60+ 配置项 + 175+ 环境变量，6 层优先级体系 | [claude-settings.md](best-practice/claude-settings.md) | [settings.json](.claude/settings.json) |
| **Commands** | 斜杠命令 — 可重复工作流的入口点 | [claude-commands.md](best-practice/claude-commands.md) | [实现](implementation/claude-commands-implementation.md) |
| **Skills** | 可复用知识模块 — 预加载或按需调用 | [claude-skills.md](best-practice/claude-skills.md) | [实现](implementation/claude-skills-implementation.md) |
| **Subagents** | 专用子代理 — 并行、隔离、可编排 | [claude-subagents.md](best-practice/claude-subagents.md) | [实现](implementation/claude-subagents-implementation.md) |
| **Memory** | CLAUDE.md + 自动记忆系统 | [claude-memory.md](best-practice/claude-memory.md) | — |
| **MCP** | Model Context Protocol 服务器集成 | [claude-mcp.md](best-practice/claude-mcp.md) | — |
| **Power-Ups** | Hooks、MCP 和高级功能增强 | [claude-power-ups.md](best-practice/claude-power-ups.md) | — |
| **CLI 启动参数** | 命令行标志与环境变量 | [claude-cli-startup-flags.md](best-practice/claude-cli-startup-flags.md) | — |
| **Agent Teams** | 多代理团队协作 | — | [实现](implementation/claude-agent-teams-implementation.md) |
| **Scheduled Tasks** | 定时任务（CronCreate / /loop） | — | [实现](implementation/claude-scheduled-tasks-implementation.md) |

---

## 项目结构

```
claude-code-best-practice/
├── CLAUDE.md                          # 项目指令文件（Claude Code 启动时自动加载）
├── README.md                          # 本文件
│
├── best-practice/                     # 最佳实践文档（8 篇）
│   ├── claude-settings.md             #   设置配置
│   ├── claude-commands.md             #   斜杠命令
│   ├── claude-skills.md               #   技能系统
│   ├── claude-subagents.md            #   子代理
│   ├── claude-memory.md               #   记忆系统
│   ├── claude-mcp.md                  #   MCP 集成
│   ├── claude-power-ups.md            #   高级功能增强
│   └── claude-cli-startup-flags.md    #   CLI 启动参数
│
├── implementation/                    # 实现示例文档（5 篇）
│   ├── claude-commands-implementation.md
│   ├── claude-skills-implementation.md
│   ├── claude-subagents-implementation.md
│   ├── claude-agent-teams-implementation.md
│   └── claude-scheduled-tasks-implementation.md
│
├── reports/                           # 深度分析报告（9 篇）
│   ├── claude-advanced-tool-use.md    #   高级工具使用
│   ├── claude-agent-command-skill.md  #   Agent vs Command vs Skill 对比
│   ├── claude-agent-memory.md         #   代理记忆机制
│   ├── claude-agent-sdk-vs-cli-system-prompts.md
│   ├── claude-global-vs-project-settings.md
│   ├── claude-in-chrome-v-chrome-devtools-mcp.md
│   ├── claude-skills-for-larger-mono-repos.md
│   ├── claude-usage-and-rate-limits.md
│   └── llm-day-to-day-degradation.md
│
├── tips/                              # 实用技巧（9 篇）
│   ├── claude-boris-*.md              #   Boris（Claude Code 工程师）的技巧
│   └── claude-thariq-*.md             #   Thariq（Anthropic CEO）的技巧
│
├── tutorial/                          # 教程
│   ├── claude-code-zero-to-mastery.md #   从零到精通完整教程
│   ├── day0/                          #   Day 0: 环境安装
│   └── day1/                          #   Day 1: 入门实践
│
├── .claude/                           # Claude Code 配置目录
│   ├── settings.json                  #   项目设置
│   ├── agents/                        #   子代理定义
│   │   ├── weather-agent.md           #     天气代理（演示）
│   │   ├── time-agent.md              #     时间代理（演示）
│   │   ├── presentation-*.md          #     演示文稿专用代理
│   │   └── workflows/                 #     工作流代理
│   ├── commands/                      #   斜杠命令
│   │   ├── weather-orchestrator.md    #     天气编排命令（演示）
│   │   ├── time-command.md            #     时间命令（演示）
│   │   └── workflows/                 #     工作流命令
│   ├── skills/                        #   技能定义
│   │   ├── weather-fetcher/           #     天气获取技能
│   │   ├── weather-svg-creator/       #     天气 SVG 生成技能
│   │   ├── time-skill/                #     时间技能
│   │   ├── agent-browser/             #     浏览器自动化技能
│   │   └── presentation/             #     演示文稿相关技能
│   ├── hooks/                         #   钩子系统
│   │   ├── scripts/hooks.py           #     钩子事件处理器
│   │   ├── config/                    #     钩子配置
│   │   └── sounds/                    #     声音通知文件
│   └── rules/                         #   项目规则
│
├── orchestration-workflow/            # 编排工作流演示
│   ├── orchestration-workflow.md      #   流程文档
│   ├── orchestration-workflow.svg     #   流程图
│   └── orchestration-workflow.gif     #   动画演示
│
├── agent-teams/                       # 多代理团队演示
│   └── agent-teams-prompt.md          #   团队提示词
│
├── development-workflows/             # 开发工作流
│   ├── rpi/                           #   RPI（Research → Plan → Implement）
│   └── cross-model-workflow/          #   跨模型工作流
│
├── presentation/                      # 演示文稿
│   ├── learning-journey/              #   Claude Code 学习之旅（面向非技术人员）
│   └── vibe-coding-to-agentic-engineering/  # Vibe Coding → Agentic Engineering
│
└── changelog/                         # 变更日志追踪
    ├── best-practice/                 #   最佳实践变更
    └── development-workflows/         #   开发工作流变更
```

---

## 编排工作流

本仓库通过一个天气系统演示了 **命令 → 代理 → 技能 (Command → Agent → Skill)** 的三层编排架构：

```
用户调用 /weather-orchestrator 命令
        │
        ▼
┌─────────────────────────┐
│  weather-orchestrator    │  ← 命令（入口点）
│  询问摄氏度/华氏度       │
└─────────┬───────────────┘
          │
          ▼
┌─────────────────────────┐
│  weather-agent           │  ← 子代理（预加载 weather-fetcher 技能）
│  从 Open-Meteo 获取温度  │
└─────────┬───────────────┘
          │
          ▼
┌─────────────────────────┐
│  weather-svg-creator     │  ← 技能（按需调用）
│  生成 SVG 天气卡片       │
└─────────────────────────┘
```

**两种技能模式**：
- **代理技能**（Agent Skill）：通过子代理定义中的 `skills:` 字段预加载到代理上下文
- **普通技能**（Invoked Skill）：运行时通过 `Skill` 工具按需调用

完整流程图见 [orchestration-workflow.md](orchestration-workflow/orchestration-workflow.md)。

---

## 深度报告

| 报告 | 主题 |
|------|------|
| [高级工具使用](reports/claude-advanced-tool-use.md) | 工具调用模式、MCP 工具、并行调用策略 |
| [Agent vs Command vs Skill](reports/claude-agent-command-skill.md) | 三者对比与选择指南 |
| [代理记忆](reports/claude-agent-memory.md) | 子代理的 `memory` 字段与持久化作用域 |
| [SDK vs CLI 系统提示](reports/claude-agent-sdk-vs-cli-system-prompts.md) | Agent SDK 与 CLI 的系统提示差异 |
| [全局 vs 项目设置](reports/claude-global-vs-project-settings.md) | 设置层级优先级详解 |
| [Chrome 集成对比](reports/claude-in-chrome-v-chrome-devtools-mcp.md) | Claude in Chrome vs Chrome DevTools MCP |
| [大型 Monorepo 技能](reports/claude-skills-for-larger-mono-repos.md) | 技能在大型仓库中的加载与性能 |
| [用量与限额](reports/claude-usage-and-rate-limits.md) | 使用量统计与速率限制 |
| [LLM 日常退化](reports/llm-day-to-day-degradation.md) | 模型性能日常波动分析 |

---

## 实用技巧

来自 Anthropic 工程师和 CEO 的 Claude Code 使用技巧：

| 来源 | 文件 | 要点 |
|------|------|------|
| Boris（工程师） | [13 tips (Jan 2026)](tips/claude-boris-13-tips-03-jan-26.md) | 早期最佳实践 |
| Boris | [10 tips (Feb 2026)](tips/claude-boris-10-tips-01-feb-26.md) | CLAUDE.md 与技能技巧 |
| Boris | [12 tips (Feb 2026)](tips/claude-boris-12-tips-12-feb-26.md) | 高级工作流 |
| Boris | [2 tips (Mar 10)](tips/claude-boris-2-tips-10-mar-26.md) | 子代理与并行 |
| Boris | [2 tips (Mar 25)](tips/claude-boris-2-tips-25-mar-26.md) | 命令与编排 |
| Boris | [15 tips (Mar 30)](tips/claude-boris-15-tips-30-mar-26.md) | 综合技巧集 |
| Boris | [6 tips (Apr 16)](tips/claude-boris-6-tips-16-apr-26.md) | 最新技巧 |
| Thariq（CEO） | [tips (Mar 17)](tips/claude-thariq-tips-17-mar-26.md) | CEO 的使用心得 |
| Thariq | [tips (Apr 16)](tips/claude-thariq-tips-16-apr-26.md) | 最新 CEO 技巧 |

---

## 教程

| 教程 | 说明 |
|------|------|
| [从零到精通](tutorial/claude-code-zero-to-mastery.md) | Claude Code 完整学习指南（2000+ 行，涵盖安装到高级编排） |
| [Day 0: 环境安装](tutorial/day0/) | Linux / macOS / Windows 安装指南 |
| [Day 1: 入门实践](tutorial/day1/) | 第一天实践指南 |

---

## 演示文稿

| 演示 | 说明 | 受众 |
|------|------|------|
| [Learning Journey](presentation/learning-journey/) | Claude Code 学习之旅 — 6 主题连续弧线 | 非技术人员 |
| [Vibe Coding → Agentic Engineering](presentation/vibe-coding-to-agentic-engineering/) | 从 Vibe Coding 到 Agentic Engineering 的进阶 | 技术人员 |

---

## 开发工作流

| 工作流 | 说明 |
|--------|------|
| [RPI 工作流](development-workflows/rpi/rpi-workflow.md) | Research → Plan → Implement 系统化开发流程 |
| [跨模型工作流](development-workflows/cross-model-workflow/cross-model-workflow.md) | 多模型协作工作流 |

---

## 快速开始

```bash
# 1. 克隆仓库
git clone https://github.com/your-username/claude-code-best-practice.git
cd claude-code-best-practice

# 2. 启动 Claude Code（会自动加载 CLAUDE.md）
claude

# 3. 试试编排工作流
/weather-orchestrator

# 4. 查看完整教程
# 打开 tutorial/claude-code-zero-to-mastery.md
```

---

## 钩子系统

本仓库包含一个跨平台声音通知系统，位于 `.claude/hooks/`：

- **scripts/hooks.py** — 钩子事件主处理器
- **config/hooks-config.json** — 团队共享配置
- **config/hooks-config.local.json** — 个人覆盖（已 gitignore）
- **sounds/** — 按事件组织的音频文件

支持的钩子事件：PreToolUse、PostToolUse、UserPromptSubmit、Notification、Stop、SubagentStart、SubagentStop、PreCompact、SessionStart、SessionEnd 等。

---

## 致谢

本仓库 fork 自 [shanraisshan/claude-code-best-practice](https://github.com/shanraisshan/claude-code-best-practice)，在其基础上进行了本地化和扩展。感谢原作者的出色工作。
