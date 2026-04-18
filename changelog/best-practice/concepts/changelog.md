# 变更日志 — README CONCEPTS 部分

跟踪 README CONCEPTS 表格与 Claude Code 官方文档之间的偏差。

## 状态图例

| 状态 | 含义 |
|--------|---------|
| ✅ `COMPLETE (原因)` | 操作已执行并成功解决 |
| ❌ `INVALID (原因)` | 发现不正确、不适用或系有意为之 |
| ✋ `ON HOLD (原因)` | 操作已推迟 — 等待外部依赖或用户决定 |

---

## [2026-03-02 11:14 AM PKT] Claude Code v2.1.63

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 失效 URL | 将 Permissions URL 从 `/iam` 修复为 `/permissions` | ✅ COMPLETE (URL 已更新为 /permissions) |
| 2 | HIGH | 缺失概念 | 在 CONCEPTS 表格中添加 Agent Teams 行 | ✅ COMPLETE (已添加行，位置为 ~\/\.claude\/teams\/) |
| 3 | HIGH | 缺失概念 | 在 CONCEPTS 表格中添加 Keybindings 行 | ✅ COMPLETE (已添加行，位置为 ~\/\.claude\/keybindings\.json) |
| 4 | HIGH | 缺失概念 | 在 CONCEPTS 表格中添加 Model Configuration 行 | ✅ COMPLETE (已添加行，位置为 \.claude\/settings\.json) |
| 5 | HIGH | 缺失概念 | 在 CONCEPTS 表格中添加 Auto Memory 行 | ✅ COMPLETE (已添加行，位置为 ~\/\.claude\/projects\/<project>\/memory\/) |
| 6 | HIGH | 过时锚点 | 将 Rules URL 锚点从 `#modular-rules-with-clauderules` 修复为 `#organize-rules-with-clauderules` | ✅ COMPLETE (锚点已更新) |
| 7 | MED | 缺失概念 | 在 CONCEPTS 表格中添加 Checkpointing 行 | ✅ COMPLETE (已添加行，位置为自动 git-based) |
| 8 | MED | 缺失概念 | 在 CONCEPTS 表格中添加 Status Line 行 | ✅ COMPLETE (已添加行，位置为 ~\/\.claude\/settings\.json) |
| 9 | MED | 缺失概念 | 在 CONCEPTS 表格中添加 Remote Control 行 | ✅ COMPLETE (已添加行，位置为 CLI \/ claude\.ai) |
| 10 | MED | 缺失概念 | 在 CONCEPTS 表格中添加 Fast Mode 行 | ✅ COMPLETE (已添加行，位置为 \.claude\/settings\.json) |
| 11 | MED | 缺失概念 | 在 CONCEPTS 表格中添加 Headless Mode 行 | ✅ COMPLETE (已添加行，位置为 CLI flag -p) |
| 12 | LOW | 描述变更 | 更新 Memory 描述以提及 auto memory | ✅ COMPLETE (描述和位置已更新) |
| 13 | LOW | 位置变更 | 更新 MCP Servers 位置以包含 `.mcp.json` | ✅ COMPLETE (位置已更新以包含 .mcp.json) |
| 14 | LOW | 缺失徽章 | 为 Hooks 行添加 Implemented 徽章 | ✅ COMPLETE (已添加 Implemented 徽章，链接到 .claude/hooks/) |

---

