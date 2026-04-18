# 计划：Claude Code 从零到精通教程

## Context

用户是视觉/VLA/机器人算法工程师，希望基于本项目整理一份详细的 Claude Code 教程，从零基础到精通，以便应用到自己的 ML/机器人项目中。

本仓库已有丰富的参考材料（8 篇 best-practice、9 篇 reports、9 篇 tips、5 篇 implementation、完整的 .claude/ 配置示例），但现有 tutorial/ 仅覆盖安装（day0）和概念入门（day1）。需要将散落的知识整合为一份渐进式、面向 ML/机器人工程师的完整教程。

另外，还有 12 个已翻译的 agent 文件需要先提交 git commit（每个文件单独提交）。

---

## 输出文件

`tutorial/claude-code-zero-to-mastery.md` — 单一中文 markdown 文件，约 2000-2200 行

---

## 教程结构（13 部分 + 4 附录）

### 阅读指南 (~20 行)
- 适用人群、阅读方式、标记符号说明

### Part 0: 准备工作 (~60 行)
- 链接到 day0/ 安装指南，不重复内容
- 三种认证方式、首次启动验证
- 来源：`tutorial/day0/`

### Part 1: 基础对话 (~120 行)
- @-文件引用、自然语言提问、代码理解
- **机器人示例**：解释 CUDA kernel、分析 ROS 节点、理解 VLA 模型
- 来源：`tutorial/day1/README.md`、Boris tip #10

### Part 2: CLAUDE.md 项目记忆 (~170 行)
- 为什么重要、写什么内容、加载机制、迭代改进
- **机器人示例**：完整的机器人视觉导航项目 CLAUDE.md 模板
- 来源：`best-practice/claude-memory.md`、Boris tip #3/#4/#5

### Part 3: 上下文管理 (~180 行)
- 上下文窗口概念、/context 命令、300-400K 腐化阈值
- 5 个决策点、回退 vs 纠正、/compact vs /clear、会话分支
- **机器人示例**：训练脚本长时间调试时的上下文管理策略
- 来源：`tips/claude-thariq-tips-16-apr-26.md`（主要来源）、Boris tips

### Part 4: 命令系统 (~160 行)
- 70+ 内置命令精选、创建自定义命令、14 个前置元数据字段
- **机器人示例**：自定义 `/train-debug` 命令（诊断训练失败）
- 来源：`best-practice/claude-commands.md`、`implementation/claude-commands-implementation.md`

### Part 5: 技能系统 (~200 行)
- 两种模式、5 个官方技能、14 字段、Thariq 的 9 种类别 + 9 个制作提示
- **机器人示例**：`/evaluate-model` 技能（标准化评估流程）
- 来源：`best-practice/claude-skills.md`、`tips/claude-thariq-tips-17-mar-26.md`

### Part 6: 子代理系统 (~170 行)
- 5 种官方类型、16 字段、创建自定义代理、记忆持久化
- **机器人示例**：`dataset-validator` 代理（数据集完整性检查）
- 来源：`best-practice/claude-subagents.md`、`implementation/claude-subagents-implementation.md`

### Part 7: MCP 服务器 (~120 行)
- Top 5 MCP、配置方法、作用域层级
- **机器人示例**：Context7 查 PyTorch/ROS 文档、Playwright 监控 W&B
- 来源：`best-practice/claude-mcp.md`

### Part 8: 钩子系统 (~150 行)
- 27 个事件精选 8 个、4 种处理器类型、匹配器模式
- **机器人示例**：提交前自动 ruff/black、启动时激活 conda 环境
- 来源：`.claude/hooks/HOOKS-README.md`

### Part 9: 设置与配置 (~130 行)
- 5 层层级、精选 15 个最重要设置、权限管理
- **机器人示例**：机器人实验室团队设置模板
- 来源：`best-practice/claude-settings.md`

