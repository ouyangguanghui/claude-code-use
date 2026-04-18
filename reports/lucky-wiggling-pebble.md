# 项目结构分析：claude-code-best-practice

## 项目定位

这是一个 **Claude Code 配置最佳实践参考仓库**，不是应用代码库。它演示了 Claude Code 的 Skills（技能）、Subagents（子代理）、Hooks（钩子）、Commands（命令）等高级配置模式，同时维护了一套对官方文档进行持续漂移检测的工作流系统。

---

## 一、根目录文件

| 文件 | 作用 |
|------|------|
| `README.md` | 项目主页 —— 包含 CONCEPTS 表（Claude Code 核心概念与官方文档链接）、TIPS 表（来自 Anthropic 工程师的使用建议）、仓库徽章导航 |
| `CLAUDE.md` | Claude Code 的项目指令文件 —— 告诉 Claude 如何理解和操作本仓库（架构概览、提交规则、代理调用模式等） |
| `.mcp.json` | MCP (Model Context Protocol) 服务器配置 —— 定义了 Playwright、Context7、DeepWiki 等外部工具集成 |
| `.gitignore` | Git 忽略规则 |
| `LICENSE` | 开源许可证 |

---

## 二、`.claude/` — Claude Code 配置核心

这是整个仓库的**引擎室**，定义了 Claude Code 的所有行为扩展。

### 2.1 `agents/` — 子代理定义（12 个）

| 文件 | 模型 | 作用 |
|------|------|------|
| `weather-agent.md` | inherit | 天气数据获取代理，预加载 `weather-fetcher` 技能，演示"代理技能模式" |
| `time-agent.md` | inherit | 显示巴基斯坦时间（PKT），演示简单代理 |
| `presentation-vibe-coding.md` | inherit | 专门维护 vibe-coding 演示幻灯片的代理 |
| `presentation-learning-journey.md` | inherit | 专门维护 learning-journey 演示幻灯片的代理 |
| `development-workflows-research-agent.md` | inherit | 研究代理，负责获取 GitHub 仓库数据、分析工作流仓库 |
| `workflows/best-practice/workflow-claude-commands-agent.md` | sonnet | 命令报告漂移检测代理 |
| `workflows/best-practice/workflow-claude-settings-agent.md` | sonnet | 设置报告漂移检测代理 |
| `workflows/best-practice/workflow-claude-skills-agent.md` | sonnet | 技能报告漂移检测代理 |
| `workflows/best-practice/workflow-claude-subagents-agent.md` | sonnet | 子代理报告漂移检测代理 |
| `workflows/best-practice/workflow-concepts-agent.md` | sonnet | README CONCEPTS 表漂移检测代理 |
| `workflows/development-workflows-research-agent.md` | — | 开发工作流漂移检测代理 |

**设计模式**：工作流代理（`workflows/`）采用 Sonnet 模型以节省成本，通过 `skills:` 字段预加载对应技能获取背景知识，每个代理只关注一个报告文件的漂移检测。

### 2.2 `commands/` — 斜杠命令（8 个）

| 文件 | 作用 |
|------|------|
| `weather-orchestrator.md` | `/weather-orchestrator` —— 天气编排入口，询问温度单位→调用代理→生成SVG |
| `time-command.md` | `/time-command` —— 时间查询入口 |
| `workflows/best-practice/workflow-claude-commands.md` | `/workflow-claude-commands` —— 触发命令报告漂移检测工作流 |
| `workflows/best-practice/workflow-claude-settings.md` | `/workflow-claude-settings` —— 触发设置报告漂移检测工作流 |
| `workflows/best-practice/workflow-claude-skills.md` | `/workflow-claude-skills` —— 触发技能报告漂移检测工作流 |
| `workflows/best-practice/workflow-claude-subagents.md` | `/workflow-claude-subagents` —— 触发子代理报告漂移检测工作流 |
| `workflows/best-practice/workflow-concepts.md` | `/workflow-concepts` —— 触发 CONCEPTS 表漂移检测工作流 |
| `workflows/development-workflows.md` | `/workflow-development-workflows` —— 触发开发工作流漂移检测 |