## [2026-03-02 11:57 AM PKT] Claude Code v2.1.63

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 表格整合 | 将 CONCEPTS 表格从 22 行整合为 10 行 — 将相关概念折叠为内联文档链接 | ✅ COMPLETE (22 → 10 行) |
| 2 | MED | 合并概念 | 将 Marketplaces 折叠到 Plugins 行作为内联链接 | ✅ COMPLETE (已链接到 /discover-plugins) |
| 3 | MED | 合并概念 | 将 Agent Teams 折叠到 Sub-Agents 行作为内联链接 | ✅ COMPLETE (已链接到 /agent-teams) |
| 4 | MED | 合并概念 | 将 Permissions、Model Config、Output Styles、Sandboxing、Keybindings、Status Line、Fast Mode 折叠到 Settings 行作为内联链接 | ✅ COMPLETE (7 个概念已折叠并附带文档链接) |
| 5 | MED | 合并概念 | 将 Auto Memory 和 Rules 折叠到 Memory 行作为内联链接 | ✅ COMPLETE (已链接到 /memory 和 /memory#organize-rules-with-clauderules) |
| 6 | MED | 合并概念 | 将 Headless Mode 折叠到 Remote Control 行作为内联链接 | ✅ COMPLETE (已链接到 /headless) |
| 7 | LOW | 重新排序 | 按逻辑分组重排表格：构建块 → 扩展 → 配置 → 上下文 → 运行时 | ✅ COMPLETE (已按关注点分组，而非按时间顺序) |

---

## [2026-03-07 08:40 AM PKT] Claude Code v2.1.71

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 失效 URL | 修复 TIPS 中的 `context-management` → `interactive-mode`（第 112、115、135 行） | ✅ COMPLETE (3 处已替换为 interactive-mode) |
| 2 | HIGH | 失效 URL | 修复 TIPS 中的 `model-configuration` → `model-config`（第 115、116、135 行） | ✅ COMPLETE (3 处已替换为 model-config) |
| 3 | HIGH | 失效 URL | 修复 TIPS 中的 `usage-billing` → `costs`（第 115 行） | ✅ COMPLETE (已替换为 costs) |
| 4 | HIGH | 失效 URL | 移除 STARTUPS 中的 `cowork` URL（第 167 行）— 页面不存在 | ✅ COMPLETE (超链接已移除，纯文本保留) |
| 5 | HIGH | 缺失概念 | 在 CONCEPTS 和 Hot 部分添加 Scheduled Tasks 行（`/loop`、cron 工具） | ✅ COMPLETE (由用户添加到两个表格 + /loop 提示 + Boris 推文) |
| 6 | MED | 位置变更 | 将 Agent Teams 位置从 `.claude/agents/<name>.md` 更新为 `built-in (env var)` | ✅ COMPLETE (位置已更新为 built-in env var) |

---

## [2026-03-10 01:18 PM PKT] Claude Code v2.1.72

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 失效 URL | 将 CONCEPTS 表格（第 24 行）中的 Commands URL 从 `/slash-commands` 修复为 `/skills` — `/slash-commands` 提供 Skills 页面内容；文档说"commands 已合并到 skills" | ❌ INVALID (URL 仍可访问；用户选择保留原样) |
| 2 | HIGH | 失效 URL | 将 TIPS 部分（第 108 行）中的 Commands URL 从 `/slash-commands` 修复为 `/skills` — 同一过时 URL | ❌ INVALID (URL 仍可访问；用户选择保留原样) |
| 3 | MED | 缺失内联链接 | 为 CLI Startup Flags 行添加 Interactive Mode (`/interactive-mode`) 内联链接 — 涵盖 /compact、/clear、/context、/extra-usage | ✅ COMPLETE (已为 CLI Startup Flags 描述添加内联链接) |
| 4 | MED | 缺失内联链接 | 为 Settings 行添加 Costs (`/costs`) 内联链接 — 涵盖 /usage、billing、pay-as-you-go | ❌ INVALID (用户选择跳过) |
| 5 | LOW | 缺失概念 | 考虑添加 IDE Integrations 行（VS Code、JetBrains、Desktop App、Web）或作为 Best Practices 的内联链接 | ❌ INVALID (用户选择跳过 — 属于平台界面，非配置概念) |
| 6 | HIGH | 缺失概念 | 在 Hot 表格中添加 Code Review 行 — 多 Agent PR 分析（研究预览，Teams 和 Enterprise） | ✅ COMPLETE (已作为第一个 Hot 条目添加，附带博客链接和最佳实践推文) |
| 7 | MED | 新徽章 | 创建 `!/tags/beta.svg` 标签（黄色，38x20px）并添加到 Hot 表格中的 Code Review 和 Agent Teams | ✅ COMPLETE (beta.svg 已创建；已添加到 Code Review 和 Agent Teams 行) |
| 8 | MED | 重新排序 | 按发布日期排序 Hot 表格（最新在前）：Code Review → Scheduled Tasks → Voice Mode → Agent Teams → Remote Control → Git Worktrees → Ralph Wiggum | ✅ COMPLETE (Voice Mode 和 Agent Teams 已交换以匹配时间顺序) |

---

## [2026-03-12 12:22 PM PKT] Claude Code v2.1.74

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 失效 URL | 将 CONCEPTS 表格（第 24 行）中的 Commands URL 从 `/slash-commands` 修复为 `/skills` — `/slash-commands` 重定向到 `/skills` 页面 | ❌ INVALID (2026-03-10 的重复项；URL 仍可访问；用户选择保留原样) |
| 2 | LOW | 验证 | 所有外部文档 URL 已验证 — 未发现失效链接 | ✅ COMPLETE (所有 20+ 个 URL 返回有效页面) |
| 3 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件 | ✅ COMPLETE (所有徽章目标均存在于文件系统中) |
| 4 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在目标页面确认 | ✅ COMPLETE (/memory 页面上存在该标题) |
| 5 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 | ✅ COMPLETE (未检测到描述偏差) |

---

## [2026-03-15 12:48 PM PKT] Claude Code v2.1.76

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 过时 URL | Commands URL `/slash-commands` 提供 Skills 页面 — 文档说"commands 已合并到 skills" | ❌ INVALID (2026-03-10 的重复项；URL 仍可访问；用户选择保留原样) |
| 2 | MED | 缺失徽章 | Remote Control (Hot) 没有徽章 — 唯一没有任何 BP 或 Impl 徽章的 Hot 条目 | ✅ COMPLETE (已添加 BP 徽章，链接到官方文档页面) |
| 3 | LOW | 命名 | README 中使用 "Sub-Agents" 而官方文档使用 "subagents"（一个词）— 外观不一致 | ✅ COMPLETE (已在 CONCEPTS 表格中重命名为 "Subagents") |
| 4 | LOW | 验证 | 所有 27 个外部文档 URL 已验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面) |
| 5 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件 | ✅ COMPLETE (所有徽章目标均存在于文件系统中) |
| 6 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落存在) |
| 7 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有 13 个 CONCEPTS + 9 个 Hot 行的描述均准确) |

