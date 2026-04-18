# Subagent 报告 — 变更日志历史

## 状态图例

| 状态 | 含义 |
|--------|---------|
| ✅ `COMPLETE (原因)` | 已采取操作并成功解决 |
| ❌ `INVALID (原因)` | 发现不正确、不适用或为有意设计 |
| ✋ `ON HOLD (原因)` | 操作已推迟 — 等待外部依赖或用户决定 |

---

## [2026-02-28 03:22 PM PKT] Claude Code v2.1.63

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | Agent 表格 | 将 `workflow-changelog-claude-agents-frontmatter-agent` 添加到本仓库 Agent 表格 | ✅ COMPLETE (已添加，model: opus，继承所有工具，无 skills/memory) |
| 2 | HIGH | Agent 表格 | 修复 presentation-curator 的 skills 列 — 为技能名称添加 `presentation/` 前缀 | ✅ COMPLETE (已更新为 presentation/vibe-to-agentic-framework 等) |
| 3 | MED | 字段文档 | 为 `color` 字段添加备注，说明该字段功能可用但未出现在官方前置元数据表中 | ✅ COMPLETE (已在描述列中添加非官方状态备注) |
| 4 | MED | 调用章节 | 扩展调用章节，包含 --agents CLI 标志、/agents 命令、claude agents CLI、Agent 恢复 | ✅ COMPLETE (已添加包含 5 种方法的调用方式表格) |

---

## [2026-03-07 08:35 AM PKT] Claude Code v2.1.71

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 失效链接 | 修复 Agent memory 链接到 `reports/claude-agent-memory.md` | ✅ COMPLETE |
| 2 | HIGH | 行为变更 | 更新 `tools` 字段描述：`Task(agent_type)` → `Agent(agent_type)` (v2.1.63 重命名) | ✅ COMPLETE |
| 3 | HIGH | 行为变更 | 更新调用章节：Task 工具 → Agent 工具 (v2.1.63 重命名) | ✅ COMPLETE (已更新标题、代码示例，并添加重命名说明) |
| 4 | HIGH | 示例更新 | 更新完整示例：`Task(monitor, rollback)` → `Agent(monitor, rollback)` | ✅ COMPLETE |
| 5 | HIGH | 内置 Agent | 将 `Bash` Agent 添加到官方 Claude Agent 表格 (model: inherit，用途：在独立上下文中执行终端命令) | ✅ COMPLETE (已添加到表格) |
| 6 | HIGH | Agent 表格 | 将 `workflow-concepts-agent` 添加到本仓库 Agent 表格 (model: opus, color: green) | ✅ COMPLETE |
| 7 | HIGH | Agent 表格 | 将 `workflow-claude-settings-agent` 添加到本仓库 Agent 表格 (model: opus, color: yellow) | ✅ COMPLETE |
| 8 | MED | 内置 Agent | 修复 `statusline-setup` 的 model：`inherit` → `Sonnet` | ✅ COMPLETE |
| 9 | MED | 内置 Agent | 修复 `claude-code-guide` 的 model：`inherit` → `Haiku` | ❌ NOT APPLICABLE (已从表格中移除) |
| 10 | MED | Agent 表格 | 修复 `weather-agent` 的 color：`teal` → `green` | ✅ COMPLETE |
| 11 | MED | 调用方式 | 将 `--agent <name>` CLI 标志添加到调用方式表格 | ✅ COMPLETE (已作为调用方式表格的第一行添加) |
| 12 | MED | 行为变更 | 更新第 147 行文本：官方 Claude Agent 表格标题中的 "Task tool" → "Agent tool" | ✅ COMPLETE (用户已重写标题文本) |
| 13 | MED | 跨文件 | 更新 CLAUDE.md：`Task(...)` → `Agent(...)` 引用 (第 50-53、61 行) | ✅ COMPLETE (已更新编排章节和 tools 字段描述) |

---

## [2026-03-12 12:17 PM PKT] Claude Code v2.1.74

未检测到偏差 — 报告与官方文档完全同步。全部 13 个前置元数据字段和 6 个内置 Agent 均匹配。

---

## [2026-03-13 04:21 PM PKT] Claude Code v2.1.74

未检测到偏差 — 报告与官方文档完全同步。全部 13 个前置元数据字段和 6 个内置 Agent 均匹配。

---

## [2026-03-15 12:50 PM PKT] Claude Code v2.1.76

未检测到偏差 — 报告与官方文档完全同步。全部 13 个前置元数据字段和 6 个内置 Agent 均匹配。

---

## [2026-03-17 12:42 PM PKT] Claude Code v2.1.77

未检测到偏差 — 报告与官方文档完全同步。全部 13 个前置元数据字段和 6 个内置 Agent 均匹配。

---

## [2026-03-18 11:41 PM PKT] Claude Code v2.1.78

未检测到偏差 — 报告与官方文档完全同步。全部 13 个前置元数据字段和 6 个内置 Agent 均匹配。

---

## [2026-03-19 11:56 AM PKT] Claude Code v2.1.79

未检测到偏差 — 报告与官方文档完全同步。全部 13 个前置元数据字段和 6 个内置 Agent 均匹配。

---

## [2026-03-20 08:35 AM PKT] Claude Code v2.1.80

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新字段 | 将 `effort` 字段添加到前置元数据字段表 (string, optional — 努力程度覆盖：`low`, `medium`, `high`, `max`) | ✅ COMPLETE (已添加在 `background` 和 `isolation` 之间，计数更新 14→15) |

