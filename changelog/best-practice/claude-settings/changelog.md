# Settings 报告 — 变更日志历史

## 状态图例

| 状态 | 含义 |
|--------|---------|
| ✅ `COMPLETE (reason)` | 操作已执行并成功解决 |
| ❌ `INVALID (reason)` | 发现不正确、不适用或属于预期行为 |
| ✋ `ON HOLD (reason)` | 操作已推迟 — 等待外部依赖或用户决策 |

---

## [2026-03-05 06:18 AM PKT] Claude Code v2.1.69

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 缺失 Settings | 添加 13 个非 Hook 缺失 Settings 键（`$schema`、`availableModels`、`fastModePerSessionOptIn`、`teammateMode`、`prefersReducedMotion`、`sandbox.filesystem.*`、`sandbox.network.allowManagedDomainsOnly`、`sandbox.enableWeakerNetworkIsolation`、`allowManagedMcpServersOnly`、`blockedMarketplaces`、`includeGitInstructions`、`pluginTrustMessage`、`fileSuggestion` 表格条目） | ✅ COMPLETE（已添加到报告） |
| 2 | HIGH | 缺失环境变量 | 添加缺失的环境变量，包括 `CLAUDE_CODE_DISABLE_ADAPTIVE_THINKING`、`CLAUDE_CODE_DISABLE_1M_CONTEXT`、`CLAUDE_CODE_ACCOUNT_UUID`、`CLAUDE_CODE_DISABLE_GIT_INSTRUCTIONS`、`ENABLE_CLAUDEAI_MCP_SERVERS` 等 | ✅ COMPLETE（已添加 13 个缺失环境变量到报告） |
| 3 | HIGH | Effort 默认值 | 将 effort 级别默认值从 "High" 更新为 "Medium"（适用于 Max/Team 订阅者）；添加 Sonnet 4.6 支持（v2.1.68 变更） | ✅ COMPLETE（已更新默认值并添加 Sonnet 说明） |
| 4 | MED | Settings 层级 | 添加通过 macOS plist/Windows Registry 管理的 Settings（v2.1.61/v2.1.69）；记录跨作用域的数组合并行为 | ✅ COMPLETE（已添加 plist/registry 和合并说明） |
| 5 | MED | Sandbox 文件系统 | 添加 `sandbox.filesystem.allowWrite`、`denyWrite`、`denyRead` 及路径前缀语义（`//`、`~/`、`/`、`./`） | ✅ COMPLETE（已添加到 sandbox 表格） |
| 6 | MED | 权限语法 | 添加 `Agent(name)` 权限模式；记录 `MCP(server:tool)` 语法形式 | ✅ COMPLETE（已添加到工具语法表格） |
| 7 | MED | Plugin 缺漏 | 添加 `blockedMarketplaces`、`pluginTrustMessage` | ✅ COMPLETE（已添加到 plugins 表格） |
| 8 | MED | Model 配置 | 添加 `availableModels` 设置 | ✅ COMPLETE（已添加到常规设置表格） |
| 9 | MED | 可疑键 | 验证 `sandbox.network.deniedDomains`、`sandbox.ignoreViolations`、`pluginConfigs` — 存在于报告中但未在官方文档中出现 | ✋ ON HOLD（保留在报告中待验证） |
| 10 | LOW | 标题计数 | 将标题从 "38 settings and 84 env vars" 更新为反映实际计数（~55+ settings, ~110+ 环境变量） | ✅ COMPLETE（已更新标题） |
| 11 | LOW | CLAUDE.md 同步 | 更新 CLAUDE.md 配置层级（添加 managed/CLI/user 级别） | ✋ ON HOLD（等待用户批准） |
| 12 | LOW | 示例更新 | 使用 `$schema`、sandbox 文件系统、`Agent(*)`更新快速参考示例，移除 hooks 示例 | ✅ COMPLETE（已更新示例） |
| 13 | MED | Hooks 重定向 | 将 hooks 部分替换为指向 claude-code-hooks 仓库的重定向 | ✅ COMPLETE（hooks 已外部化到专用仓库） |

---

## [2026-03-07 02:17 PM PKT] Claude Code v2.1.71

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 行为变更 | 修复 `teammateMode`：类型 `boolean` → `string`，默认值 `false` → `"auto"`，描述 → "Agent team 显示模式：auto, in-process, tmux" | ✅ COMPLETE（类型、默认值和描述已更新） |
| 2 | HIGH | 新 Setting | 将 `allowManagedPermissionRulesOnly` 添加到权限表格（boolean，仅限 managed） | ✅ COMPLETE（已添加到 Permission Keys 表格） |
| 3 | HIGH | 缺失环境变量 | 添加约 31 个缺失环境变量，包括已确认的（`CLAUDE_CODE_MAX_OUTPUT_TOKENS`、`CLAUDE_CODE_DISABLE_FAST_MODE`、`CLAUDE_CODE_DISABLE_AUTO_MEMORY`、`CLAUDE_CODE_USER_EMAIL`、`CLAUDE_CODE_ORGANIZATION_UUID`、`CLAUDE_CONFIG_DIR`）和 Agent 报告的（Foundry、Bedrock、mTLS、shell prefix 等） | ✅ COMPLETE（已添加 31 个环境变量到表格） |
| 4 | MED | 默认值变更 | 修复 `plansDirectory` 默认值从 `.claude/plans/` 到 `~/.claude/plans` | ✅ COMPLETE（默认值已更新） |
| 5 | MED | 描述变更 | 修复 `sandbox.enableWeakerNetworkIsolation` 描述为 "（仅 macOS）允许访问系统 TLS 信任；降低安全性" | ✅ COMPLETE（描述已更新） |
| 6 | MED | 作用域修复 | 修复 `extraKnownMarketplaces` 作用域从 "Any" 到 "Project" | ✅ COMPLETE（作用域和描述已更新） |
| 7 | MED | 边界违规 | 将 `claude-cli-startup-flags.md` 中的 `CLAUDE_CODE_EFFORT_LEVEL` 替换为指向 settings 报告的交叉引用 | ✅ COMPLETE（已替换为链接） |
| 8 | MED | 版本徽章 | 将报告版本从 v2.1.69 更新到 v2.1.71 | ✅ COMPLETE（徽章和标题已更新） |
| 9 | LOW | 可疑键 | 验证 `skipWebFetchPreflight`、`sandbox.ignoreViolations`、`sandbox.network.deniedDomains`、`skippedMarketplaces`、`skippedPlugins`、`pluginConfigs` | ✋ ON HOLD（保留在报告中待验证 — 自 2026-03-05 延续） |
| 10 | LOW | CLAUDE.md 同步 | 更新 CLAUDE.md 配置层级（3 级 → 5+ 级） | ✅ COMPLETE（已更新为包含 managed 层的 5 级层级） |

---

## [2026-03-12 12:23 PM PKT] Claude Code v2.1.74

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 行为变更 | 修复 `dontAsk` 权限模式描述："自动接受所有工具" → "自动拒绝未通过 `/permissions` 或 `permissions.allow` 规则预批准的工具" | ✅ COMPLETE（描述已按官方权限文档修正） |
| 2 | HIGH | 新 Setting | 将 `modelOverrides` 添加到 Model Configuration 部分（object，将 Anthropic model ID 映射到特定提供商 ID，如 Bedrock ARN） | ✅ COMPLETE（已添加示例和描述） |
| 3 | HIGH | 新 Setting | 将 `allow_remote_sessions` 添加到仅限 managed 的设置列表（boolean，默认 `true`，控制 Remote Control/web 会话访问） | ✅ COMPLETE（已添加到 Permission Keys 表格） |
| 4 | HIGH | 默认值变更 | 修复 `$schema` URL 从 `https://www.schemastore.org/...` 到 `https://json.schemastore.org/...`（按官方文档） | ✅ COMPLETE（已在描述、示例和来源中更新） |
| 5 | MED | 描述变更 | 修复 `ANTHROPIC_CUSTOM_HEADERS` 格式描述从 "JSON string" 到 "Name: Value 格式，换行分隔" | ✅ COMPLETE（描述已按官方文档更新） |
| 6 | MED | 未验证模式 | `askEdits` 和 `viewOnly` 权限模式未在官方文档中出现 — 仅记录了 5 种模式（default、acceptEdits、plan、dontAsk、bypassPermissions） | ✅ COMPLETE（已在表格中标记为 "未在官方文档中 — 未验证"） |
| 7 | MED | 缺失环境变量 | 添加 `CLAUDE_CODE_SESSIONEND_HOOKS_TIMEOUT_MS`、`CLAUDE_CODE_DISABLE_FEEDBACK_SURVEY`、`CLAUDE_CODE_DISABLE_TERMINAL_TITLE`、`CLAUDE_CODE_IDE_SKIP_AUTO_INSTALL`、`CLAUDE_CODE_OTEL_HEADERS_HELPER_DEBOUNCE_MS` | ✅ COMPLETE（已添加 5 个环境变量及 `CLAUDE_CODE_OTEL_HEADERS_HELPER_DEBOUNCE_MS`） |
| 8 | MED | 新 Setting | 将 `autoMemoryDirectory` 添加到 Core Configuration（string，自定义自动记忆目录）— 版本不确定（Agent 意见不一致：v2.1.68 vs v2.1.74），未在 settings 页面出现 | ✅ COMPLETE（已添加到 plansDirectory 附近 — 版本未解决） |
| 9 | LOW | 可疑键 | 验证 `skipWebFetchPreflight`、`sandbox.ignoreViolations`、`sandbox.network.deniedDomains`、`skippedMarketplaces`、`skippedPlugins`、`pluginConfigs` — 仍未在官方文档中出现 | ✋ ON HOLD（保留在报告中待验证 — 自 2026-03-05 延续） |
| 10 | LOW | 缺失环境变量 | 将 `CLAUDE_CODE_SUBAGENT_MODEL` 添加到环境变量表格（已在 Model 环境变量示例代码块中但缺失于表格） | ✅ COMPLETE（已添加到环境变量表格） |
| 11 | LOW | 示例更新 | 使用 `modelOverrides` 和修正的 `$schema` URL 更新快速参考示例 | ✅ COMPLETE（两项均已更新到示例中） |