---

## [2026-03-17 12:46 PM PKT] Claude Code v2.1.77

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 过时 URL | Commands URL `/slash-commands` 提供 Skills 页面 — 文档说"commands 已合并到 skills" | ❌ INVALID (2026-03-10 的重复项；URL 仍可访问；用户选择保留原样) |
| 2 | HIGH | 描述变更 | Hooks 描述说"确定性脚本"但 Hooks 现在包含 4 种类型：command、HTTP、prompt 和 agent — 只有 command hooks 是确定性的 | ✅ COMPLETE (已在 CONCEPTS 表格中更新为"用户定义的处理器（脚本、HTTP、提示词、Agent）") |
| 3 | MED | 缺失概念 | Desktop App 在 `/desktop` 有专门文档页面 — 未在 CONCEPTS 或 Hot 表格中 | ❌ INVALID (用户选择跳过 — Desktop 属于平台界面，非配置概念) |
| 4 | MED | URL 变更 | Hooks 文档现在分为指南 (`/hooks-guide`) 和参考 (`/hooks`) — CONCEPTS 仅链接到参考 | ✅ COMPLETE (已在 Hooks 行描述中添加指南链接作为内联链接) |
| 5 | LOW | 验证 | 所有 28 个外部文档 URL 已验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面，包括 /slash-commands 重定向) |
| 6 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件 | ✅ COMPLETE (所有 20 个徽章目标均存在于文件系统中) |
| 7 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落存在) |
| 8 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 | ✅ COMPLETE (检测到 Hooks 描述偏差 — 见 #2) |

---

## [2026-03-18 11:43 PM PKT] Claude Code v2.1.78

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 过时 URL | Commands URL `/slash-commands` 提供 Skills 页面 — 文档说"commands 已合并到 skills" | ❌ INVALID (2026-03-10 的重复项；URL 仍可访问；用户选择保留原样) |
| 2 | HIGH | URL+名称变更 | Hot 表格中的 Voice Mode 链接到推文而非官方文档 `/voice-dictation`；官方名称为 "Voice Dictation" | ✅ COMPLETE (已重命名为 "Voice Dictation"，链接到 /voice-dictation，描述已更新；BP 徽章保留链接到推文；同时更新了 STARTUPS 表格) |
| 3 | LOW | 验证 | 所有 29 个外部文档 URL 已验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面，包括 /slash-commands 重定向) |
| 4 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件 | ✅ COMPLETE (所有 20+ 个徽章目标均存在于文件系统中) |
| 5 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落存在) |
| 6 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有描述准确) |

---

## [2026-03-19 11:59 AM PKT] Claude Code v2.1.79

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 过时 URL | Commands URL `/slash-commands` 提供 Skills 页面 — 文档说"commands 已合并到 skills" | ❌ INVALID (2026-03-10 的重复项；URL 仍可访问；用户选择保留原样) |
| 2 | LOW | 验证 | 所有 30 个外部文档 URL 已验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面，包括 /slash-commands 重定向) |
| 3 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件 | ✅ COMPLETE (所有 20+ 个徽章目标均存在于文件系统中) |
| 4 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落存在) |
| 5 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有描述准确) |

---

## [2026-03-20 08:38 AM PKT] Claude Code v2.1.80

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 缺失概念 | 在 Hot 表格中添加 Channels 行 — 从 Telegram/Discord/webhooks 推送事件到运行中的会话（研究预览，v2.1.80） | ✅ COMPLETE (已作为第一个 Hot 条目添加，附带 beta 徽章和 Reference 链接) |
| 2 | HIGH | 过时 URL | Commands URL `/slash-commands` 提供 Skills 页面 — 文档说"commands 已合并到 skills" | ❌ INVALID (2026-03-10 的重复项；URL 仍可访问；用户选择保留原样) |
| 3 | MED | 缺失深层链接 | Git Worktrees URL 应锚定到 `#run-parallel-claude-code-sessions-with-git-worktrees` | ✅ COMPLETE (已为 Hot 表格中的 Git Worktrees URL 添加锚点) |
| 4 | LOW | 缺失内联链接 | Plugins 行可添加 `[Marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)` 子链接 | ✅ COMPLETE (已为 Plugins 行创建 Marketplaces 内联链接) |
| 5 | LOW | 验证 | 所有 31 个外部文档 URL 已验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面，包括 /slash-commands 重定向) |
| 6 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件 | ✅ COMPLETE (所有 20+ 个徽章目标均存在于文件系统中) |
| 7 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落存在) |
| 8 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有描述准确) |

---