**架构关系**：`命令` → 调用 `代理` → 代理使用 `技能` 获取数据。这是 **Command → Agent → Skill** 的三层编排模式。

### 2.3 `skills/` — 技能定义（7 个）

| 技能 | 文件 | 作用 |
|------|------|------|
| `weather-fetcher` | `SKILL.md` | 从 Open-Meteo API 获取迪拜天气温度 |
| `weather-svg-creator` | `SKILL.md` + `examples.md` + `reference.md` | 根据温度数据创建 SVG 天气卡片 |
| `time-skill` | `SKILL.md` | 获取并显示巴基斯坦时间 |
| `agent-browser` | `SKILL.md` | 浏览器自动化技能 |
| `presentation/presentation-structure` | `SKILL.md` | 演示文稿结构技能 |
| `presentation/presentation-styling` | `SKILL.md` | 演示文稿样式技能 |
| `presentation/vibe-to-agentic-framework` | `SKILL.md` | vibe-coding 演示框架技能 |

**两种技能模式**：
1. **代理技能**（Agent Skill）：通过代理的 `skills:` 字段预加载，如 `weather-fetcher` 预加载到 `weather-agent`
2. **普通技能**（Invocable Skill）：通过 `Skill` 工具调用，如 `weather-svg-creator`

### 2.4 `rules/` — 规则文件（2 个）

| 文件 | 作用 |
|------|------|
| `markdown-docs.md` | 匹配 `**/*.md` —— 文档标准（目录结构、链接格式、徽章使用规范） |
| `presentation.md` | 匹配 `presentation/**` —— 强制将演示文稿修改委派给专用代理 |

### 2.5 `hooks/` — 钩子系统

跨平台声音通知系统，为 27 种 Claude Code 事件提供音效反馈：

| 组件 | 作用 |
|------|------|
| `scripts/hooks.py` | Python 主处理器 —— 解析钩子事件、匹配声音文件、播放音效 |
| `config/hooks-config.json` | 团队共享配置（启用/禁用特定钩子、音量设置） |
| `sounds/` | 27 个事件目录，每个包含 `.mp3` + `.wav` 格式的音效文件 |
| `HOOKS-README.md` | 钩子系统的使用文档 |

特殊处理：`pretooluse` 目录包含额外的 `pretooluse-git-committing` 音效，在 git commit 时触发特定声音。

### 2.6 其他

| 文件 | 作用 |
|------|------|
| `settings.json` | 团队共享的 Claude Code 设置（钩子事件绑定、权限规则、MCP 配置等） |
| `agent-memory/weather-agent/MEMORY.md` | weather-agent 的持久化记忆文件 |
| `.gitignore` | 忽略 `settings.local.json`、`hooks-config.local.json` 等个人配置 |

---

## 三、`best-practice/` — 最佳实践报告（8 个文档）

本仓库的**知识库核心**，对 Claude Code 各功能领域进行系统化整理。

| 文件 | 内容 |
|------|------|
| `claude-commands.md` | 斜杠命令完全指南 —— 命令定义结构、内置命令参考、前置元数据字段 |
| `claude-settings.md` | 设置完全指南 —— 5 级设置层级、所有设置键、权限模式、环境变量 |
| `claude-skills.md` | 技能完全指南 —— 技能定义结构、前置元数据字段、两种技能模式 |
| `claude-subagents.md` | 子代理完全指南 —— 子代理定义结构、钩子集成、内置代理列表 |
| `claude-memory.md` | 记忆系统指南 —— 自动记忆、记忆文件结构、作用域 |
| `claude-mcp.md` | MCP 服务器指南 —— 配置方式、服务器类型、安全设置 |
| `claude-power-ups.md` | 高级功能指南 —— 模型切换、Extended thinking、会话恢复等 |
| `claude-cli-startup-flags.md` | CLI 启动参数指南 —— 命令行标志、环境变量、启动配置 |

这些文件是工作流漂移检测系统的**被监控目标** —— 每个报告都与官方文档进行对比验证。

---

## 四、`changelog/` — 变更日志与验证清单

记录每次漂移检测工作流运行的结果，防止知识腐化。