### Part 10: 工作流编排 (~170 行)
- Command → Agent → Skill 管道、代理团队、/loop、工作树隔离
- **机器人示例**：自动化夜间模型评估管线
- 来源：`implementation/claude-agent-teams-implementation.md`、`implementation/claude-scheduled-tasks-implementation.md`

### Part 11: 高级技巧 (~150 行)
- Boris/Thariq 实战精华：验证模式、测试时间算力、小 PR 策略、/powerup
- 来源：`tips/` 全部 9 个文件精选、`best-practice/claude-power-ups.md`

### Part 12: 实战项目 (~200 行)
- 完整演练：从零配置一个视觉导航机器人项目的 Claude Code 环境
- 创建 CLAUDE.md → settings → commands → skills → agents → hooks → MCP → 编排

### 附录 A: 命令速查表 (~60 行)
### 附录 B: 前置元数据字段参考 (~50 行)
### 附录 C: 常见问题与故障排除 (~40 行)
### 附录 D: 本仓库文件索引 (~40 行)

---

## 关键设计决策

1. **单文件**而非多天目录 — 方便全文搜索和离线阅读
2. **每个 Part 都有机器人/CV/ML 场景示例** — 不是通用教程
3. **引用而非复制** — 用相对链接指向 best-practice/ 和 tips/ 原文，避免内容重复
4. **一致的节格式**：概念说明 → 实战示例 → 专家提示 → 陷阱提醒
5. **中文撰写**，技术术语保留英文（PyTorch、CUDA、ROS 等）

---

## 关键来源文件（实现时需读取）

| 优先级 | 文件 | 用于 |
|--------|------|------|
| 1 | `tips/claude-thariq-tips-16-apr-26.md` | Part 3 上下文管理 |
| 2 | `tips/claude-thariq-tips-17-mar-26.md` | Part 5 技能 9 类别 |
| 3 | `best-practice/claude-commands.md` | Part 4 命令系统 |
| 4 | `best-practice/claude-skills.md` | Part 5 技能系统 |
| 5 | `best-practice/claude-subagents.md` | Part 6 子代理 |
| 6 | `best-practice/claude-settings.md` | Part 9 设置 |
| 7 | `best-practice/claude-mcp.md` | Part 7 MCP |
| 8 | `.claude/hooks/HOOKS-README.md` | Part 8 钩子 |
| 9 | `tips/claude-boris-15-tips-30-mar-26.md` | Part 10-11 高级 |
| 10 | `tips/claude-boris-10-tips-01-feb-26.md` | Part 2,3,5,6 |
| 11 | `.claude/commands/weather-orchestrator.md` | Part 4 参考实现 |
| 12 | `.claude/agents/weather-agent.md` | Part 6 参考实现 |
| 13 | `.claude/skills/weather-fetcher/SKILL.md` | Part 5 参考实现 |

---

## 实现步骤

1. **先完成 git commits** — 12 个已翻译的 agent 文件，每个单独提交
2. **读取关键来源文件** — 上表中优先级 1-8 的文件
3. **写骨架** — 目录、标题、阅读指南
4. **写 Part 0-3** — 基础部分（安装、对话、CLAUDE.md、上下文）
5. **写 Part 4-8** — 系统部分（命令、技能、代理、MCP、钩子）
6. **写 Part 9-10** — 配置与编排
7. **写 Part 11-12** — 高级技巧与实战项目
8. **写附录** — 速查表、参考表、FAQ
9. **验证** — 链接完整性、术语一致性、行数检查

---

## 验证标准

- [ ] 所有 8 篇 best-practice 文件至少引用一次
- [ ] 所有 9 篇 tips 文件至少引用一次
- [ ] 每个 Part 有至少一个机器人/CV/ML 示例
- [ ] 所有相对链接路径存在
- [ ] 中文术语全文一致
- [ ] 总行数 2000-2200 范围
- [ ] 渐进难度：不依赖后续章节知识