## [2026-03-21 09:12 PM PKT] Claude Code v2.1.81

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 过时 URL | Commands URL `/slash-commands` 提供 Skills 页面 — 文档说"commands 已合并到 skills" | ❌ INVALID (2026-03-10 的重复项；URL 仍可访问；用户选择保留原样) |
| 2 | LOW | 验证 | 所有 32 个外部文档 URL 已验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面，包括 /slash-commands 重定向) |
| 3 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件 | ✅ COMPLETE (所有 20+ 个徽章目标均存在于文件系统中) |
| 4 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落存在) |
| 5 | LOW | 验证 | Git Worktrees 锚点 `#run-parallel-claude-code-sessions-with-git-worktrees` 已在 /common-workflows 页面确认 | ✅ COMPLETE (标题段落存在) |
| 6 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有描述准确) |

---

## [2026-03-23 09:53 PM PKT] Claude Code v2.1.81

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 过时 URL | Commands URL `/slash-commands` 提供 Skills 页面 — 文档说"commands 已合并到 skills" | ❌ INVALID (2026-03-10 的重复项；URL 仍可访问；用户选择保留原样) |
| 2 | LOW | 验证 | 所有 33 个外部文档 URL 已验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面，包括 /slash-commands 重定向) |
| 3 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件 | ✅ COMPLETE (所有 20+ 个徽章目标均存在于文件系统中) |
| 4 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落存在) |
| 5 | LOW | 验证 | Git Worktrees 锚点 `#run-parallel-claude-code-sessions-with-git-worktrees` 已在 /common-workflows 页面确认 | ✅ COMPLETE (标题段落存在) |
| 6 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有描述准确) |

---

## [2026-03-25 08:12 PM PKT] Claude Code v2.1.83

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 过时 URL | Commands URL `/slash-commands` 提供 Skills 页面 — 文档说"commands 已合并到 skills" | ❌ INVALID (2026-03-10 的重复项；URL 仍可访问；用户选择保留原样) |
| 2 | MED | URL 变更 | Simplify & Batch 的主链接指向推文而非官方文档 `/skills#bundled-skills` — 现已是官方 bundled skills | ✅ COMPLETE (主链接已更新为 /skills#bundled-skills；BP 徽章保留链接到 Boris 的推文) |
| 3 | LOW | 验证 | 所有 34 个外部文档 URL 已验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面，包括 /slash-commands 重定向) |
| 4 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件 | ✅ COMPLETE (所有 20+ 个徽章目标均存在于文件系统中) |
| 5 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落存在) |
| 6 | LOW | 验证 | Git Worktrees 锚点 `#run-parallel-claude-code-sessions-with-git-worktrees` 已在 /common-workflows 页面确认 | ✅ COMPLETE (标题段落存在) |
| 7 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有描述准确) |
| 8 | HIGH | 缺失概念 | 在 Hot 表格中添加 Auto Mode 行 — 后台安全分类器取代权限提示（研究预览，Team/Enterprise） | ✅ COMPLETE (已作为第一个 Hot 条目添加，附带 beta 徽章、链接到 @claudeai 推文的 BP 徽章和博客链接) |

---

## [2026-03-26 01:05 PM PKT] Claude Code v2.1.84

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 过时 URL | Commands URL `/slash-commands` 提供 Skills 页面 — 文档说"commands 已合并到 skills" | ❌ INVALID (2026-03-10 的重复项；URL 仍可访问；用户选择保留原样) |
| 2 | MED | 缺失概念 | 在 Hot 表格中添加 Slack 集成 — 在 Slack 中 @Claude 将编码任务路由到 Claude Code Web 会话 | ✅ COMPLETE (已在 Channels 之后添加行，位置为 @Claude，描述为 Web 会话) |
| 3 | MED | 缺失概念 | 在 Hot 表格中添加 GitHub Actions / CI-CD — 在 CI/CD 流水线中自动化 PR 审查、issue 分类和代码生成 | ✅ COMPLETE (已在 Code Review 之后添加行，位置为 .github/workflows/，附带 GitLab CI/CD 内联链接) |
| 4 | LOW | 验证 | 所有 35 个外部文档 URL 已验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面，包括 /slash-commands 重定向) |
| 5 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件 | ✅ COMPLETE (所有 20+ 个徽章目标均存在于文件系统中) |
| 6 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落存在) |
| 7 | LOW | 验证 | Git Worktrees 锚点 `#run-parallel-claude-code-sessions-with-git-worktrees` 已在 /common-workflows 页面确认 | ✅ COMPLETE (标题段落存在) |
| 8 | LOW | 验证 | Auto Mode 锚点 `#eliminate-prompts-with-auto-mode` 已在 /permission-modes 页面确认 | ✅ COMPLETE (标题段落存在) |
| 9 | LOW | 验证 | Bundled Skills 锚点 `#bundled-skills` 已在 /skills 页面确认 | ✅ COMPLETE (标题段落存在) |
| 10 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有描述准确) |

---