```
changelog/
├── best-practice/
│   ├── claude-commands/
│   │   └── changelog.md          # 命令报告的漂移检测历史
│   ├── claude-settings/
│   │   ├── changelog.md          # 设置报告的漂移检测历史
│   │   └── verification-checklist.md  # 验证规则清单（31条规则，10个类别）
│   ├── claude-skills/
│   │   └── changelog.md          # 技能报告的漂移检测历史
│   ├── claude-subagents/
│   │   ├── changelog.md          # 子代理报告的漂移检测历史
│   │   └── verification-checklist.md  # 验证规则清单（8个类别）
│   └── concepts/
│       ├── changelog.md          # CONCEPTS 表的漂移检测历史
│       └── verification-checklist.md  # 验证规则清单（6条规则）
└── development-workflows/
    └── changelog.md              # 开发工作流的漂移检测历史
```

**设计理念**：验证清单按"深度级别"分层（`exists` → `presence-check` → `content-match` → `field-level` → `cross-file`），规则随时间积累，每次发现新的偏差类型就追加新规则。这是一个自我进化的质量保障系统。

---

## 五、`reports/` — 深度研究报告（10 个）

| 文件 | 主题 |
|------|------|
| `claude-agent-command-skill.md` | Agent、Command、Skill 三者关系解析 |
| `claude-agent-memory.md` | 代理记忆机制深度分析 |
| `claude-agent-sdk-vs-cli-system-prompts.md` | Agent SDK vs CLI 系统提示词对比 |
| `claude-advanced-tool-use.md` | 高级工具使用模式 |
| `claude-global-vs-project-settings.md` | 全局设置 vs 项目设置对比 |
| `claude-in-chrome-v-chrome-devtools-mcp.md` | Chrome 集成 vs DevTools MCP 对比 |
| `claude-skills-for-larger-mono-repos.md` | 大型单体仓库中的技能管理策略 |
| `claude-usage-and-rate-limits.md` | 使用量和速率限制分析 |
| `llm-day-to-day-degradation.md` | LLM 日常性能衰退观察 |

---

## 六、`implementation/` — 实现指南（5 个）

| 文件 | 主题 |
|------|------|
| `claude-commands-implementation.md` | 如何实现自定义命令 |
| `claude-skills-implementation.md` | 如何实现自定义技能 |
| `claude-subagents-implementation.md` | 如何实现自定义子代理 |
| `claude-agent-teams-implementation.md` | 如何实现代理团队编排 |
| `claude-scheduled-tasks-implementation.md` | 如何实现定时任务 |

---

## 七、`tips/` — Anthropic 工程师使用建议（8 个）

收集自 Boris Cherny（Claude Code 工程主管）和 Thariq（Anthropic 工程师）的社交媒体帖子，每个文件附带截图。

| 文件 | 来源 | 要点数量 |
|------|------|----------|
| `claude-boris-13-tips-03-jan-26.md` | Boris, 2026-01-03 | 13 条 |
| `claude-boris-10-tips-01-feb-26.md` | Boris, 2026-02-01 | 10 条 |
| `claude-boris-12-tips-12-feb-26.md` | Boris, 2026-02-12 | 12 条 |
| `claude-boris-2-tips-10-mar-26.md` | Boris, 2026-03-10 | 2 条 |
| `claude-boris-2-tips-25-mar-26.md` | Boris, 2026-03-25 | 2 条 |
| `claude-boris-15-tips-30-mar-26.md` | Boris, 2026-03-30 | 15 条 |
| `claude-boris-6-tips-16-apr-26.md` | Boris, 2026-04-16 | 6 条 |
| `claude-thariq-tips-17-mar-26.md` | Thariq, 2026-03-17 | 多条 |
| `claude-thariq-tips-16-apr-26.md` | Thariq, 2026-04-16 | 多条 |

---

## 八、`videos/` — 视频笔记（6 个）

| 文件 | 视频来源 |
|------|----------|
| `claude-boris-lennys-podcast-19-feb-26.md` | Lenny's Podcast 访谈 |
| `claude-boris-pragmatic-engineer-04-mar-26.md` | Pragmatic Engineer 访谈 |
| `claude-boris-ryan-peterman-15-dec-25.md` | Ryan Peterman 访谈 |
| `claude-boris-y-combinator-17-feb-26.md` | Y Combinator 访谈 |
| `claude-cat-every-29-oct-25.md` | Cat Wu (Every) 演讲 |
| `claude-dex-mlops-community-24-mar-26.md` | Dex (MLOps Community) 演讲 |