---

## [2026-03-21 09:07 PM PKT] Claude Code v2.1.81

未检测到偏差 — 报告与官方文档完全同步。全部 15 个前置元数据字段和 6 个内置 Agent 均匹配。

---

## [2026-03-23 09:49 PM PKT] Claude Code v2.1.81

未检测到偏差 — 报告与官方文档完全同步。全部 15 个前置元数据字段 (14 个官方 + 1 个非官方 `color`) 和 6 个内置 Agent 均匹配。

---

## [2026-03-25 08:07 PM PKT] Claude Code v2.1.83

未检测到偏差 — 报告与官方文档完全同步。全部 15 个前置元数据字段 (14 个官方 + 1 个非官方 `color`) 和 6 个内置 Agent 均匹配。

**关注事项：** `initialPrompt` 已在 v2.1.83 变更日志中添加，但尚未出现在官方文档的支持前置元数据字段表中。当其出现时，报告需要更新。

---

## [2026-03-26 01:01 PM PKT] Claude Code v2.1.84

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新字段 | 将 `initialPrompt` 添加到前置元数据字段表 (string, optional — 当 Agent 通过 `--agent` 或 `agent` 设置作为主会话 Agent 运行时，自动作为第一个用户轮次提交) | ✅ COMPLETE (已添加在 `isolation` 和 `color` 之间，计数更新 15→16) |

---

## [2026-03-27 06:28 PM PKT] Claude Code v2.1.85

未检测到偏差 — 报告与官方文档完全同步。全部 16 个前置元数据字段 (15 个官方 + 1 个非官方 `color`) 和 6 个内置 Agent 均匹配。

---

## [2026-03-28 06:00 PM PKT] Claude Code v2.1.86

未检测到偏差 — 报告与官方文档完全同步。全部 16 个前置元数据字段 (15 个官方 + 1 个非官方 `color`) 和 6 个内置 Agent 均匹配。

---

## [2026-04-01 12:26 PM PKT] Claude Code v2.1.89

未检测到偏差 — 报告与官方文档完全同步。全部 16 个前置元数据字段 (15 个官方 + 1 个非官方 `color`) 和 6 个内置 Agent 均匹配。

---

## [2026-04-02 09:11 PM PKT] Claude Code v2.1.90

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 移除 Agent | 从官方 Claude Agent 表格中移除 `Bash` — 官方文档列出 5 个内置 Agent，`Bash` 不在其中 | ✅ COMPLETE (已移除 Bash 行，重新编号 6→5 个 Agent) |
| 2 | LOW | 字段文档 | 更新 `color` 字段描述 — 移除"未出现在官方前置元数据表中"的备注；`color` 现已出现在官方支持的前置元数据字段表中 | ✅ COMPLETE (已从 color 字段描述中移除非官方备注) |

---

## [2026-04-03 08:30 PM PKT] Claude Code v2.1.91

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | LOW | 字段文档 | 更新 `permissionMode` 字段描述 — 添加 `auto` 作为有效值 (官方文档现列出：`default`, `acceptEdits`, `auto`, `dontAsk`, `bypassPermissions`, `plan`) | ✅ COMPLETE (已在 permissionMode 描述中将 `auto` 添加到 `acceptEdits` 和 `dontAsk` 之间) |

---

## [2026-04-04 10:43 PM PKT] Claude Code v2.1.92

未检测到偏差 — 报告与官方文档完全同步。全部 16 个前置元数据字段和 5 个内置 Agent 均匹配。

---

## [2026-04-08 09:34 PM PKT] Claude Code v2.1.96

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | LOW | 字段文档 | 更新 `model` 字段描述 — 在别名之外添加完整模型 ID 支持 (例如 `claude-opus-4-6`) | ✅ COMPLETE (已更新描述以匹配官方文档措辞) |
| 2 | LOW | 字段文档 | 更新 `effort` 字段描述 — 添加 `max (仅限 Opus 4.6)` 限定说明 | ✅ COMPLETE (已在 max 选项中添加仅限 Opus 4.6 的备注) |
| 3 | LOW | 字段文档 | 更新 `color` 字段描述 — 将 `(例如 green, magenta)` 替换为明确的有效值：`red`, `blue`, `green`, `yellow`, `purple`, `orange`, `pink`, `cyan` | ✅ COMPLETE (已将基于示例的描述替换为完整的有效值列表) |

---

## [2026-04-09 11:34 PM PKT] Claude Code v2.1.97

未检测到偏差 — 报告与官方文档完全同步。全部 16 个前置元数据字段和 5 个内置 Agent 均匹配。

---

## [2026-04-11 06:10 PM PKT] Claude Code v2.1.101

未检测到偏差 — 报告与官方文档完全同步。全部 16 个前置元数据字段和 5 个内置 Agent 均匹配。

---

## [2026-04-13 08:02 PM PKT] Claude Code v2.1.101

未检测到偏差 — 报告与官方文档完全同步。全部 16 个前置元数据字段和 5 个内置 Agent 均匹配。

---

## [2026-04-14 11:14 PM PKT] Claude Code v2.1.107

未检测到偏差 — 报告与官方文档完全同步。全部 16 个前置元数据字段和 5 个内置 Agent 均匹配。

---

## [2026-04-16 08:16 PM PKT] Claude Code v2.1.110

未检测到偏差 — 报告与官方文档完全同步。全部 16 个前置元数据字段和 5 个内置 Agent 均匹配。