## [2026-03-27 06:37 PM PKT] Claude Code v2.1.85

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 过时 URL | Commands URL `/slash-commands` 提供 Skills 页面 — 文档说"commands 已合并到 skills" | ❌ INVALID (2026-03-10 的重复项；URL 仍可访问；用户选择保留原样) |
| 2 | MED | 缺失概念 | 在 Hot 表格中添加 Chrome 集成 — 通过 Claude in Chrome 扩展进行浏览器自动化（beta，专用文档位于 `/chrome`） | ✅ COMPLETE (已在 GitHub Actions 之后添加行，位置为 --chrome，附带 beta 徽章) |
| 3 | LOW | 验证 | 所有 36 个外部文档 URL 已验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面，包括 /slash-commands 重定向) |
| 4 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件 | ✅ COMPLETE (所有 20+ 个徽章目标均存在于文件系统中) |
| 5 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落存在) |
| 6 | LOW | 验证 | Git Worktrees 锚点 `#run-parallel-claude-code-sessions-with-git-worktrees` 已在 /common-workflows 页面确认 | ✅ COMPLETE (标题段落存在) |
| 7 | LOW | 验证 | Auto Mode 锚点 `#eliminate-prompts-with-auto-mode` 已在 /permission-modes 页面确认 | ✅ COMPLETE (标题段落存在) |
| 8 | LOW | 验证 | Bundled Skills 锚点 `#bundled-skills` 已在 /skills 页面确认 | ✅ COMPLETE (标题段落存在) |
| 9 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有描述准确) |

---

## [2026-03-28 06:04 PM PKT] Claude Code v2.1.86

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 过时 URL | Commands URL `/slash-commands` 提供 Skills 页面 — 文档说"commands 已合并到 skills" | ❌ INVALID (2026-03-10 的重复项；URL 仍可访问；用户选择保留原样) |
| 2 | MED | 缺失徽章 | Hot 表格中的 Chrome 行没有 BP 徽章 — 报告存在于 `reports/claude-in-chrome-v-chrome-devtools-mcp.md` | ✅ COMPLETE (已添加 BP 徽章，链接到 reports/claude-in-chrome-v-chrome-devtools-mcp.md) |
| 3 | LOW | 描述变更 | Plugins 描述缺少 LSP 服务器 — 官方文档将 `.lsp.json` 列为插件组件 | ✅ COMPLETE (已在 Plugins 描述中添加 "and LSP servers") |
| 4 | LOW | 验证 | 所有 37 个外部文档 URL 已验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面，包括 /slash-commands 重定向) |
| 5 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件 | ✅ COMPLETE (所有 20+ 个徽章目标均存在于文件系统中) |
| 6 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落 `.claude/rules/` 存在) |
| 7 | LOW | 验证 | Git Worktrees 锚点 `#run-parallel-claude-code-sessions-with-git-worktrees` 已在 /common-workflows 页面确认 | ✅ COMPLETE (标题段落存在) |
| 8 | LOW | 验证 | Auto Mode 锚点 `#eliminate-prompts-with-auto-mode` 已在 /permission-modes 页面确认 | ✅ COMPLETE (标题段落存在) |
| 9 | LOW | 验证 | Bundled Skills 锚点 `#bundled-skills` 已在 /skills 页面确认 | ✅ COMPLETE (标题段落存在) |
| 10 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有描述准确，Plugins LSP 备注除外 — 见 #3) |

---

## [2026-04-01 12:33 PM PKT] Claude Code v2.1.89

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 缺失概念 | 在 Hot 表格中添加 Computer Use 行 — 通过内置 MCP 服务器在 macOS 上进行屏幕控制（研究预览，v2.1.85+） | ✅ COMPLETE (已在 Fullscreen Rendering 之后添加行，附带 beta 徽章和 Desktop 内联链接) |
| 2 | HIGH | 过时 URL | Commands URL `/slash-commands` 提供 Skills 页面 — 文档说"commands 已合并到 skills" | ❌ INVALID (2026-03-10 的重复项；URL 仍可访问；用户选择保留原样) |
| 3 | MED | 缺失概念 | 在 Hot 表格中添加 Fullscreen Rendering 行 — 无闪烁全屏渲染，支持鼠标操作（研究预览，v2.1.88+） | ✅ COMPLETE (已作为第一个 Hot 条目添加，位置为 CLAUDE_CODE_NO_FLICKER=1) |
| 4 | LOW | 验证 | 所有 38 个外部文档 URL 已验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面，包括 /slash-commands 重定向) |
| 5 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件 | ✅ COMPLETE (所有 20+ 个徽章目标均存在于文件系统中) |
| 6 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落存在) |
| 7 | LOW | 验证 | Git Worktrees 锚点 `#run-parallel-claude-code-sessions-with-git-worktrees` 已在 /common-workflows 页面确认 | ✅ COMPLETE (标题段落存在) |
| 8 | LOW | 验证 | Auto Mode 锚点 `#eliminate-prompts-with-auto-mode` 已在 /permission-modes 页面确认 | ✅ COMPLETE (标题段落存在) |
| 9 | LOW | 验证 | Bundled Skills 锚点 `#bundled-skills` 已在 /skills 页面确认 | ✅ COMPLETE (标题段落存在) |
| 10 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有描述准确) |

---