---

## 九、`tutorial/` — 入门教程

| 文件 | 内容 |
|------|------|
| `day0/README.md` | 第0天：安装和环境配置概览 |
| `day0/mac.md` | macOS 安装步骤 |
| `day0/linux.md` | Linux 安装步骤 |
| `day0/windows.md` | Windows 安装步骤 |
| `day1/README.md` | 第1天：Claude Code 基础使用 |

---

## 十、`orchestration-workflow/` — 编排工作流演示

| 文件 | 作用 |
|------|------|
| `orchestration-workflow.md` | 完整的 Command → Agent → Skill 流程图和架构说明 |
| `orchestration-workflow.svg` | 流程图 SVG |
| `weather.svg` | 天气工作流生成的 SVG 输出 |
| `output.md` | 工作流执行结果摘要 |

---

## 十一、`development-workflows/` — 开发工作流

### 11.1 `rpi/` — RPI 工作流

**RPI** = Research → Plan → Implement（研究→规划→实现），带有验证门控的系统化开发方法：
- 自带独立的 `.claude/` 配置（代理 + 命令），可复制到任何仓库使用
- 三步流程：`/rpi:research` → `/rpi:plan` → `/rpi:implement`
- 每步有专用代理团队（如研究阶段使用 6 个代理并行分析）

### 11.2 `cross-model-workflow/` — 跨模型工作流

Claude Code (Opus) + Codex CLI (GPT) 双模型协作：
1. Claude 规划 → 2. Codex QA 审查 → 3. Claude 实现 → 4. Codex 验证

---

## 十二、`agent-teams/` — 代理团队演示

| 文件 | 作用 |
|------|------|
| `agent-teams-prompt.md` | 多代理团队规范 —— 定义 time-agent 和 weather-agent 的并行编排 |
| `output/output.md` | 代理团队执行输出 |
| `output/dubai-time.svg` | 生成的时间卡片 SVG |
| `.claude/` | 独立的代理/技能/命令配置（可复制到其他项目） |

---

## 十三、`presentation/` — 演示文稿

| 演示 | 文件 | 受众 |
|------|------|------|
| Vibe Coding → Agentic Engineering | `vibe-coding-to-agentic-engineering/index.html` | 技术人员 |
| Claude Code Learning Journey | `learning-journey/index.html` | 非技术人员（6级2天学习体系） |

由专用子代理维护，禁止直接编辑 HTML。

---

## 十四、`.codex/` — Codex CLI 配置

与 `.claude/` 平行的 OpenAI Codex CLI 配置，包含类似的钩子系统（5 个事件）和声音通知。用于跨模型工作流。

---

## 十五、`!/` — 静态资源

| 子目录 | 内容 |
|--------|------|
| `root/` | 仓库成就徽章 SVG（如 GitHub trending） |
| `tags/` | 文档分类标签 SVG（如 best-practice、implemented 等） |
| `thumbnail/` | 缩略图资源 |
| `claude-jumping.svg` / `claude-speaking.svg` | Claude 角色插图 |
| `codex-jumping.svg` / `codex-speaking.svg` | Codex 角色插图 |
| `video-presentation-transcript/` | 视频演示脚本 |

---

## 整体架构总结

```
用户 ──→ /命令 ──→ 代理（Agent）──→ 技能（Skill）──→ 外部 API / 文件操作
              │
              ├── 天气工作流：/weather-orchestrator → weather-agent → weather-fetcher + weather-svg-creator
              ├── 时间工作流：/time-command → time-agent → time-skill
              └── 漂移检测：/workflow-* → workflow-*-agent → 对比官方文档 → 更新 changelog
                                                               ↓
                                                    verification-checklist（验证规则自我进化）
```

**核心价值**：这个仓库不只是文档集合，它是一个**活的系统** —— 通过漂移检测工作流持续对比官方文档，确保知识不腐化；通过验证清单的规则积累，让质量保障随时间自我进化。