---

## [2026-03-14 01:35 AM PKT] Claude Code v2.1.75

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | Settings 层级 | 重构以匹配官方 5 级层级：Managed (#1) > CLI 参数 > Local > Project > User。移除 `~/.claude/settings.local.json` 行。添加 managed 层内部优先级（server-managed > MDM > file > HKCU）。注意 Managed "不能被任何其他级别覆盖，包括 CLI 参数" | ✅ COMPLETE（已重构表格为 5 级，包含 Managed 为 #1，添加了传递方式、内部优先级和文件路径） |
| 2 | HIGH | 行为变更 | 修复 `availableModels` 描述：从复杂对象数组（`title`/`modelId`/`effortOptions`）改为简单字符串数组 `["sonnet", "haiku"]`（按官方文档） | ✅ COMPLETE（已更新描述以匹配官方文档格式） |
| 3 | HIGH | 行为变更 | 添加 `cleanupPeriodDays` `0` 值行为："设置为 `0` 将在启动时删除所有现有转录并完全禁用会话持久化" | ✅ COMPLETE（已在描述中添加 0 值行为） |
| 4 | HIGH | 权限语法 | 在权限部分添加求值顺序说明："规则按顺序求值：先 deny 规则，然后 ask，然后 allow。第一个匹配的规则生效。" | ✅ COMPLETE（已在 Bash 通配符说明之前添加求值顺序） |
| 5 | MED | 描述变更 | 添加 `autoMemoryDirectory` 作用域限制："不接受项目设置（`.claude/settings.json`）。接受来自 policy、local 和 user 设置" | ✅ COMPLETE（已在描述中添加作用域限制） |
| 6 | MED | 描述变更 | 添加 `permissions.defaultMode` Remote 环境说明：在 Remote 环境中仅 `acceptEdits` 和 `plan` 被接受（v2.1.70） | ✅ COMPLETE（已在描述中添加 Remote 限制） |
| 7 | MED | Model 配置 | 添加 Opus 4.6 1M 上下文默认说明：自 v2.1.75 起，1M 上下文是 Max/Team/Enterprise 计划的默认值 | ✅ COMPLETE（已添加到 Effort Level 说明） |
| 8 | MED | Settings 层级 | 添加 Windows managed 路径说明：v2.1.75 移除了已弃用的 `C:\ProgramData\ClaudeCode\` 回退 — 使用 `C:\Program Files\ClaudeCode\managed-settings.json` | ✅ COMPLETE（已在层级部分添加弃用说明） |
| 9 | MED | 显示和用户体验 | 添加 `fileSuggestion` stdin JSON 格式（`{"query": "..."}`）和 15 路径输出限制详情 | ✅ COMPLETE（已在 File Suggestion 部分添加 stdin 格式和输出限制） |
| 10 | MED | Settings 层级 | 将数组合并说明从 "merged" 更新为 "concatenated and deduplicated"（按官方文档） | ✅ COMPLETE（已在层级 Important 部分更新措辞） |
| 11 | LOW | 可疑键 | `sandbox.ignoreViolations`、`sandbox.network.deniedDomains` 仍未在官方文档或 JSON schema 顶层出现 | ✋ ON HOLD（保留在报告中待验证 — 自 2026-03-05 延续） |
| 12 | LOW | 可疑键 | `skipWebFetchPreflight`、`skippedMarketplaces`、`skippedPlugins`、`pluginConfigs` — 已在 JSON schema 中确认但未在官方 settings 页面出现 | ✋ ON HOLD（保留在报告中 — 按 schema 有效，自 2026-03-05 延续） |

---

## [2026-03-15 12:52 PM PKT] Claude Code v2.1.76

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新 Setting | 将 `effortLevel` 添加到 General Settings 或 Model Configuration — 跨会话持久化 effort 级别（`"low"`、`"medium"`、`"high"`）。已在官方 settings 页面确认 | ✋ ON HOLD（等待用户批准） |
| 2 | HIGH | 新 Settings | 添加 Worktree Settings 部分，包含 `worktree.sparsePaths`（数组，sparse-checkout cone 模式）和 `worktree.symlinkDirectories`（数组，符号链接目录以避免重复）。已在官方 settings 页面确认 | ✋ ON HOLD（等待用户批准） |
| 3 | HIGH | 新 Setting | 将 `feedbackSurveyRate` 添加到 General Settings — 会话质量调查的概率（0-1）。已在官方 settings 页面确认 | ✋ ON HOLD（等待用户批准） |
| 4 | HIGH | 缺失环境变量 | 添加 20 个缺失环境变量到表格：`CLAUDE_CODE_AUTO_COMPACT_WINDOW`、`CLAUDE_CODE_ENABLE_PROMPT_SUGGESTION`、`CLAUDE_CODE_PLAN_MODE_REQUIRED`、`CLAUDE_CODE_TEAM_NAME`、`CLAUDE_CODE_TASK_LIST_ID`、`CLAUDE_ENV_FILE`、`FORCE_AUTOUPDATE_PLUGINS`、`HTTP_PROXY`、`HTTPS_PROXY`、`NO_PROXY`、`MCP_TOOL_TIMEOUT`、`MCP_CLIENT_SECRET`、`MCP_OAUTH_CALLBACK_PORT`、`IS_DEMO`、`SLASH_COMMAND_TOOL_CHAR_BUDGET`、`VERTEX_REGION_CLAUDE_3_5_HAIKU`、`VERTEX_REGION_CLAUDE_3_7_SONNET`、`VERTEX_REGION_CLAUDE_4_0_OPUS`、`VERTEX_REGION_CLAUDE_4_0_SONNET`、`VERTEX_REGION_CLAUDE_4_1_OPUS`。已在官方 /en/env-vars 页面确认 | ✋ ON HOLD（等待用户批准） |
| 5 | HIGH | 缺失环境变量 | 将 `ANTHROPIC_DEFAULT_OPUS_MODEL`、`ANTHROPIC_DEFAULT_SONNET_MODEL`、`MAX_THINKING_TOKENS` 从仅代码块移到 Common Environment Variables 表格 | ✋ ON HOLD（等待用户批准） |
| 6 | HIGH | 失效链接 | 修复 `https://claudelog.com/configuration/` — 返回 ECONNREFUSED。移除或替换为可用来源 | ✋ ON HOLD（等待用户批准） |
| 7 | MED | 描述变更 | 更新 `cleanupPeriodDays` 描述，添加：设置为 0 时 "hooks 接收空的 `transcript_path`"。按官方文档 | ✋ ON HOLD（等待用户批准） |
| 8 | MED | 未验证环境变量 | 将报告中存在但未在官方文档中出现的 7 个环境变量标记为未验证：`CLAUDE_CODE_DISABLE_MCP`、`CLAUDE_CODE_DISABLE_TOOLS`、`CLAUDE_CODE_HIDE_ACCOUNT_INFO`、`CLAUDE_CODE_MAX_TURNS`、`CLAUDE_CODE_PROMPT_CACHING_ENABLED`、`CLAUDE_CODE_SKIP_SETTINGS_SETUP`、`DISABLE_NON_ESSENTIAL_MODEL_CALLS` | ✋ ON HOLD（等待用户批准） |
| 9 | MED | 新来源 | 将 `https://code.claude.com/docs/en/env-vars` 添加到来源部分 — 官方环境变量参考页面 | ✋ ON HOLD（等待用户批准） |
| 10 | MED | 示例更新 | 使用 `effortLevel` 和 `worktree` 设置更新快速参考示例 | ✋ ON HOLD（等待用户批准） |
| 11 | LOW | 可疑键 | `sandbox.ignoreViolations`、`sandbox.network.deniedDomains` 仍未在官方文档 sandbox 表格中出现 | ✋ ON HOLD（保留在报告中待验证 — 自 2026-03-05 延续） |
| 12 | LOW | 可疑键 | `skipWebFetchPreflight`、`skippedMarketplaces`、`skippedPlugins`、`pluginConfigs` — 仍在 JSON schema 中但未在官方 settings 页面出现 | ✋ ON HOLD（保留在报告中 — 按 schema 有效，自 2026-03-05 延续） |

---

## [2026-03-15 01:10 PM PKT] Claude Code v2.1.76

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新 Setting | 将 `effortLevel` 添加到 Model Configuration — 跨会话持久化 effort 级别（`"low"`、`"medium"`、`"high"`）。同时将 `/effort` 命令添加到 Useful Commands 并更新 Effort Level 操作指南部分 | ✅ COMPLETE（已添加到 Model Overrides 表格，更新了操作指南，添加了 /effort 命令） |
| 2 | HIGH | 新 Settings | 添加 Worktree Settings 部分，包含 `worktree.sparsePaths`（数组，sparse-checkout cone 模式）和 `worktree.symlinkDirectories`（数组，符号链接目录以避免重复） | ✅ COMPLETE（在 Core Configuration 中新建 Worktree Settings 子部分，含表格和示例） |
| 3 | HIGH | 新 Setting | 将 `feedbackSurveyRate` 添加到 General Settings — 会话质量调查的概率（0-1） | ✅ COMPLETE（已添加到 General Settings 表格） |
| 4 | HIGH | 缺失环境变量 | 添加 23 个缺失环境变量到表格（20 个全新 + 3 个从仅代码块提升） | ✅ COMPLETE（已将全部 23 个环境变量添加到 Common Environment Variables 表格） |
| 5 | HIGH | 失效链接 | 上次运行标记 `https://claudelog.com/configuration/` 为 ECONNREFUSED — 现在加载成功 | ✅ COMPLETE（链接已恢复，无需操作） |
| 6 | MED | 权限语法 | 添加 Read/Edit gitignore 风格路径模式（`//path`、`~/path`、`/path`、`./path`），词边界通配符详情，以及旧版 `:*` 弃用说明 | ✅ COMPLETE（已添加路径模式表格、词边界说明和 `:*` 弃用） |
| 7 | MED | 描述变更 | 更新 `cleanupPeriodDays`，添加设置为 0 时 "hooks 接收空的 `transcript_path`" | ✅ COMPLETE（已添加到描述） |
| 8 | MED | 未验证环境变量 | 将未在官方文档中出现的 7 个环境变量标记为未验证 | ✅ COMPLETE（已添加 "未在官方文档中 — 未验证" 标记） |
| 9 | MED | 新来源 | 将 `https://code.claude.com/docs/en/env-vars` 和 `https://code.claude.com/docs/en/permissions` 添加到来源部分 | ✅ COMPLETE（已添加两个 URL） |
| 10 | MED | 示例更新 | 使用 `effortLevel` 和 `worktree` 设置更新快速参考示例 | ✅ COMPLETE（已将 effortLevel 和 worktree 块添加到示例） |
| 11 | LOW | 可疑键 | `sandbox.ignoreViolations`、`sandbox.network.deniedDomains` 仍未在官方文档 sandbox 表格中出现 | ✋ ON HOLD（保留在报告中待验证 — 自 2026-03-05 延续） |
| 12 | LOW | 可疑键 | `skipWebFetchPreflight`、`skippedMarketplaces`、`skippedPlugins`、`pluginConfigs` — 仍在 JSON schema 中但未在官方 settings 页面出现 | ✋ ON HOLD（保留在报告中 — 按 schema 有效，自 2026-03-05 延续） |

---

## [2026-03-17 12:54 PM PKT] Claude Code v2.1.77

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新 Setting | 将 `sandbox.filesystem.allowRead` 添加到 Sandbox Settings 表格 — 在 `denyRead` 区域内重新允许读取访问（数组，默认 `[]`）。已在 v2.1.77 变更日志中确认 | ✅ COMPLETE（已添加到 Sandbox Settings 表格 denyRead 行之后） |
| 2 | HIGH | 描述变更 | 更新 `CLAUDE_CODE_MAX_OUTPUT_TOKENS` 描述：Opus 4.6 默认值增加到 64k，Opus 4.6 和 Sonnet 4.6 上限增加到 128k（v2.1.77 变更日志） | ✅ COMPLETE（已更新特定模型的默认值和上限） |
| 3 | HIGH | 缺失环境变量 | 将 `CLAUDECODE` 添加到 Common Environment Variables 表格 — 在衍生的 shell 环境中设置为 `1`。已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已添加到环境变量表格） |
| 4 | HIGH | 缺失环境变量 | 将 `CLAUDE_CODE_SKIP_FAST_MODE_NETWORK_ERRORS` 添加到 Common Environment Variables 表格 — 在组织状态检查失败时允许 fast mode。已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已添加到环境变量表格） |
| 5 | MED | 环境变量表格 | 将 `ANTHROPIC_MODEL` 和 `ANTHROPIC_DEFAULT_HAIKU_MODEL` 从仅代码块移到 Common Environment Variables 表格。两者均已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已将两者添加到环境变量表格中其他 ANTHROPIC_ 变量附近） |
| 6 | MED | 可疑键升级 | `sandbox.network.deniedDomains` — 连续 8 次 ON HOLD（自 2026-03-05）。未在官方文档页面或 JSON schema 中出现。按规则 10B：标记为 "未在官方文档中 — 未验证" | ✅ COMPLETE（已在描述中添加未验证标注） |
| 7 | MED | 可疑键升级 | `allow_remote_sessions` — 未在官方文档页面或 JSON schema 中出现。标记为 "未在官方文档中 — 未验证" | ✅ COMPLETE（已在描述中添加未验证标注） |
| 8 | LOW | 可疑键解决 | `sandbox.ignoreViolations` — 连续 8 次 ON HOLD。已在 JSON schema 中确认。标注："在 JSON schema 中，未在官方 settings 页面" | ✅ COMPLETE（已在描述中添加 schema 标注） |
| 9 | LOW | 可疑键解决 | `skipWebFetchPreflight`、`skippedMarketplaces`、`skippedPlugins`、`pluginConfigs` — 连续 8 次 ON HOLD。全部已在 JSON schema 中确认。标注："在 JSON schema 中，未在官方 settings 页面" | ✅ COMPLETE（已在全部 4 个描述中添加 schema 标注） |
| 10 | LOW | 标题计数 | 将标题环境变量计数从 "160+" 更新为 "100+" — 实际表格有 97 个环境变量 | ✅ COMPLETE（标题已更新为 "100+ environment variables"，版本更新为 v2.1.77） |

---

## [2026-03-18 11:53 PM PKT] Claude Code v2.1.78

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 缺失 Setting | 将 `voiceEnabled` 添加到 General Settings 表格 — 启用按键说话语音听写（boolean，由 `/voice` 写入，需要 Claude.ai 账户）。已在官方 settings 页面确认 | ✅ COMPLETE（已添加到 General Settings 表格 feedbackSurveyRate 之前） |
| 2 | HIGH | 缺失 Setting | 将 `filesystem.allowManagedReadPathsOnly` 添加到 Sandbox Settings 表格 — 仅限 managed，只有 managed 的 `allowRead` 路径被接受（boolean，默认 false）。已在官方 settings 页面确认 | ✅ COMPLETE（已添加到 Sandbox Settings 表格 enableWeakerNetworkIsolation 之前） |
| 3 | HIGH | 显示位置 | 将 `showTurnDuration` 和 `terminalProgressBarEnabled` 从 Display Settings 表格移到单独的 "Global Config Settings (~/.claude.json)" 子部分。官方文档声明："将它们添加到 settings.json 会触发 schema 验证错误" | ✅ COMPLETE（创建了新子部分含表格；从 settings.json Display Settings 表格和示例中移除） |
| 4 | HIGH | 默认值变更 | 修复 `MAX_MCP_OUTPUT_TOKENS` 默认值从 50000 到 25000。官方 /en/env-vars 页面确认默认值为 25000 | ✅ COMPLETE（默认值已更新，添加了警告阈值说明） |
| 5 | HIGH | 缺失环境变量 | 将 `CLAUDE_CODE_NEW_INIT`、`CLAUDE_CODE_PLUGIN_SEED_DIR`、`DISABLE_FEEDBACK_COMMAND` 添加到环境变量表格。全部已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已添加全部 3 个环境变量到表格） |
| 6 | MED | 验证修复 | 移除 `allow_remote_sessions` 的 "未验证" 标注 — 现已在官方权限页面确认为仅限 managed 的设置。上次运行（v2.1.77 #7）错误地将其标记为未验证 | ✅ COMPLETE（已移除 "未验证" 标注） |
| 7 | MED | 环境变量重命名 | 将 `DISABLE_BUG_COMMAND` 更新为 `DISABLE_FEEDBACK_COMMAND` — 官方文档称 `DISABLE_FEEDBACK_COMMAND` 是当前名称，`DISABLE_BUG_COMMAND` 是 "旧名称" | ✅ COMPLETE（已重命名并添加别名说明） |
| 8 | MED | 描述变更 | 更新 `CLAUDE_CODE_EFFORT_LEVEL` 以包含 `max`（仅 Opus 4.6）和 `auto` 值。官方 /en/env-vars 页面确认："值：low, medium, high, max（仅 Opus 4.6）, 或 auto" | ✅ COMPLETE（描述已更新包含所有值和优先级说明） |
| 9 | MED | 描述变更 | 修复 `CLAUDE_CODE_ENABLE_TASKS` 描述 — 官方："设置为 true 以在非交互模式（-p 标志）中启用任务跟踪。交互模式下默认开启。" 报告当前显示 "设置为 false 以禁用" | ✅ COMPLETE（描述已修正以匹配官方文档） |
| 10 | MED | 描述变更 | 更新 `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` 说明："等效于设置 DISABLE_AUTOUPDATER、DISABLE_FEEDBACK_COMMAND、DISABLE_ERROR_REPORTING 和 DISABLE_TELEMETRY" | ✅ COMPLETE（描述已更新包含等效变量列表） |
| 11 | MED | 示例更新 | 从快速参考示例中移除 `showTurnDuration` — 按官方文档不属于 settings.json | ✅ COMPLETE（已从快速参考示例和 Display & UX 示例中移除） |
| 12 | LOW | 环境变量默认值 | 验证 `MCP_TIMEOUT` 默认值（报告显示 10000）— 官方文档未指定默认值 | ✅ COMPLETE（已移除未验证的默认值 — 官方文档省略了此值） |

---

## [2026-03-19 12:38 PM PKT] Claude Code v2.1.79

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 缺失环境变量 | 将 `ANTHROPIC_CUSTOM_MODEL_OPTION`、`ANTHROPIC_CUSTOM_MODEL_OPTION_NAME`、`ANTHROPIC_CUSTOM_MODEL_OPTION_DESCRIPTION` 添加到 Common Environment Variables 表格 — 用于向 `/model` 选择器添加自定义条目的 model 配置变量。已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已将 3 个环境变量添加到表格中 ANTHROPIC_BASE_URL 之后） |
| 2 | HIGH | 描述变更 | 将 `CLAUDE_CODE_PLUGIN_SEED_DIR` 从单数更新为复数："一个或多个只读 plugin seed 目录的路径，在 Unix 上用 `:` 分隔，在 Windows 上用 `;` 分隔"。在 v2.1.79 变更日志中变更。已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（描述已更新为支持多目录） |
| 3 | HIGH | Sandbox 路径前缀 | 修复 sandbox.filesystem 路径前缀文档：`/` = 绝对路径（标准 Unix），`./` = 项目相对路径，`//` = 旧版仍可用。报告当前显示反向约定。官方文档明确说明："此语法与 Read 和 Edit 权限规则不同" | ✅ COMPLETE（已更新全部 4 个 sandbox.filesystem 条目的正确前缀约定，添加了与 Read/Edit 权限规则的交叉引用说明，添加了跨作用域合并详情） |
| 4 | MED | 描述变更 | 扩展 `CLAUDE_CODE_AUTO_COMPACT_WINDOW` 描述 — 当前 "自动压缩窗口行为配置" 过于简略。官方文档描述：token 容量、默认值（200K 标准 / 1M 扩展）、与 `CLAUDE_AUTOCOMPACT_PCT_OVERRIDE` 的交互、状态行解耦 | ✅ COMPLETE（已扩展描述包含 token 容量、模型默认值、AUTOCOMPACT_PCT 交互和状态行解耦） |

---

## [2026-03-20 08:41 AM PKT] Claude Code v2.1.80

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新 Setting | 将 `channelsEnabled` 添加到 MCP Settings 表格 — 仅限 managed 的 boolean，控制 Team 和 Enterprise 用户的频道消息传递。已在官方 settings 页面确认 | ✅ COMPLETE（已添加到 MCP Settings 表格 allowManagedMcpServersOnly 之后） |
| 2 | MED | 版本徽章 | 将报告版本从 v2.1.79 更新到 v2.1.80 | ✅ COMPLETE（徽章和标题已更新） |

---

## [2026-03-21 09:17 PM PKT] Claude Code v2.1.81

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 缺失 Settings (~/.claude.json) | 将 `autoConnectIde`（boolean，默认 `false`）和 `autoInstallIdeExtension`（boolean，默认 `true`）添加到 Global Config Settings 表格。已在官方 settings 页面 "Global config settings" 下确认 | ✅ COMPLETE（已将两个键添加到 ~/.claude.json 表格 showTurnDuration 之前） |
| 2 | HIGH | 不正确的 Setting | `allow_remote_sessions` 列在 Permission Keys 表格中为仅限 managed 的 boolean，但官方权限页面声明："Remote Control 和 web 会话的访问不受 managed settings 键控制。" 标记为未验证或移除 | ✅ COMPLETE（重新添加了未验证标注，包含官方文档引用和管理 UI 链接） |
| 3 | MED | 版本更新 | 将报告版本徽章从 v2.1.80 更新到 v2.1.81 | ✅ COMPLETE（徽章、标题版本和标题文字已更新） |
| 4 | MED | 新 Setting | 添加 `showClearContextOnPlanAccept` — 已在 v2.1.81 变更日志中确认。当设置为 `true` 时，恢复计划接受时的 "清除上下文" 选项（默认隐藏）。尚未在官方 settings 页面出现 — 可能是 `~/.claude.json` 键 | ✅ COMPLETE（已添加到 Global Config Settings 表格，带变更日志来源说明） |
| 5 | MED | Plugin 文档 | 将 `source: 'settings'` 记录为 Plugin Settings 部分中的 marketplace 来源类型。官方 settings 页面将其列为 `extraKnownMarketplaces` 的 7 种来源类型之一 | ✅ COMPLETE（添加了全部 7 种来源类型列表和内联 marketplace 示例） |
| 6 | MED | 状态行字段 | 将 `rate_limits` 字段组添加到 Status Line Input Fields 表格 — 包括 `five_hour.used_percentage`、`five_hour.resets_at`、`seven_day.used_percentage`、`seven_day.resets_at`。在 v2.1.80 中添加 | ✅ COMPLETE（已将 4 个 rate_limits 字段添加到 Status Line Input Fields 表格） |

---

## [2026-03-23 10:02 PM PKT] Claude Code v2.1.81

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 缺失 Setting (~/.claude.json) | 将 `editorMode`（string，默认 `"normal"`，值：`"normal"` 或 `"vim"`）添加到 Global Config Settings 表格。运行 `/vim` 时自动写入。已在官方 settings 页面确认 | ✅ COMPLETE（已添加到 Global Config Settings 表格 autoInstallIdeExtension 之后） |
| 2 | HIGH | 文件作用域修复 | 将 `showClearContextOnPlanAccept` 从 Global Config Settings (~/.claude.json) 移到 General Settings (settings.json)。官方文档现将其列在主 Available settings 表格中，而非 Global config 表格。移除过时标注 "尚未在官方 settings 页面" | ✅ COMPLETE（已移到 General Settings 表格 feedbackSurveyRate 之前，移除了过时标注） |
| 3 | MED | 描述变更 | 修复 `terminalProgressBarEnabled` 支持的终端从 "Windows Terminal, iTerm2" 到 "ConEmu, Ghostty 1.2.0+, 和 iTerm2 3.6.6+"（按官方文档） | ✅ COMPLETE（终端列表已更新） |
| 4 | MED | 描述变更 | 在 `availableModels` 描述中添加 "Config tool" — 官方文档称 "通过 `/model`、`--model`、Config tool 或 `ANTHROPIC_MODEL`"。报告当前遗漏了 "Config tool" | ✅ COMPLETE（已将 "Config tool" 添加到描述） |

---

## [2026-03-25 08:16 PM PKT] Claude Code v2.1.83

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新 Setting | 将 `autoMode` 添加到权限部分 — 包含 `environment`、`allow`、`soft_deny` 数组的对象，用于配置 auto mode 分类器。不从共享项目设置（`.claude/settings.json`）读取。可在 user、local 和 managed settings 中使用。已在官方 settings + permissions 页面确认 | ✅ COMPLETE（已添加到 Permission Keys 表格，包含完整描述、作用域限制和 `claude auto-mode defaults` 说明） |
| 2 | HIGH | 新 Setting | 将 `disableAutoMode` 添加到权限部分 — string，设置为 `"disable"` 以阻止 auto mode 激活。从 Shift+Tab 循环中移除 `auto`。可在任何 settings 级别设置，在 managed settings 中最有用。已在官方 settings + permissions 页面确认 | ✅ COMPLETE（已添加到 Permission Keys 表格 `autoMode` 之后） |
| 3 | HIGH | 新权限模式 | 将 `auto` 添加到 Permission Modes 表格 — 后台分类器替代手动提示。研究预览。需要 Team 计划 + Sonnet/Opus 4.6。已在官方 permission-modes 页面确认 | ✅ COMPLETE（已添加到 Permission Modes 表格，包含分类器详情和回退行为） |
| 4 | HIGH | 新 Setting | 将 `sandbox.failIfUnavailable` 添加到 Sandbox Settings 表格 — boolean，默认 `false`，当 sandbox 启用但无法启动时以错误退出而非以无沙箱方式运行。已在 v2.1.83 变更日志中确认 | ✅ COMPLETE（已添加到 Sandbox Settings 表格 `sandbox.enabled` 之后） |
| 5 | HIGH | 新 Setting | 将 `disableDeepLinkRegistration` 添加到 General Settings 表格 — boolean，阻止 `claude-cli://` 协议处理器注册。已在 v2.1.83 变更日志中确认 | ✅ COMPLETE（已添加到 General Settings 表格 `feedbackSurveyRate` 之前） |
| 6 | HIGH | 缺失环境变量 | 将 `CLAUDE_CODE_SUBPROCESS_ENV_SCRUB` 添加到 Common Environment Variables 表格 — 设置为 `1` 以从子进程环境（Bash 工具、hooks、MCP stdio 服务器）中剥离 Anthropic 和云提供商凭据。已在 v2.1.83 变更日志中确认 | ✅ COMPLETE（已添加到环境变量表格 `CLAUDE_CODE_SUBAGENT_MODEL` 之后） |
| 7 | HIGH | Settings 层级 | 将 `managed-settings.d/` 插入目录添加到 Managed Settings 部分 — 与 `managed-settings.json` 并列的独立策略片段，按字母顺序合并。已在 v2.1.83 变更日志中确认 | ✅ COMPLETE（已作为项目符号添加到 managed settings 传递方式下） |
| 8 | HIGH | 失效链接 | 修复来源中的 `https://claudelog.com/configuration/` — 返回 403 Forbidden。移除或替换为可用来源 | ✅ COMPLETE（已替换为 `https://claudelog.com/claude-code-changelog/`，验证可用） |
| 9 | MED | 版本徽章 | 将报告版本从 v2.1.81 更新到 v2.1.83 | ✅ COMPLETE（徽章和标题已在 Phase 2.6 中更新） |
| 10 | MED | 示例更新 | 将 `autoMode` 添加到快速参考示例以演示 auto mode 分类器配置 | ✅ COMPLETE（已在 `permissions` 块之前添加包含 `environment` 数组的 `autoMode` 块） |
| 11 | MED | 路径变更 | 修复 Windows 注册表路径从 `Software\Anthropic\ClaudeCode` 到 `SOFTWARE\Policies\ClaudeCode`（HKLM 和 HKCU）。官方文档已更新为使用 `Policies` 子键 | ✅ COMPLETE（已更新为 `HKLM\SOFTWARE\Policies\ClaudeCode` 和 `HKCU\SOFTWARE\Policies\ClaudeCode`，包含优先级说明） |
| 12 | LOW | 缺失别名 | 将 `opus[1m]` 添加到 Model Aliases 表格 — Opus 4.6 带 1M 上下文，自 v2.1.75 起在 Max/Team/Enterprise 上默认可用 | ✅ COMPLETE（已添加到 Model Aliases 表格 `sonnet[1m]` 之后） |

---

## [2026-03-26 01:04 PM PKT] Claude Code v2.1.84

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新 Setting | 将 `defaultShell` 添加到 General Settings — string，默认 `"bash"`，接受 `"bash"` 或 `"powershell"`。在 Windows 上通过 PowerShell 路由交互式 `!` 命令。需要 `CLAUDE_CODE_USE_POWERSHELL_TOOL=1`。已在官方 settings 页面确认 | ✅ COMPLETE（已添加到 General Settings 表格 teammateMode 之后） |
| 2 | HIGH | 新 Setting | 将 `allowedChannelPlugins` 添加到 MCP Settings — 数组，仅限 managed。可推送消息的频道 plugin 白名单。设置后替换默认的 Anthropic 白名单。需要 `channelsEnabled: true`。已在官方 settings 页面确认 | ✅ COMPLETE（已添加到 MCP Settings 表格 channelsEnabled 之后） |
| 3 | HIGH | 新 Setting | 将 `useAutoModeDuringPlan` 添加到 Permission Keys — boolean，默认 `true`。当 auto mode 可用时，plan mode 使用 auto mode 语义。不从共享项目设置读取。已在官方 settings 页面确认 | ✅ COMPLETE（已添加到 Permission Keys 表格 disableAutoMode 之后） |
| 4 | HIGH | 缺失环境变量 | 添加 9 个 model 自定义环境变量：`ANTHROPIC_DEFAULT_{OPUS,SONNET,HAIKU}_MODEL_{NAME,DESCRIPTION,SUPPORTED_CAPABILITIES}` 用于 Bedrock/Vertex/Foundry 上的 `/model` 选择器自定义。已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已在每个基础 model 变量之后添加 3 个变量：Haiku、Opus、Sonnet） |
| 5 | HIGH | 缺失环境变量 | 添加 `CLAUDE_CODE_DISABLE_NONSTREAMING_FALLBACK` — 在流式传输失败时禁用非流式回退。防止通过代理的重复工具执行。已在官方 /en/env-vars 页面确认（v2.1.83 添加，上次运行遗漏） | ✅ COMPLETE（已添加到 CLAUDE_CODE_DISABLE_FAST_MODE 之后） |
| 6 | HIGH | 缺失环境变量 | 添加 `CLAUDE_CODE_USE_POWERSHELL_TOOL` — 在 Windows 上启用 PowerShell 工具（选择性加入预览）。仅原生 Windows，不含 WSL。已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已添加到 CLAUDE_CODE_USE_FOUNDRY 之后） |
| 7 | HIGH | 失效链接 | 修复来源中的 `https://claudelog.com/claude-code-changelog/` — 返回 403 Forbidden。替换为官方 GitHub 变更日志 URL | ✅ COMPLETE（已替换为 github.com/anthropics/claude-code/blob/main/CHANGELOG.md） |
| 8 | MED | Settings 层级 | 更新 managed 层优先级："file-based（`managed-settings.d/*.json` + `managed-settings.json`）"，添加 "across tiers" 限定词。按官方文档添加层内合并说明 | ✅ COMPLETE（已更新优先级描述，包含 file-based 层和跨层限定词） |
| 9 | MED | Settings 层级 | 扩展插入目录合并语义：systemd 约定、标量覆盖、数组拼接+去重、深度合并、隐藏文件排除、数字前缀建议。按官方 settings 页面 | ✅ COMPLETE（已扩展包含完整 systemd 约定详情和数字前缀建议） |
| 10 | MED | 标注 | 按规则 1F 反向完整性检查为 `disableDeepLinkRegistration` 添加 "在变更日志中，未在官方 settings 页面" 标注 | ✅ COMPLETE（已在描述中添加标注） |
| 11 | MED | 示例更新 | 将 `defaultShell` 添加到快速参考示例以演示 PowerShell 配置 | ✅ COMPLETE（已将 "defaultShell": "bash" 添加到示例） |

---

## [2026-03-27 06:32 PM PKT] Claude Code v2.1.85

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 缺失环境变量 | 将 `CLAUDE_STREAM_IDLE_TIMEOUT_MS` 添加到 Common Environment Variables 表格 — 流式传输空闲看门狗关闭停滞连接前的超时时间（毫秒）（默认：90000）。已在官方 /en/env-vars 页面确认。在 v2.1.84 添加但上次运行遗漏 | ✅ COMPLETE（已添加到环境变量表格 CLAUDE_CODE_OTEL_HEADERS_HELPER_DEBOUNCE_MS 之后） |
| 2 | HIGH | 版本更新 | 将报告版本徽章从 v2.1.84 更新到 v2.1.85 | ✅ COMPLETE（徽章、标题版本和标题文字已在 Phase 2.6 中更新） |
| 3 | MED | 新环境变量 | 将 `OTEL_LOG_TOOL_DETAILS` 添加到环境变量表格 — 控制 OpenTelemetry 事件中的 `tool_parameters`。仅在 v2.1.85 变更日志中（尚未在官方 env-vars 页面）。添加变更日志来源标注 | ✅ COMPLETE（已添加 "在 v2.1.85 变更日志中，尚未在官方 env-vars 页面" 标注） |
| 4 | MED | 新环境变量（归属） | 确定 `CLAUDE_CODE_MCP_SERVER_NAME` 和 `CLAUDE_CODE_MCP_SERVER_URL` 的归属 — 传递给 MCP `headersHelper` 脚本的环境变量（v2.1.85 变更日志）。可能属于 hooks 仓库而非 settings 报告 | ✅ COMPLETE（已添加到 settings 报告带变更日志标注 — 这些是通过 `env` 键可配置的环境变量，不仅限于 hook） |

---

## [2026-03-28 06:10 PM PKT] Claude Code v2.1.86

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 文件作用域 | 将 `teammateMode` 从 General Settings (settings.json) 移到 Global Config Settings (~/.claude.json)。官方 settings 页面将其列在 "Global config settings" 下 — 添加到 settings.json 会触发 schema 验证错误（规则 1H）。与 v2.1.78 `showTurnDuration` 修复模式相同 | ✅ COMPLETE（已从 General Settings 表格移除，添加到 Global Config Settings 表格 terminalProgressBarEnabled 之后，带 agent-teams 文档链接） |
| 2 | HIGH | 类型 + 标注 | 修复 `disableDeepLinkRegistration`：类型从 `boolean` 改为 `string`（值：`"disable"`），更新描述以匹配官方文档，移除过时的 "（在变更日志中，未在官方 settings 页面）" 标注。现已在官方 settings 页面确认（第 169 行） | ✅ COMPLETE（类型已改为 string，描述已更新以匹配官方文档，变更日志标注已移除） |
| 3 | HIGH | 版本更新 | 将报告版本徽章从 v2.1.85 更新到 v2.1.86 | ✅ COMPLETE（徽章和标题已在 Phase 2.6 中更新） |

---

## [2026-03-31 07:02 PM PKT] Claude Code v2.1.88

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 缺失环境变量 | 将 `CLAUDE_CODE_NO_FLICKER` 添加到 Common Environment Variables 表格 — 启用无闪烁 alt-screen 渲染（v2.1.88）。已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已添加到 CLAUDE_CODE_DISABLE_TERMINAL_TITLE 之后） |
| 2 | HIGH | 缺失环境变量 | 将 `CLAUDE_CODE_SCROLL_SPEED` 和 `CLAUDE_CODE_DISABLE_MOUSE` 添加到 Common Environment Variables 表格 — 全屏 UI 控制。已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已添加到 CLAUDE_CODE_NO_FLICKER 之后） |
| 3 | HIGH | 版本更新 | 将报告版本徽章从 v2.1.86 更新到 v2.1.88 | ✅ COMPLETE（徽章、标题版本和标题文字已在 Phase 2.6 中更新） |
| 4 | HIGH | 失效链接 | 修复来源中的 `https://www.eesel.ai/blog/settings-json-claude-code` — 返回仅 CSS 内容，无可读博文 | ✅ COMPLETE（已从来源部分移除失效链接） |
| 5 | MED | Settings 层级 | 将 `managed-mcp.json` 添加到 file-based managed 传递方式 — 官方 settings 页面将其与 `managed-settings.json` 并列用于 MCP 服务器配置 | ✅ COMPLETE（已添加到 Settings 层级中的 File 传递方式项目符号） |
| 6 | MED | Plugin 来源类型 | 将 `url`、`npm`、`file` marketplace 来源类型标注为 "未在官方文档中 — 未验证"（仅 `github`、`git`、`directory`、`hostPattern`、`settings` 已确认） | ✅ COMPLETE（已为全部 3 种来源类型添加未验证标注） |
| 7 | LOW | 标题计数 | 将标题从 "60+ settings" 更新为匹配任何新增后的实际表格计数 | ❌ INVALID（计数准确 — 60+ settings 和 125 个环境变量，均在声明范围内） |

---

## [2026-04-01 12:32 PM PKT] Claude Code v2.1.89

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 缺失 Setting | 将 `skipDangerousModePermissionPrompt` 添加到 Permission Keys 表格 — boolean，跳过 bypass 模式确认提示。在项目设置中忽略。已在官方 settings 页面确认 | ✅ COMPLETE（已添加到 Permission Keys 表格 disableBypassPermissionsMode 之后） |
| 2 | HIGH | 新 Setting | 将 `showThinkingSummaries` 添加到 General Settings — boolean，默认 `false`。思考摘要默认不再生成；设置为 `true` 以恢复。v2.1.89 变更日志 — 尚未在官方 settings 页面 | ✅ COMPLETE（已添加到 feedbackSurveyRate 之前带变更日志标注） |
| 3 | HIGH | 行为变更 | 更新 `cleanupPeriodDays` 描述 — v2.1.89 变更日志称 `0` 现在会被拒绝并产生验证错误。矛盾：官方 settings 页面仍描述 `0` 为有效值。标记给用户 | ✅ COMPLETE（已更新描述包含变更日志和文档页面之间的矛盾说明） |
| 4 | HIGH | 缺失环境变量 | 添加约 46 个已在官方 /en/env-vars 页面确认的缺失环境变量：`ANTHROPIC_BEDROCK_BASE_URL`、`ANTHROPIC_VERTEX_BASE_URL`、`ANTHROPIC_BETAS`、`ANTHROPIC_VERTEX_PROJECT_ID`、`CLAUDE_CODE_DISABLE_THINKING`、`DISABLE_INTERLEAVED_THINKING`、`ENABLE_PROMPT_CACHING_1H_BEDROCK`、`DISABLE_AUTO_COMPACT`、`DISABLE_COMPACT`、`CLAUDE_CODE_DISABLE_FILE_CHECKPOINTING`、`CLAUDE_CODE_DISABLE_ATTACHMENTS`、`CLAUDE_CODE_DISABLE_CLAUDE_MDS`、`CLAUDE_CODE_GLOB_HIDDEN`、`CLAUDE_CODE_GLOB_NO_IGNORE`、`CLAUDE_CODE_GLOB_TIMEOUT_SECONDS`、`CLAUDE_CODE_DISABLE_OFFICIAL_MARKETPLACE_AUTOINSTALL`、`CLAUDE_CODE_SYNC_PLUGIN_INSTALL`、`CLAUDE_CODE_SYNC_PLUGIN_INSTALL_TIMEOUT_MS`、`CLAUDE_CODE_AUTO_CONNECT_IDE`、`CLAUDE_CODE_IDE_HOST_OVERRIDE`、`CLAUDE_CODE_IDE_SKIP_VALID_CHECK`、`CLAUDE_CODE_MAX_RETRIES`、`API_TIMEOUT_MS`、`CLAUDE_CODE_OTEL_FLUSH_TIMEOUT_MS`、`CLAUDE_CODE_OTEL_SHUTDOWN_TIMEOUT_MS`、`CLAUDE_ENABLE_STREAM_WATCHDOG`、`CLAUDE_CODE_ENABLE_FINE_GRAINED_TOOL_STREAMING`、`CLAUDE_CODE_DEBUG_LOGS_DIR`、`CLAUDE_CODE_DEBUG_LOG_LEVEL`、`CLAUDE_CODE_ACCESSIBILITY`、`CLAUDE_CODE_SYNTAX_HIGHLIGHT`、`CLAUDE_CODE_RESUME_INTERRUPTED_TURN`、`CLAUDE_CODE_MAX_TOOL_USE_CONCURRENCY`、`CLAUDE_CODE_DISABLE_LEGACY_MODEL_REMAP`、`FALLBACK_FOR_ALL_PRIMARY_MODELS`、`CLAUDE_CODE_GIT_BASH_PATH`、`CLAUDE_AUTO_BACKGROUND_TASKS`、`CLAUDE_AGENT_SDK_DISABLE_BUILTIN_AGENTS`、`CLAUDE_AGENT_SDK_MCP_NO_PREFIX`、`DISABLE_DOCTOR_COMMAND`、`DISABLE_LOGIN_COMMAND`、`DISABLE_LOGOUT_COMMAND`、`DISABLE_UPGRADE_COMMAND`、`DISABLE_EXTRA_USAGE_COMMAND`、`DISABLE_INSTALL_GITHUB_APP_COMMAND`、`CLAUDE_CODE_PLUGIN_CACHE_DIR`、`CLAUDE_CODE_SIMPLE` | ✅ COMPLETE（已将全部 46 个环境变量添加到表格中相关变量附近） |
| 5 | HIGH | 版本更新 | 将报告版本徽章从 v2.1.88 更新到 v2.1.89 | ✅ COMPLETE（徽章和标题已在 Phase 2.6 中更新） |
| 6 | MED | 新环境变量 | 将 `MCP_CONNECTION_NONBLOCKING` 添加到环境变量表格 — 在 `-p` 模式下设置为 `true` 以跳过 MCP 连接等待。仅在 v2.1.89 变更日志中，尚未在官方 /en/env-vars 页面 | ✅ COMPLETE（已添加到 CLAUDE_AGENT_SDK_MCP_NO_PREFIX 之后带变更日志标注） |
| 7 | MED | 归属边界 | `CLAUDE_CODE_SIMPLE` 在 CLI 启动标志文件中为仅启动，但官方 /en/env-vars 页面将其列为可配置。协调归属 | ✅ COMPLETE（已添加到 settings 报告环境变量表格；CLI 文件已更新交叉引用到 settings 报告） |
| 8 | MED | 示例更新 | 如果添加了 `showThinkingSummaries`，则更新快速参考示例 | ✅ COMPLETE（已将 showThinkingSummaries: true 添加到示例） |

---

## [2026-04-02 09:24 PM PKT] Claude Code v2.1.90

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 类型 + 描述变更 | 修复 `forceLoginOrgUUID`：类型从 `string` 改为 `string \| string[]`。扩展描述包括数组行为（列出的任何组织均可接受且无需预选）、managed settings 强制执行（如果账户不在列出的组织中则登录失败）以及空数组关闭失败行为 | ✅ COMPLETE（类型已更新为 string \| array，描述已扩展包含数组行为、managed 强制执行、关闭失败语义，示例已更新） |
| 2 | HIGH | 缺失环境变量 | 将 `CLAUDE_CODE_OAUTH_TOKEN`、`CLAUDE_CODE_OAUTH_REFRESH_TOKEN`、`CLAUDE_CODE_OAUTH_SCOPES` 添加到 Common Environment Variables 表格。全部已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已将 3 个 OAuth 环境变量添加到 ANTHROPIC_AUTH_TOKEN 之后） |
| 3 | HIGH | 描述变更 + 标注 | 更新 `showThinkingSummaries`：移除 "（在 v2.1.89 变更日志中，尚未在官方 settings 页面）" 标注 — 现已在官方 settings 页面确认。更新描述以匹配官方："未设置或为 false（交互模式默认值）时，思考块由 API 编辑并显示为折叠存根。编辑仅改变显示内容，不影响模型生成" | ✅ COMPLETE（标注已移除，描述已更新以匹配官方文档） |
| 4 | HIGH | Sandbox 跨合并 | 更新 `sandbox.filesystem.allowWrite` 描述添加 "同时与 `Edit(...)` allow 权限规则中的路径合并"。更新 `denyWrite` 添加 "同时与 `Edit(...)` deny 权限规则中的路径合并"。更新 `denyRead` 添加 "同时与 `Read(...)` deny 权限规则中的路径合并"。已在官方 settings 页面确认 | ✅ COMPLETE（已为全部 3 个文件系统条目添加跨合并行为） |
| 5 | HIGH | 描述变更 | 简化 `cleanupPeriodDays` 描述：移除矛盾说明，与官方文档对齐，现在说 "最小值 1，设置为 0 会被拒绝并产生验证错误"。旧行为不再在官方页面记录 | ✅ COMPLETE（矛盾说明已移除，描述已与官方文档对齐，添加了 --no-session-persistence 替代方案） |
| 6 | HIGH | 版本更新 | 将报告版本徽章从 v2.1.89 更新到 v2.1.90 | ✅ COMPLETE（徽章、标题版本和标题文字已更新） |
| 7 | MED | 新环境变量 | 将 `CLAUDE_CODE_PLUGIN_KEEP_MARKETPLACE_ON_FAILURE` 添加到环境变量表格 — 在 git pull 失败时保留 marketplace 缓存（v2.1.90 变更日志，尚未在官方 /en/env-vars 页面） | ✅ COMPLETE（已添加到 CLAUDE_CODE_SYNC_PLUGIN_INSTALL_TIMEOUT_MS 之后带变更日志标注） |
| 8 | MED | Hook 重定向计数 | 将重定向文字从 "所有 19 个 hook 事件" 更新为 "所有 25 个 hook 事件"（按官方 hooks 页面计数） | ✅ COMPLETE（已在 hooks 重定向部分更新计数） |
| 9 | MED | 归属边界 | `CLAUDE_CODE_TMPDIR` 在官方 /en/env-vars 页面上为可通过 `env` 键配置，但 CLI 启动标志报告将其列为仅启动。协调归属 | ✅ COMPLETE（已添加到 settings 报告环境变量表格；CLI 标志文件已更新交叉引用到 settings 报告） |

---

## [2026-04-03 08:44 PM PKT] Claude Code v2.1.91

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新 Setting | 将 `disableSkillShellExecution` 添加到 General Settings 表格 — boolean，禁用 Skill、自定义斜杠命令和 plugin 命令中的内联 shell 执行。已在 v2.1.91 变更日志中确认。尚未在官方 settings 页面或 JSON schema 中 | ✅ COMPLETE（已添加到 showThinkingSummaries 之后带变更日志标注） |
| 2 | HIGH | 版本更新 | 将报告版本徽章从 v2.1.90 更新到 v2.1.91 | ✅ COMPLETE（徽章和标题已在 Phase 2.6 中更新） |

---

## [2026-04-04 10:48 PM PKT] Claude Code v2.1.92

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新 Setting | 将 `forceRemoteSettingsRefresh` 添加到 General Settings — boolean，仅限 managed，在远程 managed settings 刷新完成前阻止 CLI 启动（关闭失败）。已在官方 settings 页面确认 | ✅ COMPLETE（已添加到 General Settings 表格 feedbackSurveyRate 之前） |
| 2 | HIGH | 缺失环境变量 | 将 `CLAUDE_REMOTE_CONTROL_SESSION_NAME_PREFIX` 添加到 Common Environment Variables 表格 — 自动生成的 Remote Control 会话名称前缀，默认为主机名。已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已添加到 CLAUDE_CODE_ENABLE_TELEMETRY 之前） |
| 3 | MED | 描述变更 | 更新 `disableSkillShellExecution` — 移除 "（在 v2.1.91 变更日志中，尚未在官方 settings 页面）" 标注。现已在官方 settings 页面确认并包含扩展描述 | ✅ COMPLETE（标注已移除，描述已按官方文档扩展） |
| 4 | MED | 描述变更 | 移除 marketplace 来源类型 `url`、`npm` 和 `file` 的 "未在官方文档中 — 未验证" 标签。官方 settings 页面现记录全部 8 种来源类型 | ✅ COMPLETE（未验证标注已移除 — 自 2026-03-31 延续，现已解决） |
| 5 | MED | 描述变更 | 丰富 `cleanupPeriodDays` — 添加 "同时控制启动时自动移除孤立子代理 worktree 的年龄截止"（按官方 settings 页面） | ✅ COMPLETE（已添加 worktree 清理详情） |
| 6 | MED | 描述变更 | 丰富 `disableDeepLinkRegistration` — 添加通过 `%0A` 支持多行提示（按官方 settings 页面） | ✅ COMPLETE（已添加多行提示详情） |
| 7 | MED | 描述变更 | 丰富 `includeGitInstructions` — 更新包含 git status 快照和环境变量优先级（按官方 settings 页面） | ✅ COMPLETE（描述已扩展包含 git status 快照和 CLAUDE_CODE_DISABLE_GIT_INSTRUCTIONS 优先级） |
| 8 | MED | 描述变更 | 丰富 `language` — 添加 "同时设置语音听写语言"（按官方 settings 页面） | ✅ COMPLETE（已添加语音听写详情） |
| 9 | MED | 描述变更 | 丰富 `allowUnsandboxedCommands` — 添加企业策略详情（按官方 settings 页面） | ✅ COMPLETE（已扩展包含关闭失败行为和企业用例） |

---

## [2026-04-08 09:51 PM PKT] Claude Code v2.1.96

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 缺失环境变量 | 将 `CLAUDE_CODE_USE_MANTLE`、`ANTHROPIC_BEDROCK_MANTLE_BASE_URL`、`CLAUDE_CODE_SKIP_MANTLE_AUTH` 添加到 Common Environment Variables 表格 — Bedrock Mantle 端点支持（v2.1.94）。全部已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已添加到相关云提供商变量附近） |
| 2 | HIGH | 默认值变更 | 更新 Effort Level 部分 — API 密钥、Bedrock/Vertex/Foundry、Team 和 Enterprise 用户的默认值从 Medium 改为 High（v2.1.94）。更新表格默认标记和历史说明 | ✅ COMPLETE（表格已将 High 更新为默认值，历史说明已扩展包含 v2.1.94 变更） |
| 3 | HIGH | 版本更新 | 将报告版本徽章从 v2.1.92 更新到 v2.1.96 | ✅ COMPLETE（徽章、标题版本和标题文字已在 Phase 2.6 中更新） |
| 4 | MED | 过时标注 | 移除 `CLAUDE_CODE_PLUGIN_KEEP_MARKETPLACE_ON_FAILURE` 的 "（在 v2.1.90 变更日志中，尚未在官方 env-vars 页面）" — 现已在官方 /en/env-vars 页面确认。更新描述以匹配官方措辞 | ✅ COMPLETE（标注已移除，描述已按官方文档更新） |
| 5 | MED | 描述变更 | 更新 `CLAUDE_CODE_GLOB_HIDDEN` 描述以匹配官方："设置为 `false` 以从 Glob 结果中排除 dotfile。默认包含。不影响 `@` 文件自动补全、`ls`、Grep 或 Read" | ✅ COMPLETE（描述已按官方 env-vars 页面重写） |

---

## [2026-04-09 11:39 PM PKT] Claude Code v2.1.97

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新 Setting | 将 `sandbox.network.allowMachLookup` 添加到 Sandbox Settings 表格 — 数组，仅 macOS，XPC/Mach 服务名称支持尾部 `*` 通配符。已在官方 settings 页面确认 | ✅ COMPLETE（已添加到 sandbox network 子键中 allowManagedDomainsOnly 之后） |
| 2 | HIGH | 显示和用户体验 | 将 `refreshInterval` 字段添加到 Status Line Configuration 部分 — 可选，每 N 秒重新运行命令，最小值 1（v2.1.97）。已在官方状态行文档确认 | ✅ COMPLETE（已添加到配置表格包含 `padding` 字段，更新了 JSON 示例） |
| 3 | HIGH | 显示和用户体验 | 将 Status Line Input Fields 表格从 9 个字段扩展到 30+ 个字段以匹配官方状态行文档。添加 `model.*`、`workspace.*`、`cost.*`、`session_id`、`session_name`、`transcript_path`、`version`、`output_style.name`、`vim.mode`、`agent.name`、`worktree.*` 字段 | ✅ COMPLETE（已按官方状态行文档从 9 个扩展到 30 个字段） |
| 4 | HIGH | 版本更新 | 将报告版本徽章从 v2.1.96 更新到 v2.1.97 | ✅ COMPLETE（徽章和标题已在 Phase 2.6 中更新） |
| 5 | MED | 字段命名 | 修复 `current_usage` → `context_window.current_usage`（在 Status Line Input Fields 表格中） | ✅ COMPLETE（已重命名为完整路径并扩展描述） |
| 6 | MED | 归属边界 | 将 `CCR_FORCE_BUNDLE` 添加到 `claude-cli-startup-flags.md` — 仅启动变量用于 `claude --remote` 打包。在官方 /en/env-vars 页面但未在任一文件中 | ✅ COMPLETE（已添加到 CLI 启动标志环境变量表格） |
| 7 | MED | 描述变更 | 更新 `CLAUDE_CODE_GLOB_NO_IGNORE` 描述以匹配官方："设置为 `false` 以使 Glob 工具遵守 `.gitignore` 模式。默认情况下，Glob 返回所有匹配文件包括被 gitignore 的。不影响 `@` 文件自动补全" | ✅ COMPLETE（描述已按官方 env-vars 页面重写） |
| 8 | MED | 描述变更 | 更新 `editorMode` 描述 — 移除过时的 `/vim` 引用（在 v2.1.94 中移除），将配置标签从 "Key binding mode" 改为 "Editor mode"（按官方文档） | ✅ COMPLETE（已移除 /vim 引用，配置标签已更新） |

---

## [2026-04-13 08:10 PM PKT] Claude Code v2.1.101

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 缺失环境变量 | 将 `CLAUDE_CODE_CERT_STORE` 添加到 Common Environment Variables 表格 — 逗号分隔的 TLS CA 证书来源（`bundled`、`system`）。默认：`bundled,system`。系统证书存储需要原生二进制。v2.1.101。已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已添加到 CLAUDE_CODE_CLIENT_KEY_PASSPHRASE 之后） |
| 2 | HIGH | 缺失环境变量 | 将 `CLAUDE_CODE_PERFORCE_MODE` 添加到 Common Environment Variables 表格 — 设置为 `1` 以启用 Perforce 感知的写保护。如果目标文件缺少 owner-write 位，Edit/Write/NotebookEdit 会失败并提示 `p4 edit`。v2.1.98。已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已添加到 CLAUDE_CODE_SCRIPT_CAPS 之后） |
| 3 | HIGH | 缺失环境变量 | 将 `CLAUDE_CODE_SCRIPT_CAPS` 添加到 Common Environment Variables 表格 — 当 `CLAUDE_CODE_SUBPROCESS_ENV_SCRUB` 设置时，限制每个会话脚本调用次数的 JSON 对象。键是匹配命令文本的子字符串；值是整数调用限制。已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已添加到 CLAUDE_CODE_SUBPROCESS_ENV_SCRUB 之后） |
| 4 | HIGH | 版本更新 | 将报告版本徽章从 v2.1.97 更新到 v2.1.101 | ✅ COMPLETE（徽章、标题版本和标题文字已在 Phase 2.6 中更新） |
| 5 | MED | 描述变更 | 更新 `disableSkillShellExecution` — 添加 ` ```! `（三反引号 shell）块语法和 "来自 user、project、plugin 或 additional-directory 来源" 限定词（按官方 settings 页面） | ✅ COMPLETE（描述已按官方文档扩展） |
| 6 | MED | 归属边界 | 将 `DISABLE_AUTOUPDATER` 添加到 settings 报告环境变量表格 — 在官方 /en/env-vars 页面上为可通过 `env` 键配置，当前仅在 CLI 启动标志文件中。添加到 CLI 标志文件的交叉引用 | ✅ COMPLETE（已添加到 settings 报告 DISABLE_TELEMETRY 之前；CLI 标志文件已更新交叉引用） |

---

## [2026-04-14 11:22 PM PKT] Claude Code v2.1.107

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新 Setting | 将 `viewMode` 添加到 General Settings 表格 — string，值 `"default"`、`"verbose"`、`"focus"`。启动时的默认转录视图模式，覆盖粘性 Ctrl+O 选择。已在官方 settings 页面确认 | ✅ COMPLETE（已添加到 General Settings 中 showClearContextOnPlanAccept 之后） |
| 2 | HIGH | 缺失环境变量 | 添加 5 个已在官方 /en/env-vars 页面确认的缺失环境变量：`ANTHROPIC_CUSTOM_MODEL_OPTION_SUPPORTED_CAPABILITIES`、`CLAUDE_CODE_DISABLE_VIRTUAL_SCROLL`、`CLAUDE_ENABLE_BYTE_WATCHDOG`、`CLAUDE_CODE_MAX_CONTEXT_TOKENS`、`CLAUDE_CODE_SKIP_PROMPT_HISTORY` | ✅ COMPLETE（已添加到环境变量表格中相关变量附近） |
| 3 | HIGH | 描述变更 | 更新 `disableAllHooks` 描述 — 添加 "及任何自定义状态行"（按官方 settings 页面第 180 行） | ✅ COMPLETE（已在 hooks 重定向部分内联更新） |
| 4 | HIGH | 默认值变更 | 修复 Global Config Settings 表格中 `teammateMode` 默认值从 `"in-process"` 到 `"auto"`。官方文档描述 `auto` 为主要行为。在 v2.1.86 文件作用域移动中回归 | ✅ COMPLETE（默认值已更新为 "auto" — 自 2026-03-07 延续，v2.1.86 移动的回归） |
| 5 | MED | 描述变更 | 更新 `CLAUDE_STREAM_IDLE_TIMEOUT_MS` 描述 — 区分字节看门狗（默认/最小 300000ms）和事件看门狗（默认 90000ms）。按官方 /en/env-vars 页面 | ✅ COMPLETE（描述已扩展包含双看门狗详情和 CLAUDE_ENABLE_BYTE_WATCHDOG 交叉引用） |
| 6 | MED | 标注修复 | 移除 `CLAUDE_CODE_GIT_BASH_PATH` 的 "（仅启动）" — 官方 /en/env-vars 页面将其列为环境可配置 | ✅ COMPLETE（描述已按官方文档重写，仅启动标注已移除） |
| 7 | MED | 示例更新 | 将 `viewMode` 添加到快速参考示例 `showThinkingSummaries` 之后 | ✅ COMPLETE（已将 "viewMode": "default" 添加到示例） |
| 8 | MED | 过时标注 | `OTEL_LOG_TOOL_DETAILS` 仍标记为 "在 v2.1.85 变更日志中，尚未在官方 env-vars 页面" — 确认在 10+ 版本和 7 次连续运行后仍未出现在官方页面 | ✋ ON HOLD（标注准确 — 保持现状待官方文档更新） |
| 7 | MED | 归属边界 | 将 `CCR_FORCE_BUNDLE` 添加到 settings 报告环境变量表格 — 在官方 /en/env-vars 页面上为可通过 `env` 键配置，当前仅在 CLI 启动标志文件中。添加到 CLI 标志文件的交叉引用 | ✅ COMPLETE（已添加到 settings 报告 CLAUDE_CODE_GIT_BASH_PATH 之前；CLI 标志文件已更新交叉引用） |

---

## [2026-04-16 08:25 PM PKT] Claude Code v2.1.110

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 缺失 Setting | 将 `minimumVersion` 添加到 General Settings 表格 — string，防止自动更新器降级到特定版本以下。已在官方 settings 页面确认 | ✅ COMPLETE（已添加到 General Settings 表格 autoUpdatesChannel 之后） |
| 2 | HIGH | 缺失环境变量 | 将 `CLAUDE_CODE_TMUX_TRUECOLOR` 添加到 Common Environment Variables 表格 — 设置为 `1` 以在 tmux 内允许 24 位真彩色输出。已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已添加到 CLAUDE_CODE_NO_FLICKER 之前） |
| 3 | HIGH | 缺失环境变量 | 将 `CLAUDE_CODE_REMOTE` 添加到 Common Environment Variables 表格 — 只读，在云会话中设置为 `true`。已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已添加到 CLAUDE_REMOTE_CONTROL_SESSION_NAME_PREFIX 之前） |
| 4 | HIGH | 缺失环境变量 | 将 `CLAUDE_CODE_REMOTE_SESSION_ID` 添加到 Common Environment Variables 表格 — 只读，云会话 ID。已在官方 /en/env-vars 页面确认 | ✅ COMPLETE（已添加到 CLAUDE_REMOTE_CONTROL_SESSION_NAME_PREFIX 之前） |
| 5 | HIGH | 反向环境变量检查 | 将 `ENABLE_PROMPT_CACHING_1H_BEDROCK` 标记为 "未在官方文档中 — 未验证"。不再出现在官方 /en/env-vars 页面。按规则 5D | ✅ COMPLETE（已添加未验证标注和弃用说明） |
| 6 | MED | 新 Setting（变更日志） | 将 `autoScrollEnabled` 添加到 General Settings — boolean，在全屏模式下禁用对话自动滚动。仅在 v2.1.110 变更日志中，尚未在官方 settings 页面 | ✅ COMPLETE（已添加到 feedbackSurveyRate 之前带变更日志标注） |
| 7 | MED | 新 Setting（变更日志） | 将 `tui` 添加到 General Settings — 无闪烁渲染模式设置（`/tui fullscreen`）。仅在 v2.1.110 变更日志中，尚未在官方 settings 页面 | ✅ COMPLETE（已添加到 feedbackSurveyRate 之前带变更日志标注） |
| 8 | MED | 新环境变量（变更日志） | 将 `ENABLE_PROMPT_CACHING_1H` 添加到环境变量表格 — 1 小时 prompt cache TTL（替代已弃用的 `ENABLE_PROMPT_CACHING_1H_BEDROCK`）。仅在 v2.1.108 变更日志中，尚未在官方 /en/env-vars 页面 | ✅ COMPLETE（已添加到 DISABLE_PROMPT_CACHING 之前带变更日志标注） |
| 9 | MED | 新环境变量（变更日志） | 将 `FORCE_PROMPT_CACHING_5M` 添加到环境变量表格 — 强制 5 分钟 TTL。仅在 v2.1.108 变更日志中，尚未在官方 /en/env-vars 页面 | ✅ COMPLETE（已添加到 DISABLE_PROMPT_CACHING 之前带变更日志标注） |
| 10 | MED | Effort Level 表格 | 将 `Max` 行添加到 Effort Level 表格 — 仅 Opus 4.6，已在环境变量中记录但缺失于表格 | ✅ COMPLETE（已作为 Effort Level 表格首行添加） |
| 11 | MED | Sandbox 描述 | 添加平台特定说明：`allowUnixSockets`（仅 macOS）、`allowAllUnixSockets`（Linux/WSL2 详情）、`enableWeakerNestedSandbox`（仅 Linux/WSL2） | ✅ COMPLETE（全部 3 个描述已按官方文档更新平台特定说明） |
| 12 | LOW | 仅变更日志环境变量 | 考虑添加 `CLAUDE_CODE_ENABLE_AWAY_SUMMARY`（v2.1.108）、`OTEL_LOG_USER_PROMPTS`（v2.1.101）、`OTEL_LOG_TOOL_CONTENT`（v2.1.101）— 全部仅在变更日志中，未在官方 env-vars 页面。按规则 8A 推迟至官方文档确认 | ✋ ON HOLD（已推迟 — 仅变更日志，未经官方文档确认） |