## [2026-04-02 09:17 PM PKT] Claude Code v2.1.90

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 过时 URL | Commands URL `/slash-commands` 提供 Skills 页面 — 文档说"commands 已合并到 skills" | ❌ INVALID (2026-03-10 的重复项；URL 仍可访问；用户选择保留原样) |
| 2 | LOW | 验证 | 所有 39 个外部文档 URL 已验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面，包括 /slash-commands 重定向) |
| 3 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件 | ✅ COMPLETE (所有 20+ 个徽章目标均存在于文件系统中) |
| 4 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落 "Organize rules with `.claude/rules/`" 存在) |
| 5 | LOW | 验证 | Git Worktrees 锚点 `#run-parallel-claude-code-sessions-with-git-worktrees` 已在 /common-workflows 页面确认 | ✅ COMPLETE (标题段落存在) |
| 6 | LOW | 验证 | Auto Mode 锚点 `#eliminate-prompts-with-auto-mode` 已在 /permission-modes 页面确认 | ✅ COMPLETE (标题段落存在) |
| 7 | LOW | 验证 | Bundled Skills 锚点 `#bundled-skills` 已在 /skills 页面确认 | ✅ COMPLETE (标题段落存在) |
| 8 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有描述准确) |

---

## [2026-04-03 08:35 PM PKT] Claude Code v2.1.91

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 过时 URL | Commands URL `/slash-commands` 不在官方站点地图 (llms.txt) 中 — 重定向到 `/skills` 页面；文档说"commands 已合并到 skills" | ❌ INVALID (2026-03-10 的重复项；URL 通过重定向仍可访问；用户选择保留原样) |
| 2 | LOW | 验证 | 所有 40 个外部文档 URL 已根据 llms.txt 站点地图（80 个页面）验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面，包括 /slash-commands 重定向) |
| 3 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件（已检查 17 个本地目标） | ✅ COMPLETE (所有徽章目标均存在于文件系统中) |
| 4 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落 "Organize rules with `.claude/rules/`" 存在) |
| 5 | LOW | 验证 | Git Worktrees 锚点 `#run-parallel-claude-code-sessions-with-git-worktrees` 已在 /common-workflows 页面确认 | ✅ COMPLETE (标题段落存在) |
| 6 | LOW | 验证 | Auto Mode 锚点 `#eliminate-prompts-with-auto-mode` 已在 /permission-modes 页面确认 | ✅ COMPLETE (标题段落存在) |
| 7 | LOW | 验证 | Bundled Skills 锚点 `#bundled-skills` 已在 /skills 页面确认 | ✅ COMPLETE (标题段落存在) |
| 8 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有描述准确) |

---

## [2026-04-04 10:46 PM PKT] Claude Code v2.1.92

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 缺失概念 | 在 Hot 表格中添加 Ultraplan 行 — 基于云的计划起草，支持浏览器审查、行内评论和灵活执行（`/ultraplan`） | ✅ COMPLETE (已在 Power-ups 之后添加行，附带 beta 徽章，位置为 /ultraplan) |
| 2 | HIGH | 缺失概念 | 在 Hot 表格中添加 Claude Code Web 行 — 在 claude.ai/code 的云基础设施上运行任务，支持 PR 自动修复和并行会话 | ✅ COMPLETE (已在 Ultraplan 之后添加行，附带 beta 徽章，位置为 claude.ai/code，附带 Web Scheduled Tasks 内联链接) |
| 3 | HIGH | 过时 URL | Commands URL `/slash-commands` 不在官方站点地图中 — 重定向到 `/skills` 页面；文档说"commands 已合并到 skills" | ❌ INVALID (2026-03-10 的重复项；URL 通过重定向仍可访问；用户选择保留原样) |
| 4 | MED | 缺失概念 | 在 Hot 表格中添加 Desktop App 行 — 独立应用，支持可视化 diff、Dispatch、computer use 和并行会话 | ❌ INVALID (2026-03-17 的重复项；用户认为属于平台界面，非配置概念) |

---

## [2026-04-08 09:37 PM PKT] Claude Code v2.1.96

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 过时 URL | Commands URL `/slash-commands` 不在官方站点地图中 — 重定向到 `/skills` 页面；文档说"commands 已合并到 skills" | ❌ INVALID (2026-03-10 的重复项；URL 通过重定向仍可访问；用户选择保留原样) |
| 2 | MED | 名称变更 | Hot 表格中的 "No Flicker Mode" — 官方文档页面标题为 "Fullscreen rendering"；考虑重命名或添加副标题 | ❌ INVALID (用户选择保留 "No Flicker Mode"，遵循 Boris 推文的命名惯例；环境变量为 `CLAUDE_CODE_NO_FLICKER`) |
| 3 | MED | 缺失概念 | 在 Hot 表格中添加 Desktop App 行 — 独立应用，支持可视化 diff、Dispatch、computer use 和并行会话 | ❌ INVALID (2026-03-17 的重复项；用户认为属于平台界面，非配置概念) |
| 4 | LOW | 验证 | 所有 41 个外部文档 URL 已验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面，包括 /slash-commands 重定向) |
| 5 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件 | ✅ COMPLETE (所有 20+ 个徽章目标均存在于文件系统中) |
| 6 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落 "Organize rules with `.claude/rules/`" 存在) |
| 7 | LOW | 验证 | Git Worktrees 锚点 `#run-parallel-claude-code-sessions-with-git-worktrees` 已在 /common-workflows 页面确认 | ✅ COMPLETE (标题段落存在) |
| 8 | LOW | 验证 | Auto Mode 锚点 `#eliminate-prompts-with-auto-mode` 已在 /permission-modes 页面确认 | ✅ COMPLETE (标题段落存在) |
| 9 | LOW | 验证 | Bundled Skills 锚点 `#bundled-skills` 已在 /skills 页面确认 | ✅ COMPLETE (标题段落存在) |
| 10 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有描述准确) |

