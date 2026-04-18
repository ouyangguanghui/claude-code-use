# claude-code-best-practice
从感性编程 (Vibe Coding) 迈向智能代理工程 (Agentic Engineering) —— 实践出真知，让 Claude 更完美

![使用 Claude Code 更新](https://img.shields.io/badge/updated_with_Claude_Code-v2.1.112%20(Apr%2017%2C%202026%206%3A37%20AM%20PKT)-white?style=flat&labelColor=555) <a href="https://github.com/shanraisshan/claude-code-best-practice/stargazers"><img src="https://img.shields.io/github/stars/shanraisshan/claude-code-best-practice?style=flat&label=%E2%98%85&labelColor=555&color=white" alt="GitHub Stars"></a> ![🇵🇰 第 4 多 ★](!/root/fourth-most-starred.svg)<br>

[![最佳实践](!/tags/best-practice.svg)](best-practice/) [![已实现](!/tags/implemented.svg)](implementation/) [![编排工作流](!/tags/orchestration-workflow.svg)](orchestration-workflow/orchestration-workflow.md) [![Claude](!/tags/claude.svg)](https://code.claude.com/docs) [![Boris](!/tags/boris-cherny.svg)](#-技巧与窍门) [![社区](!/tags/community.svg)](#-订阅) ![点击下方的徽章查看实际源代码](!/tags/click-badges.svg)<br>
<img src="!/tags/a.svg" height="14"> = 代理 (Agents) · <img src="!/tags/c.svg" height="14"> = 命令 (Commands) · <img src="!/tags/s.svg" height="14"> = 技能 (Skills)

<p align="center">
  <img src="!/claude-jumping.svg" alt="Claude Code 吉祥物跳跃" width="120" height="100"><br>
  <a href="https://github.com/trending"><img src="!/root/github-trending-day.svg" alt="GitHub 今日趋势榜第一项目"></a>
</p>

<p align="center">
  <img src="!/root/boris-slider.gif" alt="Boris Cherny 谈论 Claude Code" width="600"><br>
  Boris Cherny 在 X 上 (<a href="https://x.com/bcherny/status/2007179832300581177">推文 1</a> · <a href="https://x.com/bcherny/status/2017742741636321619">推文 2</a> · <a href="https://x.com/bcherny/status/2021699851499798911">推文 3</a>)
</p>


## 🧠 核心概念 (CONCEPTS)

| 功能 | 位置 | 描述 |
|---------|----------|-------------|
| <img src="!/tags/a.svg" height="14"> [**子代理 (Subagents)**](https://code.claude.com/docs/en/sub-agents) | `.claude/agents/<name>.md` | [![最佳实践](!/tags/best-practice.svg)](best-practice/claude-subagents.md) [![已实现](!/tags/implemented.svg)](implementation/claude-subagents-implementation.md) 处于全新独立上下文中的自主行动者 —— 拥有自定义工具、权限、模型、内存和持久身份 |
| <img src="!/tags/c.svg" height="14"> [**命令 (Commands)**](https://code.claude.com/docs/en/slash-commands) | `.claude/commands/<name>.md` | [![最佳实践](!/tags/best-practice.svg)](best-practice/claude-commands.md) [![已实现](!/tags/implemented.svg)](implementation/claude-commands-implementation.md) 将知识注入现有上下文 —— 用于工作流编排的简单用户调用提示词模板 |
| <img src="!/tags/s.svg" height="14"> [**技能 (Skills)**](https://code.claude.com/docs/en/skills) | `.claude/skills/<name>/SKILL.md` | [![最佳实践](!/tags/best-practice.svg)](best-practice/claude-skills.md) [![已实现](!/tags/implemented.svg)](implementation/claude-skills-implementation.md) 将知识注入现有上下文 —— 可配置、可预加载、支持自动发现，具有上下文分叉和渐进式披露功能 · [官方技能库](https://github.com/anthropics/skills/tree/main/skills) |
| [**工作流 (Workflows)**](https://code.claude.com/docs/en/common-workflows) | [`.claude/commands/weather-orchestrator.md`](.claude/commands/weather-orchestrator.md) | [![编排工作流](!/tags/orchestration-workflow.svg)](orchestration-workflow/orchestration-workflow.md) |
| [**钩子 (Hooks)**](https://code.claude.com/docs/en/hooks) | `.claude/hooks/` | [![最佳实践](!/tags/best-practice.svg)](https://github.com/shanraisshan/claude-code-hooks) [![已实现](!/tags/implemented.svg)](https://github.com/shanraisshan/claude-code-hooks) 用户定义的处理器（脚本、HTTP、提示词、代理），在特定事件发生时于智能代理循环之外运行 · [指南](https://code.claude.com/docs/en/hooks-guide) |
| [**MCP 服务器**](https://code.claude.com/docs/en/mcp) | `.claude/settings.json`, `.mcp.json` | [![最佳实践](!/tags/best-practice.svg)](best-practice/claude-mcp.md) [![已实现](!/tags/implemented.svg)](.mcp.json) 连接外部工具、数据库和 API 的模型上下文协议 (Model Context Protocol) |
| [**插件 (Plugins)**](https://code.claude.com/docs/en/plugins) | 可分发的软件包 | 技能、子代理、钩子、MCP 服务器和 LSP 服务器的集合包 · [市场](https://code.claude.com/docs/en/discover-plugins) · [创建市场](https://code.claude.com/docs/en/plugin-marketplaces) |
| [**设置 (Settings)**](https://code.claude.com/docs/en/settings) | `.claude/settings.json` | [![最佳实践](!/tags/best-practice.svg)](best-practice/claude-settings.md) [![已实现](!/tags/implemented.svg)](.claude/settings.json) 分层配置系统 · [权限](https://code.claude.com/docs/en/permissions) · [模型配置](https://code.claude.com/docs/en/model-config) · [输出样式](https://code.claude.com/docs/en/output-styles) · [沙箱机制](https://code.claude.com/docs/en/sandboxing) · [按键绑定](https://code.claude.com/docs/en/keybindings) · [快速模式](https://code.claude.com/docs/en/fast-mode) |
| [**状态栏 (Status Line)**](https://code.claude.com/docs/en/statusline) | `.claude/settings.json` | [![最佳实践](!/tags/best-practice.svg)](https://github.com/shanraisshan/claude-code-status-line) [![已实现](!/tags/implemented.svg)](.claude/settings.json) 可自定义的状态栏，显示上下文使用情况、模型、成本和会话信息 |
| [**记忆 (Memory)**](https://code.claude.com/docs/en/memory) | `CLAUDE.md`, `.claude/rules/`, `~/.claude/rules/`, `~/.claude/projects/<project>/memory/` | [![最佳实践](!/tags/best-practice.svg)](best-practice/claude-memory.md) [![已实现](!/tags/implemented.svg)](CLAUDE.md) 通过 CLAUDE.md 文件和 `@path` 导入实现的持久上下文 · [自动记忆](https://code.claude.com/docs/en/memory) · [规则](https://code.claude.com/docs/en/memory#organize-rules-with-clauderules) |
| [**检查点 (Checkpointing)**](https://code.claude.com/docs/en/checkpointing) | 自动 (基于 git) | 自动跟踪文件编辑，支持回溯 (`Esc Esc` 或 `/rewind`) 和定向总结 |
| [**CLI 启动标志**](https://code.claude.com/docs/en/cli-reference) | `claude [flags]` | [![最佳实践](!/tags/best-practice.svg)](best-practice/claude-cli-startup-flags.md) 用于启动 Claude Code 的命令行标志、子命令和环境变量 · [交互模式](https://code.claude.com/docs/en/interactive-mode) · [环境变量](https://code.claude.com/docs/en/env-vars) |
| **AI 术语** | | [![最佳实践](!/tags/best-practice.svg)](https://github.com/shanraisshan/claude-code-codex-cursor-gemini/blob/main/reports/ai-terms.md) 代理工程 (Agentic Engineering) · 上下文工程 (Context Engineering) · 感性编程 (Vibe Coding) |
| [**最佳实践**](https://code.claude.com/docs/en/best-practices) | | 官方最佳实践 · [提示词工程](https://github.com/anthropics/prompt-eng-interactive-tutorial) · [扩展 Claude Code](https://code.claude.com/docs/en/features-overview) |

### 🔥 热门功能 (Hot)

| 功能 | 位置 | 描述 |
|---------|----------|-------------|
| [**例行程序 (Routines)**](https://code.claude.com/docs/en/routines) ![beta](!/tags/beta.svg) | `claude.ai/code/routines`, `/schedule` | 基于 Anthropic 基础设施的云自动化 —— 支持计划任务、API 触发或 GitHub 事件驱动，即使电脑关闭也能运行 · [桌面任务](https://code.claude.com/docs/en/desktop-scheduled-tasks) |
| [**Devcontainers**](https://code.claude.com/docs/en/devcontainer) | `.devcontainer/` | 预配置的开发容器，具有安全隔离和防火墙规则，确保一致的 Claude Code 环境 |
| [**频道 (Channels)**](https://code.claude.com/docs/en/channels) ![beta](!/tags/beta.svg) | `--channels`, 基于插件 | 将来自 Telegram、Discord 或 Webhook 的事件推送到运行中的会话 —— 让 Claude 在你离开时做出响应 · [参考](https://code.claude.com/docs/en/channels-reference) |
| [**超级计划 (Ultraplan)**](https://code.claude.com/docs/en/ultraplan) ![beta](!/tags/beta.svg) | `/ultraplan` | 在云端草拟计划，支持基于浏览器的评审、行内评论和灵活执行 —— 可远程操作或传送回终端 |
| [**无闪烁模式**](https://code.claude.com/docs/en/fullscreen) ![beta](!/tags/beta.svg) | `CLAUDE_CODE_NO_FLICKER=1` | [![最佳实践](!/tags/best-practice.svg)](https://x.com/bcherny/status/2039421575422980329) 无闪烁的备用屏幕渲染，支持鼠标、稳定内存和应用内滚动 —— 可选的研究预览版 |
| [**自动模式 (Auto Mode)**](https://code.claude.com/docs/en/permission-modes#eliminate-prompts-with-auto-mode) ![beta](!/tags/beta.svg) | `claude --enable-auto-mode` | [![最佳实践](!/tags/best-practice.svg)](https://x.com/claudeai/status/2036503582166393240) 后台安全分类器取代手动权限提示 —— Claude 自主决定操作安全性，同时拦截提示词注入和风险升级 · 使用 `claude --enable-auto-mode` (或 `--permission-mode auto`) 启动，或在会话中通过 `Shift+Tab` 切换 · [博客](https://claude.com/blog/auto-mode) |
| [**能量提升 (Power-ups)**](best-practice/claude-power-ups.md) | `/powerup` | [![最佳实践](!/tags/best-practice.svg)](best-practice/claude-power-ups.md) 通过动画演示教学 Claude Code 功能的交互式课程 (v2.1.90) |
| [**电脑操作 (Computer Use)**](https://docs.anthropic.com/en/docs/agents-and-tools/computer-use) ![beta](!/tags/beta.svg) | `computer-use` MCP 服务器 | 让 Claude 控制你的屏幕 —— 在 macOS 上打开应用、点击、输入并截屏 · [桌面版](https://code.claude.com/docs/en/desktop#let-claude-use-your-computer) |
| [**代理 SDK (Agent SDK)**](https://code.claude.com/docs/en/agent-sdk/overview) | `npm` / `pip` 包 | 使用 Claude Code 作为库构建生产级 AI 代理 —— 提供 Python 和 TypeScript SDK，内置工具、钩子、子代理和 MCP · [快速上手](https://code.claude.com/docs/en/agent-sdk/quickstart) · [示例](https://github.com/anthropics/claude-agent-sdk-demos) |
| [**Ralph Wiggum 循环**](https://github.com/anthropics/claude-code/tree/main/plugins/ralph-wiggum) | 插件 | [![最佳实践](!/tags/best-practice.svg)](https://github.com/ghuntley/how-to-ralph-wiggum) [![已实现](!/tags/implemented.svg)](https://github.com/shanraisshan/novel-llm-26) 用于长期任务的自主开发循环 —— 循环迭代直至完成任务 |
| [**Chrome**](https://code.claude.com/docs/en/chrome) ![beta](!/tags/beta.svg) | `--chrome`, 扩展程序 | [![最佳实践](!/tags/best-practice.svg)](reports/claude-in-chrome-v-chrome-devtools-mcp.md) 通过 Chrome 中的 Claude 实现浏览器自动化 —— 测试 Web 应用、使用控制台调试、自动填写表单、从页面提取数据 |
| [**Claude Code 网页版**](https://code.claude.com/docs/en/claude-code-on-the-web) ![beta](!/tags/beta.svg) | `claude.ai/code` | 在云端基础设施上运行任务 —— 长期任务、PR 自动修复、无需本地设置的并行会话 · [例行程序](https://code.claude.com/docs/en/routines) |
| [**Slack**](https://code.claude.com/docs/en/slack) | 在 Slack 中 `@Claude` | 在团队聊天中提及 @Claude 并布置编程任务 —— 路由到 Claude Code 网页会话进行 Bug 修复、代码评审和并行任务执行 |
| [**代码评审 (Code Review)**](https://code.claude.com/docs/en/code-review) ![beta](!/tags/beta.svg) | GitHub App (托管) | [![最佳实践](!/tags/best-practice.svg)](https://x.com/claudeai/status/2031088171262554195) 多代理 PR 分析，捕捉 Bug、安全漏洞和回归风险 · [博客](https://claude.com/blog/code-review) |
| [**GitHub Actions**](https://code.claude.com/docs/en/github-actions) | `.github/workflows/` | 在 CI/CD 流水线中自动进行 PR 评审、Issue 分类和代码生成 · [GitLab CI/CD](https://code.claude.com/docs/en/gitlab-ci-cd) |
| [**远程控制 (Remote Control)**](https://code.claude.com/docs/en/remote-control) | `/remote-control`, `/rc` | [![最佳实践](!/tags/best-practice.svg)](https://x.com/noahzweben/status/2032533699116355819) 从任何设备（手机、平板或浏览器）继续本地会话 · [无头模式](https://code.claude.com/docs/en/headless) |
| [**代理团队 (Agent Teams)**](https://code.claude.com/docs/en/agent-teams) ![beta](!/tags/beta.svg) | 内置 (环境变量) | [![最佳实践](!/tags/best-practice.svg)](https://x.com/bcherny/status/2019472394696683904) [![已实现](!/tags/implemented.svg)](implementation/claude-agent-teams-implementation.md) 多个代理在同一代码库上并行工作，并共享任务协调 |
| [**计划任务 (Scheduled Tasks)**](https://code.claude.com/docs/en/scheduled-tasks) | `/loop`, `/schedule`, cron 工具 | [![最佳实践](!/tags/best-practice.svg)](https://x.com/bcherny/status/2030193932404150413) [![已实现](!/tags/implemented.svg)](implementation/claude-scheduled-tasks-implementation.md) `/loop` 在本地按周期运行提示词（最长 7 天） · [`/schedule`](https://code.claude.com/docs/en/routines) 在 Anthropic 云端基础设施运行提示词 —— 即使电脑关闭也能工作 · [公告](https://x.com/noahzweben/status/2036129220959805859) |
| [**语音听写 (Voice Dictation)**](https://code.claude.com/docs/en/voice-dictation) ![beta](!/tags/beta.svg) | `/voice` | [![最佳实践](!/tags/best-practice.svg)](https://x.com/trq212/status/2028628570692890800) 一键语音输入提示词，支持 20 种语言，激活键可重新绑定 |
| [**简化与批量处理**](https://code.claude.com/docs/en/skills#bundled-skills) | `/simplify`, `/batch` | [![最佳实践](!/tags/best-practice.svg)](https://x.com/bcherny/status/2027534984534544489) 用于代码质量和批量操作的内置技能 —— 简化重构以提高复用性和效率，跨文件批量运行命令 |
| [**Git 工作树 (Worktrees)**](https://code.claude.com/docs/en/common-workflows#run-parallel-claude-code-sessions-with-git-worktrees) | 内置 | [![最佳实践](!/tags/best-practice.svg)](https://x.com/bcherny/status/2025007393290272904) 用于并行开发的隔离 git 分支 —— 每个代理获得自己的工作副本 |

<p align="center">
  <img src="!/claude-jumping.svg" alt="分节符" width="60" height="50">
</p>

<a id="orchestration-workflow"></a>

## <a href="orchestration-workflow/orchestration-workflow.md"><img src="!/tags/orchestration-workflow-hd.svg" alt="编排工作流"></a>

查看 [编排工作流 (orchestration-workflow)](orchestration-workflow/orchestration-workflow.md) 了解 <img src="!/tags/c.svg" height="14"> **命令** → <img src="!/tags/a.svg" height="14"> **代理** → <img src="!/tags/s.svg" height="14"> **技能** 模式的实现细节。


<p align="center">
  <img src="orchestration-workflow/orchestration-workflow.svg" alt="命令、技能、代理架构流图" width="100%">
</p>

<p align="center">
  <img src="orchestration-workflow/orchestration-workflow.gif" alt="编排工作流演示" width="600">
</p>

![如何使用](!/tags/how-to-use.svg)

```bash
claude
/weather-orchestrator
```

<p align="center">
  <img src="!/claude-jumping.svg" alt="分节符" width="60" height="50">
</p>

## ⚙️ 开发工作流 (DEVELOPMENT WORKFLOWS)

所有主要工作流都收敛于相同的架构模式：**调研 → 计划 → 执行 → 评审 → 发布 (Research → Plan → Execute → Review → Ship)**

| 名称 | ★ | 独特性 | 计划方式 | <img src="!/tags/a.svg" height="14"> | <img src="!/tags/c.svg" height="14"> | <img src="!/tags/s.svg" height="14"> |
|------|---|------------|------|---|---|---|
| [Everything Claude Code](https://github.com/affaan-m/everything-claude-code) | 158k | ![直觉评分](https://img.shields.io/badge/instinct_scoring-ddf4ff) ![AgentShield](https://img.shields.io/badge/AgentShield-ddf4ff) ![多语言规则](https://img.shields.io/badge/multi--lang_rules-ddf4ff) | <img src="!/tags/a.svg" height="14"> [planner](https://github.com/affaan-m/everything-claude-code/blob/main/agents/planner.md) | 48 | 143 | 230 |
| [Superpowers](https://github.com/obra/superpowers) | 156k | ![TDD优先](https://img.shields.io/badge/TDD--first-ddf4ff) ![铁律](https://img.shields.io/badge/Iron_Laws-ddf4ff) ![全局计划评审](https://img.shields.io/badge/whole--plan_review-ddf4ff) | <img src="!/tags/s.svg" height="14"> [writing-plans](https://github.com/obra/superpowers/tree/main/skills/writing-plans) | 5 | 3 | 14 |
| [Spec Kit](https://github.com/github/spec-kit) | 89k | ![规格驱动](https://img.shields.io/badge/spec--driven-ddf4ff) ![宪法](https://img.shields.io/badge/constitution-ddf4ff) ![22+ 工具](https://img.shields.io/badge/22%2B_tools-ddf4ff) | <img src="!/tags/c.svg" height="14"> [speckit.plan](https://github.com/github/spec-kit/blob/main/templates/commands/plan.md) | 0 | 9+ | 0 |
| [gstack](https://github.com/garrytan/gstack) | 74k | ![角色人格](https://img.shields.io/badge/role_personas-ddf4ff) ![/codex 评审](https://img.shields.io/badge/%2Fcodex_review-ddf4ff) ![并行冲刺](https://img.shields.io/badge/parallel_sprints-ddf4ff) | <img src="!/tags/s.svg" height="14"> [autoplan](https://github.com/garrytan/gstack/tree/main/autoplan) | 0 | 0 | 46 |
| [Get Shit Done](https://github.com/gsd-build/get-shit-done) | 54k | ![全新 200K 上下文](https://img.shields.io/badge/fresh_200K_contexts-ddf4ff) ![波动式执行](https://img.shields.io/badge/wave_execution-ddf4ff) ![XML 计划](https://img.shields.io/badge/XML_plans-ddf4ff) | <img src="!/tags/a.svg" height="14"> [gsd-planner](https://github.com/gsd-build/get-shit-done/blob/main/agents/gsd-planner.md) | 31 | 122 | 0 |
| [BMAD-METHOD](https://github.com/bmad-code-org/BMAD-METHOD) | 45k | ![全生命周期](https://img.shields.io/badge/full_SDLC-ddf4ff) ![代理人格](https://img.shields.io/badge/agent_personas-ddf4ff) ![22+ 平台](https://img.shields.io/badge/22%2B_platforms-ddf4ff) | <img src="!/tags/s.svg" height="14"> [bmad-create-prd](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/src/bmm-skills/2-plan-workflows/bmad-create-prd) | 0 | 0 | 39 |
| [OpenSpec](https://github.com/Fission-AI/OpenSpec) | 41k | ![增量规格](https://img.shields.io/badge/delta_specs-ddf4ff) ![存量开发](https://img.shields.io/badge/brownfield-ddf4ff) ![产物 DAG](https://img.shields.io/badge/artifact_DAG-ddf4ff) | <img src="!/tags/c.svg" height="14"> [opsx:propose](https://github.com/Fission-AI/OpenSpec/blob/main/src/commands/workflow/new-change.ts) | 0 | 10 | 0 |
| [oh-my-claudecode](https://github.com/Yeachan-Heo/oh-my-claudecode) | 29k | ![团队编排](https://img.shields.io/badge/teams_orchestration-ddf4ff) ![tmux 工作器](https://img.shields.io/badge/tmux_workers-ddf4ff) ![技能自动注入](https://img.shields.io/badge/skill_auto--inject-ddf4ff) | <img src="!/tags/s.svg" height="14"> [ralplan](https://github.com/Yeachan-Heo/oh-my-claudecode/tree/main/skills/ralplan) | 19 | 0 | 37 |
| [Compound Engineering](https://github.com/EveryInc/compound-engineering-plugin) | 14k | ![复合学习](https://img.shields.io/badge/Compound_Learning-ddf4ff) ![多平台 CLI](https://img.shields.io/badge/Multi--Platform_CLI-ddf4ff) ![插件市场](https://img.shields.io/badge/Plugin_Marketplace-ddf4ff) | <img src="!/tags/s.svg" height="14"> [ce-plan](https://github.com/EveryInc/compound-engineering-plugin/tree/main/plugins/compound-engineering/skills/ce-plan) | 49 | 3 | 51 |
| [HumanLayer](https://github.com/humanlayer/humanlayer) | 10k | ![RPI 模式](https://img.shields.io/badge/RPI-ddf4ff) ![上下文工程](https://img.shields.io/badge/context_engineering-ddf4ff) ![300k+ 代码行](https://img.shields.io/badge/300k%2B_LOC-ddf4ff) | <img src="!/tags/c.svg" height="14"> [create_plan](https://github.com/humanlayer/humanlayer/blob/main/.claude/commands/create_plan.md) | 6 | 27 | 0 |

### 其他
- [跨模型 (Claude Code + Codex) 工作流](development-workflows/cross-model-workflow/cross-model-workflow.md) [![已实现](!/tags/implemented.svg)](development-workflows/cross-model-workflow/cross-model-workflow.md)
- [RPI 模式](development-workflows/rpi/rpi-workflow.md) [![已实现](!/tags/implemented.svg)](development-workflows/rpi/rpi-workflow.md)
- [Ralph Wiggum 循环](https://www.youtube.com/watch?v=eAtvoGlpeRU) [![已实现](!/tags/implemented.svg)](https://github.com/shanraisshan/novel-llm-26)
- [Andrej Karpathy (OpenAI 创始成员) 工作流](https://x.com/karpathy/status/2015883857489522876)
- [Peter Steinberger (OpenClaw 创始人) 工作流](https://youtu.be/8lF7HmQ_RgY?t=2582)
- Boris Cherny (Claude Code 创始人) 工作流 —— [13 条技巧](tips/claude-boris-13-tips-03-jan-26.md) · [10 条技巧](tips/claude-boris-10-tips-01-feb-26.md) · [12 条技巧](tips/claude-boris-12-tips-12-feb-26.md) · [2 条技巧](tips/claude-boris-2-tips-25-mar-26.md) · [15 条技巧](tips/claude-boris-15-tips-30-mar-26.md) · [6 条技巧](tips/claude-boris-6-tips-16-apr-26.md) [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny)
- Thariq (Anthropic) 工作流 —— [技能篇](tips/claude-thariq-tips-17-mar-26.md) · [会话管理篇](tips/claude-thariq-tips-16-apr-26.md) [![Thariq](!/tags/thariq.svg)](https://x.com/trq212)

<p align="center">
  <img src="!/claude-jumping.svg" alt="分节符" width="60" height="50">
</p>

## 💡 技巧与窍门 (82)

🚫👶 = 不要时刻“陪跑” (do not babysit)

[提示词 (Prompting)](#tips-prompting) · [计划 (Planning)](#tips-planning) · [上下文 (Context)](#tips-context) · [会话 (Session)](#tips-session) · [CLAUDE.md](#tips-claudemd) · [代理 (Agents)](#tips-agents) · [命令 (Commands)](#tips-commands) · [技能 (Skills)](#tips-skills) · [钩子 (Hooks)](#tips-hooks) · [工作流 (Workflows)](#tips-workflows) · [高级技巧 (Advanced)](#tips-workflows-advanced) · [Git / PR](#tips-git-pr) · [调试 (Debugging)](#tips-debugging) · [工具 (Utilities)](#tips-utilities) · [日常 (Daily)](#tips-daily)

![社区](!/tags/community.svg)

<a id="tips-prompting"></a>■ **提示词 (Prompting) (3)**

| 技巧 | 来源 |
|-----|--------|
| 挑战 Claude —— “审问我这次修改，在我通过你的测试之前不要提交 PR。” 或 “向我证明这行得通”，并让 Claude 比较 main 分支和你当前分支的差异 🚫👶 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2017742752566632544) |
| 在一个平庸的修复之后 —— “既然你现在掌握了所有背景，把刚才写的删了，重新实现一个优雅的方案” 🚫👶 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2017742752566632544) |
| Claude 能自主修好大部分 Bug —— 直接贴入 Bug，说 “fix”，不要微观管理它是如何执行的 🚫👶 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2017742750473720121) |

<a id="tips-planning"></a>■ **计划/规格 (Planning/Specs) (6)**

| 技巧 | 来源 |
|-----|--------|
| 永远从 [计划模式 (plan mode)](https://code.claude.com/docs/en/common-workflows) 开始 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2007179845336527000) |
| 先给一个极简的规格或提示词，让 Claude 使用 [AskUserQuestion](https://code.claude.com/docs/en/cli-reference) 工具采访你，然后开一个新会话来执行该规格 | [![Thariq](!/tags/thariq.svg)](https://x.com/trq212/status/2005315275026260309) |
| 永远制定分阶段的门禁计划，每个阶段都要有多个测试（单元测试、自动化测试、集成测试） | |
| 启动第二个 Claude 以资深职员工程师的身份评审你的计划，或者使用 [跨模型](development-workflows/cross-model-workflow/cross-model-workflow.md) 进行评审 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2017742745365057733) |
| 在交接工作前编写详细的规格说明并消除歧义 —— 描述越具体，产出效果越好 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2017742752566632544) |
| 原型 > 需求文档 (PRD) —— 与其编写规格说明，不如构建 20-30 个版本的原型，构建成本很低，所以要多尝试 | [![Boris](!/tags/boris-cherny.svg)](https://youtu.be/julbw1JuAz0?t=3630) [![视频](!/tags/video.svg)](https://youtu.be/julbw1JuAz0?t=3630) |

<a id="tips-context"></a>■ **上下文 (Context) (5)**

| 技巧 | 来源 |
|-----|--------|
| 在 1M 上下文模型中，token 消耗到 ~300-400k 左右会出现上下文腐烂 —— 对于智力敏感型任务，不要让会话超过这个限制 | [![Thariq](!/tags/thariq.svg)](tips/claude-thariq-tips-16-apr-26.md) |
| 避开代理智力盲区，手动进行 [/compact](https://code.claude.com/docs/en/interactive-mode)（压缩）至最大 50%。如果切换到新任务，请使用 [/clear](https://code.claude.com/docs/en/cli-reference) 重置上下文 | |
| 回溯 > 修正 —— 使用 double-Esc 或 [/rewind](https://code.claude.com/docs/en/checkpointing) 回溯到失败尝试之前，用学到的教训重新提示，而不是让失败的尝试和纠正污染上下文 🚫👶 | [![Thariq](!/tags/thariq.svg)](tips/claude-thariq-tips-16-apr-26.md) |
| 带有提示的 [/compact](https://code.claude.com/docs/en/interactive-mode)（例如：/compact focus on the auth refactor, drop the test debugging）优于让其自动压缩 —— 模型在由于上下文腐烂而自动压缩时智力水平最低 | [![Thariq](!/tags/thariq.svg)](tips/claude-thariq-tips-16-apr-26.md) |
| 使用子代理进行上下文管理 —— 问问自己：“我还需要这个工具的输出吗，还是只需要结论？” —— 20 个文件读取 + 12 个 grep + 3 个死路留在子代理上下文中，只返回最终报告 🚫👶 | [![Thariq](!/tags/thariq.svg)](tips/claude-thariq-tips-16-apr-26.md) |

<a id="tips-session"></a>■ **会话管理 (Session Management) (6)**

| 技巧 | 来源 |
|-----|--------|
| 每一步都是分叉点 —— 在 Claude 结束一个轮次后，根据需要承载的现有上下文量，在继续 (Continue)、/rewind、/clear、/compact 或子代理之间做出选择 | [![Thariq](!/tags/thariq.svg)](tips/claude-thariq-tips-16-apr-26.md) |
| 新任务 = 新会话 —— 相关任务（例如为你刚刚构建的内容编写文档）可以复用上下文以提高效率，但全新的任务应该开启新鲜会话 | [![Thariq](!/tags/thariq.svg)](tips/claude-thariq-tips-16-apr-26.md) |
| 在回溯之前使用 “summarize from here” 让 Claude 写一条交接信息 —— 就像是未来版本的 Claude 给前一个版本写的备忘录 | [![Thariq](!/tags/thariq.svg)](tips/claude-thariq-tips-16-apr-26.md) |
| /compact vs /clear —— compact 是有损的，但有利于保持势头（任务中，模糊细节可以接受）；/clear + brief 工作量更大，但你可以精确控制承载内容（高风险的下一步） | [![Thariq](!/tags/thariq.svg)](tips/claude-thariq-tips-16-apr-26.md) |
| 对于长时间会话使用摘要回顾 —— 简短总结 Claude 做了什么以及下一步要做什么，在几分钟或几小时后返回时非常有用。在 /config 中可以禁用 recaps | [![Boris](!/tags/boris-cherny.svg)](tips/claude-boris-6-tips-16-apr-26.md) |
| 为重要的会话 [/rename](https://code.claude.com/docs/en/cli-reference)（重命名）（例如：[TODO - 重构任务]），以便稍后 [/resume](https://code.claude.com/docs/en/cli-reference)（恢复）它们 —— 同时运行多个 Claude 实例时请标注每个实例 | [![Cat](!/tags/cat-wu.svg)](https://every.to/podcast/how-to-use-claude-code-like-the-people-who-built-it) |

<a id="tips-claudemd"></a>■ **CLAUDE.md (7)**

| 技巧 | 来源 |
|-----|--------|
| [CLAUDE.md](https://code.claude.com/docs/en/memory) 每个文件的目标应在 [200 行](https://code.claude.com/docs/en/memory#write-effective-instructions) 以内。在 [humanlayer 项目中为 60 行](https://www.humanlayer.dev/blog/writing-a-good-claude-md)（[仍不能 100% 保证](https://www.reddit.com/r/ClaudeCode/comments/1qn9pb9/claudemd_says_must_use_agent_claude_ignores_it_80/)） | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2007179840848597422) [![Dex](!/tags/community-dex.svg)](https://www.humanlayer.dev/blog/writing-a-good-claude-md) |
| 将领域特定的 CLAUDE.md 规则包裹在 [\<important if="..."\> 标签](https://www.hlyr.dev/blog/stop-claude-from-ignoring-your-claude-md) 中，以防止 Claude 随着文件变长而忽略它们 | [![Dex](!/tags/community-dex.svg)](https://www.hlyr.dev/blog/stop-claude-from-ignoring-your-claude-md) |
| 对于单体大仓 (monorepos) 使用 [多个 CLAUDE.md](best-practice/claude-memory.md) —— 支持父级 + 子级加载 | |
| 使用 [.claude/rules/](https://code.claude.com/docs/en/memory#organize-rules-with-clauderules) 来拆分大型指令 | |
| [memory.md](https://code.claude.com/docs/en/memory), constitution.md 并不能保证任何事情 | |
| 任何开发者都应该能启动 Claude，说 “run the tests” 并且第一次就能成功 —— 如果不行，说明你的 CLAUDE.md 缺少基本的设置/构建/测试命令 | [![Dex](!/tags/community-dex.svg)](https://x.com/dexhorthy/status/2034713765401551053) |
| 保持代码库整洁并完成迁移 —— 部分迁移的框架会迷惑模型，使其选错模式 | [![Boris](!/tags/boris-cherny.svg)](https://youtu.be/julbw1JuAz0?t=1112) [![视频](!/tags/video.svg)](https://youtu.be/julbw1JuAz0?t=1112) |
| 使用 [settings.json](best-practice/claude-settings.md) 来强制执行行为（归属权、权限、模型） —— 当 attribution.commit: "" 是确定性的时，不要在 CLAUDE.md 中放 “永远不要添加 Co-Authored-By” | [![davila7](!/tags/community-davila7.svg)](https://x.com/dani_avila7/status/2036182734310195550) |

<a id="tips-agents"></a><img src="!/tags/a.svg" height="14"> **代理 (Agents) (4)**

| 技巧 | 来源 |
|-----|--------|
| 使用功能特定的 [子代理](https://code.claude.com/docs/en/sub-agents)（带额外上下文）和 [技能](https://code.claude.com/docs/en/skills)（渐进式披露），而不是泛泛的 QA 或后端工程师角色 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2007179850139000872) |
| 说 “use subagents” 来为问题投入更多算力 —— 卸载任务以保持主上下文整洁专注 🚫👶 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2017742755737555434) |
| 使用 [结合 tmux 的代理团队](https://code.claude.com/docs/en/agent-teams) 和 [git 工作树](https://x.com/bcherny/status/2025007393290272904) 进行并行开发 | |
| 使用 [测试时计算 (test time compute)](https://code.claude.com/docs/en/sub-agents) —— 独立的上下文窗口能产出更好的结果；一个代理可能会制造 Bug，而另一个（同模型）能发现它们 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2031151689219321886) |

<a id="tips-commands"></a><img src="!/tags/c.svg" height="14"> **命令 (Commands) (3)**

| 技巧 | 来源 |
|-----|--------|
| 使用 [命令](https://code.claude.com/docs/en/slash-commands) 来编排你的工作流，而不是用 [子代理](https://code.claude.com/docs/en/sub-agents) | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2007179847949500714) |
| 为你每天执行多次的每个 “内循环” 工作流使用 [斜杠命令](https://code.claude.com/docs/en/slash-commands) —— 节省重复提示的时间，命令存放在 .claude/commands/ 并检入 git | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2007179847949500714) |
| 如果你每天重复某件事超过一次，就把它变成 [技能](https://code.claude.com/docs/en/skills) 或 [命令](https://code.claude.com/docs/en/slash-commands) —— 构建 /techdebt（技术债）、上下文转储或分析命令 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2017742748984742078) |

<a id="tips-skills"></a><img src="!/tags/s.svg" height="14"> **技能 (Skills) (9)**

| 技巧 | 来源 |
|-----|--------|
| 使用 [context: fork](https://code.claude.com/docs/en/skills) 在隔离的子代理中运行技能 —— 主上下文只看最终结果，不看中间的工具调用。agent 字段允许你设置子代理类型 | [![Lydia](!/tags/lydia.svg)](https://x.com/lydiahallie/status/2033603164398883042) |
| 为单体大仓使用 [子文件夹中的技能库](reports/claude-skills-for-larger-mono-repos.md) | |
| 技能是文件夹而非文件 —— 使用 references/、scripts/、examples/ 子目录来实现 [渐进式披露](https://code.claude.com/docs/en/skills) | [![Thariq](!/tags/thariq.svg)](https://x.com/trq212/status/2033949937936085378) |
| 在每个技能中构建一个 Gotchas（注意事项）章节 —— 这里是最高信号的内容，随着时间推移添加 Claude 的失败点 | [![Thariq](!/tags/thariq.svg)](https://x.com/trq212/status/2033949937936085378) |
| 技能说明字段是触发器而非总结 —— 为模型编写它（“我什么时候应该启动？”） | [![Thariq](!/tags/thariq.svg)](https://x.com/trq212/status/2033949937936085378) |
| 不要在技能中陈述显而易见的事 —— 专注于那些让 Claude 跳出默认行为的内容 🚫👶 | [![Thariq](!/tags/thariq.svg)](https://x.com/trq212/status/2033949937936085378) |
| 不要通过技能来限制 Claude —— 给出目标和约束，而不是强制性的逐步指令 🚫👶 | [![Thariq](!/tags/thariq.svg)](https://x.com/trq212/status/2033949937936085378) |
| 在技能中包含脚本和库，这样 Claude 是在组合代码而不是重新构建样板代码 | [![Thariq](!/tags/thariq.svg)](https://x.com/trq212/status/2033949937936085378) |
| 在 SKILL.md 中嵌入 !command 以将动态 shell 输出注入提示词 —— Claude 在调用时运行它，模型只看结果 | [![Lydia](!/tags/lydia.svg)](https://x.com/lydiahallie/status/2034337963820327017) |

<a id="tips-hooks"></a>■ **钩子 (Hooks) (5)**

| 技巧 | 来源 |
|-----|--------|
| 在技能中使用 [按需钩子 (on-demand hooks)](https://code.claude.com/docs/en/skills) —— /careful 拦截破坏性命令，/freeze 拦截目录外的编辑 | [![Thariq](!/tags/thariq.svg)](https://x.com/trq212/status/2033949937936085378) |
| 通过 PreToolUse 钩子 [测量技能使用情况](https://code.claude.com/docs/en/skills) 以发现热门或触发不足的技能 | [![Thariq](!/tags/thariq.svg)](https://x.com/trq212/status/2033949937936085378) |
| 使用 [PostToolUse 钩子](https://code.claude.com/docs/en/hooks) 自动格式化代码 —— Claude 生成格式良好的代码，钩子处理最后 10% 以避免 CI 失败 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2007179852047335529) |
| 将 [权限请求](https://code.claude.com/docs/en/hooks) 通过钩子路由给 Opus —— 让它扫描攻击并自动批准安全的请求 🚫👶 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2017742755737555434) |
| 使用 [Stop 钩子](https://code.claude.com/docs/en/hooks) 促使 Claude 在轮次结束时继续执行或验证其工作 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2021701059253874861) |

<a id="tips-workflows"></a>■ **工作流 (Workflows) (6)**

| 技巧 | 来源 |
|-----|--------|
| 原生 Claude Code 对于小型任务比任何工作流都好用 | |
| 使用 [/model](https://code.claude.com/docs/en/model-config) 选择模型和推理，[/context](https://code.claude.com/docs/en/interactive-mode) 查看上下文占用，[/usage](https://code.claude.com/docs/en/costs) 检查额度限制，[/extra-usage](https://code.claude.com/docs/en/interactive-mode) 配置溢出计费，[/config](https://code.claude.com/docs/en/settings) 配置设置 —— 对计划模式使用 Opus，对代码编写使用 Sonnet，以获得两者的最佳结合 | [![Cat](!/tags/cat-wu.svg)](https://x.com/_catwu/status/1955694117264261609) |
| 始终在 [/config](https://code.claude.com/docs/en/settings) 中开启 [思维模式 (thinking mode)](https://code.claude.com/docs/en/model-config)（以查看推理过程）并将 [输出样式 (Output Style)](https://code.claude.com/docs/en/output-styles) 设置为解释型 (Explanatory)（以查看带有 ★ 洞察框的详细输出），从而更好地理解 Claude 的决策 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2007179838864666847) |
| 在提示词中使用 ultrathink 关键字以获得 [高强度推理](https://docs.anthropic.com/en/docs/build-with-claude/extended-thinking#tips-and-best-practices) | |
| /focus 模式隐藏所有中间工作，只显示最终结果 —— 信任模型运行正确的命令，只需查看结果（使用 /focus 切换） | [![Boris](!/tags/boris-cherny.svg)](tips/claude-boris-6-tips-16-apr-26.md) |
| 通过 Opus 4.7 的自适应思维调节努力程度 —— 低档追求速度和更少 token，最大档追求最强智能（滑块：low · medium · high · xhigh · max） | [![Boris](!/tags/boris-cherny.svg)](tips/claude-boris-6-tips-16-apr-26.md) |

<a id="tips-workflows-advanced"></a>■ **高级工作流 (Workflows Advanced) (9)**

| 技巧 | 来源 |
|-----|--------|
| 大量使用 ASCII 图表来理解你的架构 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2017742759218794768) |
| 使用 [/loop](https://code.claude.com/docs/en/scheduled-tasks) 进行本地循环监控（长达 7 天） · 使用 [/schedule](https://code.claude.com/docs/en/routines) 进行即使电脑关闭也能运行的云端循环任务 | |
| 使用 [Ralph Wiggum 插件](https://github.com/shanraisshan/novel-llm-26) 进行长时间自主任务 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2007179858435281082) |
| 使用通配符语法设置 [/permissions](https://code.claude.com/docs/en/permissions)（如 Bash(npm run *), Edit(/docs/**)），而不是危险地跳过权限确认 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2007179854077407667) |
| 使用 [/sandbox](https://code.claude.com/docs/en/sandboxing) 通过文件和网络隔离减少权限提示 —— 内部减少了 84% 的提示 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2021700506465579443) [![Cat](!/tags/cat-wu.svg)](https://creatoreconomy.so/p/inside-claude-code-how-an-ai-native-actually-works-cat-wu) |
| 投入精力开发 [产品验证 (product verification)](https://code.claude.com/docs/en/skills) 技能（如：注册流驱动器、结账验证器） —— 值得花一周时间来完善 | [![Thariq](!/tags/thariq.svg)](https://x.com/trq212/status/2033949937936085378) |
| 使用 [自动模式 (auto mode)](https://code.claude.com/docs/en/permission-modes#eliminate-prompts-with-auto-mode) 而不是危险地跳过权限确认 —— 一个基于模型的分类器会决定每个命令是否安全并自动批准，有风险时会暂停询问。使用 Shift+Tab 在 询问 → 计划 → 自动 模式间循环 🚫👶 | [![Boris](!/tags/boris-cherny.svg)](tips/claude-boris-6-tips-16-apr-26.md) |
| 使用 /fewer-permission-prompts 技能扫描会话历史中不断提示的安全 bash/MCP 命令，然后获取建议的白名单并粘贴到 [设置](best-practice/claude-settings.md) 中 | [![Boris](!/tags/boris-cherny.svg)](tips/claude-boris-6-tips-16-apr-26.md) |
| 构建一个 /go 技能，它可以 (1) 通过 bash/浏览器/电脑操作进行端到端测试 (2) 运行 /simplify (3) 提交 PR —— 这样当你回来时，你知道代码是没问题的 🚫👶 | [![Boris](!/tags/boris-cherny.svg)](tips/claude-boris-6-tips-16-apr-26.md) |

<a id="tips-git-pr"></a>■ **Git / PR (5)**

| 技巧 | 来源 |
|-----|--------|
| 保持 PR 细小且专注 —— [中位数 118 行](tips/claude-boris-2-tips-25-mar-26.md)（一天内 141 个 PR，改变了 45K 行代码），每个 PR 一个功能，更易于评审和回滚 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2038552880018538749) |
| 始终对 PR 进行 [压缩合并 (squash merge)](tips/claude-boris-2-tips-25-mar-26.md) —— 保持干净的线性历史，每个功能一个 commit，方便 git 回滚和 git 二分法查找 (bisect) | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2038552880018538749) |
| 频繁提交 —— 尝试至少每小时提交一次，任务一完成就立即提交 | ![Shayan](!/tags/community-shayan.svg) |
| 在同事的 PR 上标记 [@claude](https://github.com/apps/claude)，为循环往复的评审反馈自动生成 lint 规则 —— 将自己从代码评审中自动化解脱出来 🚫👶 | [![Boris](!/tags/boris-cherny.svg)](https://youtu.be/julbw1JuAz0?t=2715) [![视频](!/tags/video.svg)](https://youtu.be/julbw1JuAz0?t=2715) |
| 使用 [/code-review](https://code.claude.com/docs/en/code-review) 进行多代理 PR 分析 —— 在合并前捕获 Bug、安全漏洞和回归 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2031089411820228645) |

<a id="tips-debugging"></a>■ **调试 (Debugging) (7)**

| 技巧 | 来源 |
|-----|--------|
| 养成只要遇到任何问题就截图并分享给 Claude 的习惯 | ![Shayan](!/tags/community-shayan.svg) |
| 使用 MCP（[Chrome 中的 Claude](https://code.claude.com/docs/en/chrome)、[Playwright](https://github.com/microsoft/playwright-mcp)、[Chrome DevTools](https://developer.chrome.com/blog/chrome-devtools-mcp)）让 Claude 自行查看 Chrome 控制台日志 | |
| 始终要求 Claude 将终端（你想看日志的那个）作为后台任务运行，以便更好地调试 | |
| 使用 [/doctor](https://code.claude.com/docs/en/cli-reference) 诊断安装、身份验证和配置问题 | |
| 压缩 (compaction) 期间的错误可以通过使用 [/model](https://code.claude.com/docs/en/model-config) 选择 1M token 模型，然后运行 [/compact](https://code.claude.com/docs/en/interactive-mode) 来解决 | |
| 使用跨模型进行质检 (QA) —— 例如使用 [Codex](https://github.com/shanraisshan/codex-cli-best-practice) 评审计划和实现 | |
| 智能代理搜索 (glob + grep) 优于 RAG —— Claude Code 尝试并弃用了向量数据库，因为代码会脱节且权限管理复杂 | [![Boris](!/tags/boris-cherny.svg)](https://youtu.be/julbw1JuAz0?t=3095) [![视频](!/tags/video.svg)](https://youtu.be/julbw1JuAz0?t=3095) |

<a id="tips-utilities"></a>■ **工具 (Utilities) (5)**

| 技巧 | 来源 |
|-----|--------|
| 使用 [iTerm](https://iterm2.com/)/[Ghostty](https://ghostty.org/)/[tmux](https://github.com/tmux/tmux) 终端而不是 IDE ([VS Code](https://code.visualstudio.com/)/[Cursor](https://www.cursor.com/)) | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2017742753971769626) |
| 使用 [/voice](https://code.claude.com/docs/en/voice-dictation) 或 [Wispr Flow](https://wisprflow.ai) 进行语音提示（效率提升 10 倍） | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2038454362226467112) |
| 使用 [claude-code-hooks](https://github.com/shanraisshan/claude-code-hooks) 获取 Claude 反馈 | ![Shayan](!/tags/community-shayan.svg) |
| 使用 [状态栏 (status line)](https://github.com/shanraisshan/claude-code-status-line) 获取上下文感知和快速压缩功能 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2021700784019452195) ![Shayan](!/tags/community-shayan.svg) |
| 探索 [settings.json](best-practice/claude-settings.md) 的功能，如 [计划目录 (Plans Directory)](best-practice/claude-settings.md#plans-directory)、[加载动画词 (Spinner Verbs)](best-practice/claude-settings.md#display--ux) 以获得个性化体验 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny/status/2021701145023197516) |

<a id="tips-daily"></a>■ **日常 (Daily) (2)**

| 技巧 | 来源 |
|-----|--------|
| 每日 [更新 (update)](https://code.claude.com/docs/en/setup) Claude Code | ![Shayan](!/tags/community-shayan.svg) |
| 每天以阅读 [变更日志 (changelog)](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md) 开始你的工作 | ![Shayan](!/tags/community-shayan.svg) |

![Boris Cherny + 团队](!/tags/claude.svg)

| 文章 / 推文 | 来源 |
|-----------------|--------|
| [让 Opus 4.7 发挥最大能力的 6 条技巧 (Boris) \| 26年4月16日](tips/claude-boris-6-tips-16-apr-26.md) | [推文](https://x.com/bcherny) |
| [会话管理与 1M 上下文 (Thariq) \| 26年4月16日](tips/claude-thariq-tips-16-apr-26.md) | [推文](https://x.com/trq212) |
| [Claude Code 中 15 个隐藏且被低估的功能 (Boris) \| 26年3月30日](tips/claude-boris-15-tips-30-mar-26.md) | [推文](https://x.com/bcherny/status/2038454336355999749) |
| [压缩合并与 PR 规模分布 (Boris) \| 26年3月25日](tips/claude-boris-2-tips-25-mar-26.md) | [推文](https://x.com/bcherny/status/2038552880018538749) |
| [构建 Claude Code 的教训：我们如何使用技能 (Thariq) \| 26年3月17日](tips/claude-thariq-tips-17-mar-26.md) | [文章](https://x.com/trq212/status/2033949937936085378) |
| [代码评审与测试时计算 (Boris) \| 26年3月10日](tips/claude-boris-2-tips-10-mar-26.md) | [推文](https://x.com/bcherny/status/2031089411820228645) |
| /loop —— 安排长达 3 天的循环任务 (Boris) \| 2026年3月07日 | [推文](https://x.com/bcherny/status/2030193932404150413) |
| AskUserQuestion + ASCII Markdown (Thariq) \| 2026年2月28日 | [推文](https://x.com/trq212/status/2027543858289250472) |
| 像智能代理一样思考 —— 构建 Claude Code 的教训 (Thariq) \| 2026年2月28日 | [文章](https://x.com/trq212/status/2027463795355095314) |
| Git 工作树 —— Boris 使用它的 5 种方式 \| 2026年2月21日 | [推文](https://x.com/bcherny/status/2025007393290272904) |
| 构建 Claude Code 的教训：提示词缓存即一切 (Thariq) \| 2026年2月20日 | [文章](https://x.com/trq212/status/2024574133011673516) |
| [人们定制 Claude 的 12 种方式 (Boris) \| 26年2月12日](tips/claude-boris-12-tips-12-feb-26.md) | [推文](https://x.com/bcherny/status/2021699851499798911) |
| [来自团队的 10 条 Claude Code 使用技巧 (Boris) \| 26年2月01日](tips/claude-boris-10-tips-01-feb-26.md) | [推文](https://x.com/bcherny/status/2017742741636321619) |
| [我是如何使用 Claude Code 的 —— 来自我个人惊人原生设置的 13 条技巧 (Boris) \| 26年1月03日](tips/claude-boris-13-tips-03-jan-26.md) | [推文](https://x.com/bcherny/status/2007179832300581177) |
| 使用 AskUserQuestion 工具让 Claude 采访你 (Thariq) \| 25年12月28日 | [推文](https://x.com/trq212/status/2005315275026260309) |
| 始终开启计划模式，给 Claude 验证手段，使用 /code-review (Boris) \| 25年12月27日 | [推文](https://x.com/bcherny/status/2004711722926616680) |

<p align="center">
  <img src="!/claude-jumping.svg" alt="分节符" width="60" height="50">
</p>

## 🎬 视频 / 播客

| 视频 / 播客 | 来源 | YouTube 链接 |
|-----------------|--------|---------|
| 我们关于 调研-计划-实现 (RPI) 的所有错误看法 (Dex) \| 2026年3月24日 \| MLOps 社区 | [![Dex](!/tags/community-dex.svg)](https://x.com/daborhyde) | [YouTube](https://youtu.be/YwZR6tc7qYg) |
| 与 Boris Cherny 一起构建 Claude Code (Boris) \| 2026年3月04日 \| The Pragmatic Engineer | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny) | [YouTube](https://youtu.be/julbw1JuAz0) |
| Claude Code 负责人：当编程被解决后会发生什么 (Boris) \| 2026年2月19日 \| Lenny's 播客 | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny) | [YouTube](https://youtu.be/We7BZVKbCVw) |
| 走进 Claude Code 及其创造者 Boris Cherny (Boris) \| 2026年2月17日 \| Y Combinator | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny) | [YouTube](https://youtu.be/PQU9o_5rHC4) |
| Boris Cherny (Claude Code 创造者) 职业生涯是如何成长的 (Boris) \| 2025年12月15日 \| Ryan Peterman | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny) | [YouTube](https://youtu.be/AmdLVWMdjOk) |
| 构建它的工程师们揭秘 Claude Code 的秘密 (Cat) \| 2025年10月29日 \| Every | [![Boris](!/tags/boris-cherny.svg)](https://x.com/bcherny) | [YouTube](https://youtu.be/IDSAMqip6ms) |

<p align="center">
  <img src="!/claude-jumping.svg" alt="分节符" width="60" height="50">
</p>

## 🔔 订阅

| 来源 | 名称 | 勋章 |
|--------|------|-------|
| ![Reddit](https://img.shields.io/badge/-FF4500?style=flat&logo=reddit&logoColor=white) | [r/ClaudeAI](https://www.reddit.com/r/ClaudeAI/), [r/ClaudeCode](https://www.reddit.com/r/ClaudeCode/), [r/Anthropic](https://www.reddit.com/r/Anthropic/) | ![Boris + 团队](!/tags/claude.svg) |
| ![X](https://img.shields.io/badge/-000?style=flat&logo=x&logoColor=white) | [Claude](https://x.com/claudeai), [Claude 开发者](https://x.com/ClaudeDevs), [Anthropic](https://x.com/AnthropicAI), [Boris](https://x.com/bcherny), [Thariq](https://x.com/trq212), [Cat](https://x.com/_catwu), [Lydia](https://x.com/lydiahallie), [Noah](https://x.com/noahzweben), [Anthony](https://x.com/amorriscode), [Alex](https://x.com/alexalbert__), [Kenneth](https://x.com/neilhtennek) | ![Boris + 团队](!/tags/claude.svg) |
| ![X](https://img.shields.io/badge/-000?style=flat&logo=x&logoColor=white) | [Jesse Kriss](https://x.com/obra) ([Superpowers](https://github.com/obra/superpowers)), [Affaan Mustafa](https://x.com/affaanmustafa) ([ECC](https://github.com/affaan-m/everything-claude-code)), [Garry Tan](https://x.com/garrytan) ([gstack](https://github.com/garrytan/gstack)), [Dex Horthy](https://x.com/dexhorthy) ([HumanLayer](https://github.com/humanlayer/humanlayer)), [Kieran Klaassen](https://x.com/kieranklaassen) ([Compound Eng](https://github.com/EveryInc/compound-engineering-plugin)), [Tabish Gilani](https://x.com/0xTab) ([OpenSpec](https://github.com/Fission-AI/OpenSpec)), [Brian McAdams](https://x.com/BMadCode) ([BMAD](https://github.com/bmad-code-org/BMAD-METHOD)), [Lex Christopherson](https://x.com/official_taches) ([GSD](https://github.com/gsd-build/get-shit-done)), [Dani Avila](https://x.com/dani_avila7) ([CC Templates](https://github.com/davila7/claude-code-templates)), [Dan Shipper](https://x.com/danshipper) ([Every](https://every.to/)), [Andrej Karpathy](https://x.com/karpathy) ([AutoResearch](https://x.com/karpathy/status/2015883857489522876)), [Peter Steinberger](https://x.com/steipete) ([OpenClaw](https://x.com/openclaw)), [Sigrid Jin](https://x.com/realsigridjin) ([claw-code](https://github.com/ultraworkers/claw-code)), [Yeachan Heo](https://x.com/bellman_ych) ([oh-my-claudecode](https://github.com/Yeachan-Heo/oh-my-claudecode)) | ![社区](!/tags/community.svg) |
| ![YouTube](https://img.shields.io/badge/-F00?style=flat&logo=youtube&logoColor=white) | [Anthropic](https://www.youtube.com/@anthropic-ai) | ![Boris + 团队](!/tags/claude.svg) |
| ![YouTube](https://img.shields.io/badge/-F00?style=flat&logo=youtube&logoColor=white) | [Lenny's 播客](https://www.youtube.com/@LennysPodcast), [Y Combinator](https://www.youtube.com/@ycombinator), [The Pragmatic Engineer](https://www.youtube.com/@pragmaticengineer), [Ryan Peterman](https://www.youtube.com/@ryanlpeterman), [Every](https://www.youtube.com/@every_media), [MLOps 社区](https://www.youtube.com/@MLOps) | ![社区](!/tags/community.svg) |

<p align="center">
  <img src="!/claude-jumping.svg" alt="分节符" width="60" height="50">
</p>

## ☠️ 被替代的初创公司 / 业务 (STARTUPS / BUSINESSES)

| Claude 功能 | 替代了... |
||-|-|
|[**代码评审**](https://code.claude.com/docs/en/code-review)|[Greptile](https://greptile.com), [CodeRabbit](https://coderabbit.ai), [Devin Review](https://devin.ai), [OpenDiff](https://opendiff.com), [Cursor BugBot](https://bugbot.dev)|
|[**语音听写**](https://code.claude.com/docs/en/voice-dictation)|[Wispr Flow](https://wisprflow.ai), [SuperWhisper](https://superwhisper.com/)|
|[**远程控制**](https://code.claude.com/docs/en/remote-control)|[OpenClaw](https://openclaw.ai/)
|[**Chrome 中的 Claude**](https://code.claude.com/docs/en/chrome)|[Playwright MCP](https://github.com/microsoft/playwright-mcp), [Chrome DevTools MCP](https://developer.chrome.com/blog/chrome-devtools-mcp)|
|[**电脑操作**](https://docs.anthropic.com/en/docs/agents-and-tools/computer-use)|[OpenAI CUA](https://openai.com/index/computer-using-agent/)|
|[**协同办公**](https://claude.com/blog/cowork-research-preview)|[ChatGPT 代理](https://openai.com/chatgpt/agent/), [Perplexity 电脑](https://www.perplexity.ai/computer/), [Manus](https://manus.im)|
|[**任务管理**](https://x.com/trq212/status/2014480496013803643)|[Beads](https://github.com/steveyegge/beads)
|[**计划模式**](https://code.claude.com/docs/en/common-workflows)|[Agent OS](https://github.com/buildermethods/agent-os)|
|[**技能 / 插件**](https://code.claude.com/docs/en/plugins)|YC AI 套壳类初创公司 ([reddit 讨论](https://reddit.com/r/ClaudeAI/comments/1r6bh4d/claude_code_skills_are_basically_yc_ai_startup/))|

<p align="center">
  <img src="!/claude-jumping.svg" alt="分节符" width="60" height="50">
</p>

<a id="billion-dollar-questions"></a>
![价值十亿美元的问题](!/tags/billion-dollar-questions.svg)

*如果你有答案，请通过 shanraisshan@gmail.com 告诉开发者*

**记忆与指令 (4)**

1. CLAUDE.md 里面到底应该放什么 —— 以及应该省掉什么？
2. 如果已经有了 CLAUDE.md，是否还需要单独的 constitution.md 或 rules.md？
3. 你应该多久更新一次 CLAUDE.md，以及如何判断它已经过时了？
4. 为什么 Claude 仍然会忽略 CLAUDE.md 指令 —— 即使使用了大写的 MUST？([reddit 上的案例](https://reddit.com/r/ClaudeCode/comments/1qn9pb9/claudemd_says_must_use_agent_claude_ignores_it_80/))

**代理、技能与工作流 (6)**

1. 什么时候应该使用命令，什么时候用代理，什么时候用技能 —— 什么时候用原生 Claude Code 就行了？
2. 随着模型改进，你应该多久更新一次代理、命令和工作流？
3. 应该使用通用型子代理还是特定功能/角色型代理？赋予子代理详细的人格是否能提高质量？用于调研/视觉的 “完美人格提示词” 长什么样？
4. 你应该依赖 Claude Code 内置的计划模式 —— 还是构建自己的计划命令/代理来强制执行团队的工作流？
5. 如果你有个人专属技能（例如：/implement 以匹配你的编码风格），如何集成社区技能（例如：/simplify）而不产生冲突 —— 当它们发生分歧时谁说了算？
6. 我们达到了吗？能否将现有代码库转化为规格说明 (specs)，删除代码，然后让 AI 仅凭这些规格说明重新生成完全一致的代码？

**规格与文档 (3)**

1. 仓库中的每个功能都应该有一个 markdown 格式的规格文件吗？
2. 当实现新功能时，你需要多久更新一次规格以防其过时？
3. 实现新功能时，如何处理对其他功能规格产生的连漪效应 (ripple effect)？

<p align="center">
  <img src="!/claude-jumping.svg" alt="分节符" width="60" height="50">
</p>

## 专题报告 (REPORTS)

<p align="center">
  <a href="reports/claude-agent-sdk-vs-cli-system-prompts.md"><img src="https://img.shields.io/badge/Agent_SDK_对标_CLI-555?style=for-the-badge" alt="Agent SDK vs CLI"></a>
  <a href="reports/claude-in-chrome-v-chrome-devtools-mcp.md"><img src="https://img.shields.io/badge/浏览器自动化_MCP-555?style=for-the-badge" alt="Browser Automation MCP"></a>
  <a href="reports/claude-global-vs-project-settings.md"><img src="https://img.shields.io/badge/全局对比项目设置-555?style=for-the-badge" alt="Global vs Project Settings"></a>
  <a href="reports/claude-skills-for-larger-mono-repos.md"><img src="https://img.shields.io/badge/单体大仓中的技能管理-555?style=for-the-badge" alt="Skills in Monorepos"></a>
  <br>
  <a href="reports/claude-agent-memory.md"><img src="https://img.shields.io/badge/代理记忆-555?style=for-the-badge" alt="Agent Memory"></a>
  <a href="reports/claude-advanced-tool-use.md"><img src="https://img.shields.io/badge/高级工具使用-555?style=for-the-badge" alt="Advanced Tool Use"></a>
  <a href="reports/claude-usage-and-rate-limits.md"><img src="https://img.shields.io/badge/使用额度与速率限制-555?style=for-the-badge" alt="Usage & Rate Limits"></a>
  <a href="reports/claude-agent-command-skill.md"><img src="https://img.shields.io/badge/代理对比命令对比技能-555?style=for-the-badge" alt="Agents vs Commands vs Skills"></a>
  <br>
  <a href="reports/llm-day-to-day-degradation.md"><img src="https://img.shields.io/badge/LLM_能力衰减研究-555?style=for-the-badge" alt="LLM Degradation"></a>
</p>

<p align="center">
  <img src="!/claude-jumping.svg" alt="分节符" width="60" height="50">
</p>

![如何使用](!/tags/how-to-use.svg)

```
1. 像读课程一样阅读本仓库，在尝试使用之前先了解什么是命令、代理、技能和钩子。
2. 克隆本仓库并尝试运行示例，尝试执行 /weather-orchestrator，倾听钩子的声音，运行代理团队，这样你就能看到事物实际上是如何运作的。
3. 回到你自己的项目，让 Claude 根据本仓库的最佳实践提出建议，将本仓库作为参考喂给它，让它知道什么是可能的。
```

<a href="https://www.youtube.com/watch?v=AkAhkalkRY4"><img src="!/thumbnail/video-1.png" alt="在 YouTube 上观看" width="300"></a>

<p align="center">
  <img src="!/claude-jumping.svg" alt="分节符" width="60" height="50">
</p>

<p align="center">
  <a href="https://github.com/trending?since=monthly"><img src="!/root/github-trending.png" alt="GitHub 趋势榜" width="1200"></a><br>
  ✨2026 年 3 月 GitHub 趋势榜热门项目✨
</p>

## 其他仓库

<a href="https://github.com/shanraisshan/claude-code-hooks"><img src="!/claude-speaking.svg" alt="Claude Code Hooks" width="40" height="40" align="center"></a> <a href="https://github.com/shanraisshan/claude-code-hooks"><strong>claude-code-hooks</strong></a> · <a href="https://github.com/shanraisshan/codex-cli-best-practice"><img src="!/codex-jumping.svg" alt="Codex CLI" width="40" height="40" align="center"></a> <a href="https://github.com/shanraisshan/codex-cli-best-practice"><strong>codex-cli-best-practice</strong></a> · <a href="https://github.com/shanraisshan/codex-cli-hooks"><img src="!/codex-speaking.svg" alt="Codex CLI Hooks" width="40" height="40" align="center"></a> <a href="https://github.com/shanraisshan/codex-cli-hooks"><strong>codex-cli-hooks</strong></a>

## 开发方式

![由...开发](!/tags/developed-by.svg)

> | # | 工作流 | 描述 |
> |---|----------|-------------|
> | 1 | /workflows:development-workflows | 通过并行研究所有 10 个工作流仓库，更新开发工作流表和跨工作流分析报告 |
> | 2 | /workflows:best-practice:workflow-concepts | 使用最新的 Claude Code 功能和概念更新 README 核心概念章节 |
> | 3 | /workflows:best-practice:workflow-claude-settings | 跟踪 Claude Code 设置报告的变化并寻找需要更新的内容 |
> | 4 | /workflows:best-practice:workflow-claude-subagents | 跟踪 Claude Code 子代理报告的变化并寻找需要更新的内容 |
> | 5 | /workflows:best-practice:workflow-claude-commands | 跟踪 Claude Code 命令报告的变化并寻找需要更新的内容 |
> | 6 | /workflows:best-practice:workflow-claude-skills | 跟踪 Claude Code 技能报告的变化并寻找需要更新的内容 |

[![Claude 开源计划](!/tags/claude-for-oss.svg)](https://claude.com/contact-sales/claude-for-oss)
[![Claude 社区大使](!/tags/claude-community-ambassador.svg)](https://claude.com/community/ambassadors)
[![Claude 认证架构师](!/tags/claude-certified-architect.svg)](https://anthropic.skilljar.com/claude-certified-architect-foundations-access-request)
[![Anthropic 学院](!/tags/anthropic-academy.svg)](https://anthropic.skilljar.com/)

## 星标历史 (Star History)

[![星标历史图表](https://api.star-history.com/svg?repos=shanraisshan/claude-code-best-practice&type=Date)](https://star-history.com/#shanraisshan/claude-code-best-practice&Date)

<a href="https://github.com/shanraisshan/claude-code-best-practice/stargazers"><img src="https://img.shields.io/github/stars/shanraisshan/claude-code-best-practice?style=flat&label=%E2%98%85&labelColor=555&color=white" alt="GitHub 星标数" align="center"></a> 颗星，持续增长中

<p align="center">
  <img src="!/claude-jumping.svg" alt="分节符" width="60" height="50">
</p>

## <img src="!/tags/sponsor-heart.svg" width="22" height="22" align="center"> 赞助我的工作

如果你喜欢我的工作，请我在 Polar 上喝杯奶茶 (doodh patti) 🍵

<a href="https://buy.polar.sh/polar_cl_R6wjUESl8RiJD0iVaTyStBUV6WNuYvDmLJ0si1XXj4C"><img src="!/tags/polar.svg" alt="Polar" width="40" height="40" align="center"></a> <a href="https://buy.polar.sh/polar_cl_R6wjUESl8RiJD0iVaTyStBUV6WNuYvDmLJ0si1XXj4C"><strong>Polar</strong></a>