---

## [2026-04-09 11:37 PM PKT] Claude Code v2.1.97

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 缺失概念 | 在 Hot 表格中添加 Agent SDK 行 — 使用 Python/TypeScript SDK 构建生产级 AI Agent（29 个文档页面，`/en/agent-sdk/overview`） | ✅ COMPLETE (已在 Claude Code Web 之后添加行，附带 Quickstart 和 Examples 内联链接) |
| 2 | HIGH | 过时 URL | Commands URL `/slash-commands` 不在官方站点地图中 — 重定向到 `/skills`；Commands 的规范参考现为 `/en/commands` | ❌ INVALID (2026-03-10 的重复项；URL 通过重定向仍可访问；用户选择保留原样) |
| 3 | MED | 缺失内联链接 | 为 CLI Startup Flags 行添加 Environment Variables (`/env-vars`) 内联链接 — 新的专用文档页面 | ✅ COMPLETE (已在 Interactive Mode 之后添加 Env Vars 内联链接) |
| 4 | LOW | 验证 | 所有 42 个外部文档 URL 已根据 llms.txt 站点地图（110 个页面）验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面，包括 /slash-commands 重定向) |
| 5 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件（已检查 20+ 个徽章目标） | ✅ COMPLETE (所有徽章目标均存在于文件系统中) |
| 6 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落 "Organize rules with `.claude/rules/`" 存在) |
| 7 | LOW | 验证 | Git Worktrees 锚点 `#run-parallel-claude-code-sessions-with-git-worktrees` 已在 /common-workflows 页面确认 | ✅ COMPLETE (标题段落存在) |
| 8 | LOW | 验证 | Auto Mode 锚点 `#eliminate-prompts-with-auto-mode` 已在 /permission-modes 页面确认 | ✅ COMPLETE (标题段落存在) |
| 9 | LOW | 验证 | Bundled Skills 锚点 `#bundled-skills` 已在 /skills 页面确认 | ✅ COMPLETE (标题段落存在) |
| 10 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有描述准确) |

---

## [2026-04-11 06:13 PM PKT] Claude Code v2.1.101

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 过时 URL | Commands URL `/slash-commands` 不在官方站点地图（110 个页面）中 — 重定向到 `/skills`；Commands 的规范参考为 `/en/commands` | ❌ INVALID (2026-03-10 的重复项；URL 通过重定向仍可访问；用户选择保留原样) |
| 2 | LOW | 验证 | 所有 43 个外部文档 URL 已根据 llms.txt 站点地图（110 个页面）验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面，包括 /slash-commands 重定向) |
| 3 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件（已检查 20+ 个徽章目标） | ✅ COMPLETE (所有徽章目标均存在于文件系统中) |
| 4 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落 "Organize rules with `.claude/rules/`" 存在) |
| 5 | LOW | 验证 | Git Worktrees 锚点 `#run-parallel-claude-code-sessions-with-git-worktrees` 已在 /common-workflows 页面确认 | ✅ COMPLETE (标题段落存在) |
| 6 | LOW | 验证 | Auto Mode 锚点 `#eliminate-prompts-with-auto-mode` 已在 /permission-modes 页面确认 | ✅ COMPLETE (标题段落存在) |
| 7 | LOW | 验证 | Bundled Skills 锚点 `#bundled-skills` 已在 /skills 页面确认 | ✅ COMPLETE (标题段落存在) |
| 8 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有描述准确) |

---

## [2026-04-13 08:07 PM PKT] Claude Code v2.1.101

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 过时 URL | Commands URL `/slash-commands` 不在官方站点地图（110 个页面）中 — 重定向到 `/skills`；Commands 的规范参考为 `/en/commands` | ❌ INVALID (2026-03-10 的重复项；URL 通过重定向仍可访问；用户选择保留原样) |
| 2 | LOW | 验证 | 所有 44 个外部文档 URL 已根据 llms.txt 站点地图（110 个页面）验证 — 未发现失效链接 | ✅ COMPLETE (所有 URL 返回有效页面，包括 /slash-commands 重定向) |
| 3 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件（已检查 20+ 个徽章目标） | ✅ COMPLETE (所有徽章目标均存在于文件系统中) |
| 4 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落 "Organize rules with `.claude/rules/`" 存在) |
| 5 | LOW | 验证 | Git Worktrees 锚点 `#run-parallel-claude-code-sessions-with-git-worktrees` 已在 /common-workflows 页面确认 | ✅ COMPLETE (标题段落存在) |
| 6 | LOW | 验证 | Auto Mode 锚点 `#eliminate-prompts-with-auto-mode` 已在 /permission-modes 页面确认 | ✅ COMPLETE (标题段落存在) |
| 7 | LOW | 验证 | Bundled Skills 锚点 `#bundled-skills` 已在 /skills 页面确认 | ✅ COMPLETE (标题段落存在) |
| 8 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有描述准确) |

---

## [2026-04-14 11:17 PM PKT] Claude Code v2.1.107

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 缺失概念 | 在 Hot 表格中添加 Routines 行 — 在 Anthropic 基础设施上的云自动化，支持定时、API 和 GitHub 事件触发器（`/en/routines`） | ✅ COMPLETE (已在 Scheduled Tasks 之后添加行，附带 beta 徽章和 Desktop Tasks 内联链接) |
| 2 | HIGH | 过时 URL | 更新 Claude Code Web 行（第 45 行）中的 `web-scheduled-tasks` 内联链接为 `/en/routines` — URL 不在站点地图中，重定向到 Routines 页面 | ✅ COMPLETE (内联链接文字改为 "Routines"，URL 更新为 /routines) |
| 3 | HIGH | 过时 URL | 更新 Scheduled Tasks 行（第 55 行）中的 `web-scheduled-tasks` 内联链接为 `/en/routines` — 同一过时 URL | ✅ COMPLETE (URL 已更新为 /routines) |
| 4 | HIGH | 过时 URL | Commands URL `/slash-commands` 不在官方站点地图（119 个页面）中 — 重定向到 `/skills`；Commands 的规范参考为 `/en/commands` | ❌ INVALID (2026-03-10 的重复项；URL 通过重定向仍可访问；用户选择保留原样) |
| 5 | MED | 描述变更 | 将 Scheduled Tasks 描述从"最长 3 天"更新为"最长 7 天" — 文档现在指定周期性任务为七天过期 | ✅ COMPLETE (描述已更新为"最长 7 天") |
| 6 | MED | 缺失概念 | 在 Hot 表格中添加 Devcontainers 行 — 预配置的开发容器，具有安全隔离和防火墙规则（`/en/devcontainer`） | ✅ COMPLETE (已在 Routines 之后添加行，位置为 .devcontainer/) |

---

## [2026-04-16 08:20 PM PKT] Claude Code v2.1.110

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 过时 URL | 修复 TIPS（第 223 行）中的 `web-scheduled-tasks` URL 为 `/en/routines` — URL 不在站点地图中；与 2026-04-14 在 Hot 表格中修复的过时 URL 相同，但 TIPS 实例被遗漏 | ✅ COMPLETE (URL 已更新为 /routines) |
| 2 | HIGH | 过时 URL | Commands URL `/slash-commands` 不在官方站点地图（111 个页面）中 — 重定向到 `/skills`；Commands 的规范参考为 `/en/commands` | ❌ INVALID (2026-03-10 的重复项；URL 通过重定向仍可访问；用户选择保留原样) |
| 3 | MED | 描述变更 | 将 TIPS（第 223 行）中的"最长 3 天"更新为"最长 7 天" — 与 2026-04-14 在 Hot 表格中更新的描述相同，但 TIPS 实例被遗漏 | ✅ COMPLETE (描述已更新为"最长 7 天") |
| 4 | LOW | 验证 | 所有 45 个外部文档 URL 已根据 llms.txt 站点地图（111 个页面）验证 — 发现 1 个失效链接（见 #1） | ✅ COMPLETE (web-scheduled-tasks 已标记) |
| 5 | LOW | 验证 | 所有本地徽章文件路径已验证 — 无缺失文件（已检查 20+ 个徽章目标） | ✅ COMPLETE (所有徽章目标均存在于文件系统中) |
| 6 | LOW | 验证 | Memory 锚点 `#organize-rules-with-clauderules` 已在 /memory 页面确认 | ✅ COMPLETE (标题段落 "Organize rules with `.claude/rules/`" 存在) |
| 7 | LOW | 验证 | Git Worktrees 锚点 `#run-parallel-claude-code-sessions-with-git-worktrees` 已在 /common-workflows 页面确认 | ✅ COMPLETE (标题段落存在) |
| 8 | LOW | 验证 | Auto Mode 锚点 `#eliminate-prompts-with-auto-mode` 已在 /permission-modes 页面确认 | ✅ COMPLETE (标题段落存在) |
| 9 | LOW | 验证 | Bundled Skills 锚点 `#bundled-skills` 已在 /skills 页面确认 | ✅ COMPLETE (标题段落存在) |
| 10 | LOW | 验证 | 所有 CONCEPTS 描述已与官方文档核对 — 未检测到偏差 | ✅ COMPLETE (所有描述准确) |
