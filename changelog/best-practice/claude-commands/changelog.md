# Commands 报告 — 变更日志历史

## 状态图例

| 状态 | 含义 |
|--------|---------|
| ✅ `COMPLETE (原因)` | 已采取操作并成功解决 |
| ❌ `INVALID (原因)` | 发现不正确、不适用或属于设计意图 |
| ✋ `ON HOLD (原因)` | 操作已推迟 — 等待外部依赖或用户决定 |

---

## [2026-03-13 04:23 PM PKT] Claude Code v2.1.74

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新字段 | 在 frontmatter 表中添加 `name` — Skill 的显示名称 | ❌ INVALID (仅限 Skill 的字段，不适用于 Command frontmatter) |
| 2 | HIGH | 新字段 | 在 frontmatter 表中添加 `disable-model-invocation` — 防止自动加载 | ❌ INVALID (仅限 Skill 的字段，不适用于 Command frontmatter) |
| 3 | HIGH | 新字段 | 在 frontmatter 表中添加 `user-invocable` — 从 `/` 菜单中隐藏 | ❌ INVALID (仅限 Skill 的字段，不适用于 Command frontmatter) |
| 4 | HIGH | 新字段 | 在 frontmatter 表中添加 `context` — fork 以在子代理上下文中运行 | ❌ INVALID (仅限 Skill 的字段，不适用于 Command frontmatter) |
| 5 | HIGH | 新字段 | 在 frontmatter 表中添加 `agent` — `context: fork` 的子代理类型 | ❌ INVALID (仅限 Skill 的字段，不适用于 Command frontmatter) |
| 6 | HIGH | 新字段 | 在 frontmatter 表中添加 `hooks` — 作用域限定于 Skill 的生命周期 Hook | ❌ INVALID (仅限 Skill 的字段，不适用于 Command frontmatter) |
| 7 | HIGH | 新 Command | 添加 `/btw <question>` — 快速提问而不添加到对话中 | ✅ COMPLETE (已添加为 Session 标签中的 #53) |
| 8 | HIGH | 新 Command | 添加 `/hooks` — 管理工具事件的 Hook 配置 | ✅ COMPLETE (已添加为 Extensions 标签中的 #30) |
| 9 | HIGH | 新 Command | 添加 `/insights` — 生成会话分析报告 | ✅ COMPLETE (已添加为 Context 标签中的 #17) |
| 10 | HIGH | 新 Command | 添加 `/plugin` — 管理 Claude Code 插件 | ✅ COMPLETE (已添加为 Extensions 标签中的 #33) |
| 11 | HIGH | 新 Command | 添加 `/skills` — 列出可用的 Skill | ✅ COMPLETE (已添加为 Extensions 标签中的 #35) |
| 12 | HIGH | 新 Command | 添加 `/upgrade` — 打开升级页面以切换套餐层级 | ✅ COMPLETE (已添加为 Auth 标签中的 #3) |
| 13 | HIGH | 已移除 Command | 移除 `/output-style` — 在 v2.1.73 中已弃用，请改用 `/config` | ✅ COMPLETE (已从 Config 标签中移除) |
| 14 | HIGH | 已移除 Command | 移除 `/bug` 行 — 现已作为 `/feedback` 的别名列出 | ✅ COMPLETE (已移除该行，在 /feedback 描述中添加了 "Alias: /bug") |
| 15 | HIGH | 描述变更 | 更新 `/passes` — 用途从审查轮次改为推荐分享 | ✅ COMPLETE (已更新描述，保留在 Model 标签中) |
| 16 | HIGH | 描述变更 | 更新 `/review` — 已弃用，被 `code-review` marketplace 插件取代 | ✅ COMPLETE (已更新 Project 标签中的描述) |
| 17 | MED | 描述变更 | 更新 `/stickers` — 从 UI 贴纸包改为订购实体贴纸 | ✅ COMPLETE (已更新 Config 标签中的描述) |

---

## [2026-03-15 12:50 PM PKT] Claude Code v2.1.76

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新 Command | 在 Config 标签中添加 `/color [color\|default]` — 设置当前会话的提示栏颜色 | ✅ COMPLETE (已添加为 Config 标签中的 #4) |
| 2 | HIGH | 新 Command | 在 Model 标签中添加 `/effort [low\|medium\|high\|max\|auto]` — 设置模型努力程度 | ✅ COMPLETE (已添加为 Model 标签中的 #38) |
| 3 | MED | 描述变更 | 更新 `/status` — 现为 "Open the Settings interface (Status tab)" 而非 "Show a concise session status summary" | ✅ COMPLETE (已更新 Context 标签中 #20 的描述) |
| 4 | MED | 描述变更 | 更新 `/desktop` — 现为 "Continue the current session in the Claude Code Desktop app. macOS and Windows only." | ✅ COMPLETE (已更新 Remote 标签中 #49 的描述) |
| 5 | LOW | 参数变更 | 更新 `/init` — 官方文档移除了 `[prompt]` 参数提示 | ✅ COMPLETE (已移除 Project 标签中 #45 的 [prompt] 提示) |

---

## [2026-03-17 12:45 PM PKT] Claude Code v2.1.77

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新别名 | 在 `/fork` 条目中添加 `Alias: /branch` (v2.1.77 将 fork 重命名为 branch) | ✅ COMPLETE (已在 Session 标签 #59 的 /fork 中添加 "Alias: /branch") |
| 2 | HIGH | 新别名 | 为 8 个 Command 添加别名: `/clear` (+/reset, /new), `/config` (+/settings), `/desktop` (+/app), `/exit` (+/quit), `/rewind` (+/checkpoint), `/resume` (+/continue), `/remote-control` (+/rc), `/mobile` (+/ios, /android) | ✅ COMPLETE (已在全部 8 个 Command 描述中添加别名标注) |
| 3 | MED | 描述变更 | 更新 `/diff` — "Open an interactive diff viewer showing uncommitted changes and per-turn diffs" | ✅ COMPLETE (已更新 Project 标签中 #44 的描述) |
| 4 | MED | 描述变更 | 更新 `/memory` — "Edit CLAUDE.md memory files, enable or disable auto-memory, and view auto-memory entries" | ✅ COMPLETE (已更新 Memory 标签中 #37 的描述) |
| 5 | MED | 描述变更 | 更新 `/copy` — "Copy the last assistant response to clipboard. Shows interactive picker for code blocks" | ✅ COMPLETE (已更新 Export 标签中 #27 的描述) |
| 6 | MED | 描述变更 | 更新 `/mobile` — "Show QR code to download the Claude mobile app" | ✅ COMPLETE (已更新 Remote 标签中 #52 的描述和别名) |
| 7 | MED | 描述变更 | 更新 `/remote-control` — "Make this session available for remote control from claude.ai" | ✅ COMPLETE (已更新 Remote 标签中 #53 的描述和别名) |
| 8 | LOW | Frontmatter 范围 | 6 个仅限 Skill 的字段仍未收录在报告中（属于有意的范围界定） | ❌ INVALID (仅限 Skill 的字段 — 与 v2.1.74 运行的判定相同) |

---

## [2026-03-18 11:38 PM PKT] Claude Code v2.1.78

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新 Command | 在 Config 标签中添加 `/voice` — 切换按键说话语音输入 | ✅ COMPLETE (已添加为 Config 标签中的 #15) |
| 2 | HIGH | 别名互换 | 将 `/fork` → `/branch` 设为主命令，`/fork` 设为别名 | ✅ COMPLETE (已在 Session 标签 #56 中互换为 `/branch`，按字母顺序重新排列) |
| 3 | MED | 新别名 | 为 `/permissions` 添加 `/allowed-tools` 别名 | ✅ COMPLETE (已在 Config 标签 #7 中添加别名) |
| 4 | MED | 新参数 | 为 `/copy` 添加 `[N]` 参数语法 | ✅ COMPLETE (已在 Export 标签 #28 中更新为 `/copy [N]`) |
| 5 | LOW | Frontmatter 范围 | 6 个仅限 Skill 的字段未收录在报告中（属于有意的范围界定） | ❌ INVALID (仅限 Skill 的字段 — 与 v2.1.74 和 v2.1.77 运行的判定相同) |

---

## [2026-03-19 11:54 AM PKT] Claude Code v2.1.79

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | LOW | Frontmatter 范围 | 6 个仅限 Skill 的字段未收录在报告中（属于有意的范围界定） | ❌ INVALID (仅限 Skill 的字段 — 与 v2.1.74、v2.1.77 和 v2.1.78 运行的判定相同) |

---

## [2026-03-20 08:33 AM PKT] Claude Code v2.1.80

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | MED | 新字段 | 在 frontmatter 表中添加 `effort` — 调用 Command 时覆盖模型努力程度 (v2.1.80) | ✅ COMPLETE (已添加为第 5 个字段，后在添加完整字段集时重新定位为第 8 个) |
| 2 | HIGH | QA 修正 | 添加 6 个缺失字段 (`name`, `disable-model-invocation`, `user-invocable`, `context`, `agent`, `hooks`) — 官方文档声明 Command 支持与 Skill "相同的 frontmatter"；之前的 INVALID 判定 (v2.1.74–v2.1.79) 是不正确的 | ✅ COMPLETE (已添加全部 6 个字段，计数从 5 更新为 11，字段顺序与官方文档一致) |
| 3 | HIGH | 跨报告修复 | 在 Skill 报告 (`claude-skills.md`) 中添加 `effort` — 该字段在那里也缺失 | ✅ COMPLETE (已在 Skill 报告中添加为第 8 个字段，计数从 10 更新为 11) |

---

## [2026-03-21 09:08 PM PKT] Claude Code v2.1.81

无优先操作项 — 报告与官方文档完全同步 (11 个 frontmatter 字段，63 个内置 Command)。

---

## [2026-03-23 09:48 PM PKT] Claude Code v2.1.81

无优先操作项 — 报告与官方文档完全同步 (11 个 frontmatter 字段，63 个内置 Command)。

---

## [2026-03-25 08:07 PM PKT] Claude Code v2.1.83

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新 Command | 在 Remote 标签中添加 `/schedule [description]` — 创建、更新、列出或运行 Cloud 计划任务 | ✅ COMPLETE (已添加为 Remote 标签中的 #56，计数从 63 更新为 64) |

---

## [2026-03-26 01:01 PM PKT] Claude Code v2.1.84

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新字段 | 在 frontmatter 表中添加 `shell` — `!command` 块的 shell 类型 (`bash` 或 `powershell`) | ✅ COMPLETE (已添加为第 12 个字段，位于 `hooks` 之前，计数从 11 更新为 12) |
| 2 | LOW | 参数变更 | 为 `/fast` Command 添加 `[on\|off]` 参数提示 | ✅ COMPLETE (已在 Model 标签 #40 中将 `/fast` 更新为 `/fast [on\|off]`) |

---

## [2026-03-27 06:25 PM PKT] Claude Code v2.1.85

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新字段 | 在 frontmatter 表中添加 `paths` — 限制 Skill 何时被激活的 glob 模式 | ✅ COMPLETE (已添加为 `user-invocable` 之后的第 6 个字段，计数从 12 更新为 13) |

---

## [2026-03-28 06:05 PM PKT] Claude Code v2.1.86

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | MED | 参数变更 | 更新 `/add-dir` — 根据官方文档添加 `<path>` 必需参数提示 | ✅ COMPLETE (已在 Project 标签 #44 中更新) |
| 2 | MED | 参数变更 | 更新 `/branch` — 根据官方文档添加 `[name]` 可选参数提示 | ✅ COMPLETE (已在 Session 标签 #57 中更新) |
| 3 | MED | 参数变更 | 更新 `/model` — 根据官方文档添加 `[model]` 可选参数提示 | ✅ COMPLETE (已在 Model 标签 #41 中更新) |
| 4 | MED | 参数变更 | 更新 `/plan` — 根据官方文档添加 `[description]` 可选参数提示 | ✅ COMPLETE (已在 Model 标签 #43 中更新) |
| 5 | MED | 参数变更 | 更新 `/pr-comments` — 根据官方文档添加 `[PR]` 可选参数提示 | ✅ COMPLETE (已在 Project 标签 #47 中更新) |
| 6 | MED | 参数变更 | 更新 `/passes` — 移除 `[number]` 参数提示（官方文档中没有） | ✅ COMPLETE (已在 Model 标签 #42 中更新) |
| 7 | MED | 参数变更 | 更新 `/rename` — 根据官方文档从 `<name>`（必需）改为 `[name]`（可选） | ✅ COMPLETE (已在 Session 标签 #62 中更新) |
| 8 | LOW | 参数变更 | 更新 `/compact` — 根据官方文档将参数标签从 `[prompt]` 改为 `[instructions]` | ✅ COMPLETE (已在 Session 标签 #60 中更新) |
| 9 | LOW | 参数变更 | 更新 `/feedback` — 根据官方文档将参数标签从 `[description]` 改为 `[report]` | ✅ COMPLETE (已在 Debug 标签 #24 中更新) |

---

## [2026-03-31 06:55 PM PKT] Claude Code v2.1.88

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | MED | 描述同步 | 同步全部 43 个 Command 描述以匹配官方文档 — 行为澄清 (`/vim` 切换, `/sandbox` 切换, `/hooks` 查看)，扩展详情 (`/effort` 持久性, `/copy` SSH 写入, `/model` 努力程度箭头)，以及 Auth、Config、Context、Debug、Export、Extensions、Model、Project、Remote 和 Session 标签的措辞对齐 | ✅ COMPLETE (全部 64 个描述现已与 code.claude.com/docs/en/commands 的官方文档匹配) |

---

## [2026-04-01 12:26 PM PKT] Claude Code v2.1.89

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | LOW | 描述变更 | 更新 `/init` — 官方文档现使用 `CLAUDE_CODE_NEW_INIT=1` 而非 `=true` | ✅ COMPLETE (已将环境变量值从 `=true` 更新为 `=1` 以匹配官方文档) |

---

## [2026-04-02 09:14 PM PKT] Claude Code v2.1.90

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | MED | 描述变更 | 更新 `/permissions` — 官方文档扩展为描述交互式对话框，包含范围规则、目录管理和自动模式拒绝审查 | ✅ COMPLETE (已更新描述以匹配官方文档) |
| 2 | MED | 新别名 | 根据官方文档为 `/tasks` Command 添加 `/bashes` 别名 | ✅ COMPLETE (已在 Debug 标签 #27 的 /tasks 中添加 "Alias: /bashes") |

---

## [2026-04-03 08:34 PM PKT] Claude Code v2.1.91

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新 Command | 在 Config 标签中添加 `/powerup` — 通过带动画演示的快速交互课程探索 Claude Code 功能 | ✅ COMPLETE (已添加为 Debug 标签中的 #26 — 在 v2.1.92 运行中解决) |

---

## [2026-04-04 10:40 PM PKT] Claude Code v2.1.92

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新 Command | 在 Debug 标签中添加 `/powerup` — 通过带动画演示的快速交互课程探索 Claude Code 功能 | ✅ COMPLETE (已添加为 Debug 标签中的 #26，从 v2.1.91 延续) |
| 2 | HIGH | 新 Command | 在 Auth 标签中添加 `/setup-bedrock` — 通过交互式向导配置 Amazon Bedrock 认证、区域和模型固定 | ✅ COMPLETE (已添加为 Auth 标签中的 #3) |
| 3 | HIGH | 新 Command | 在 Model 标签中添加 `/ultraplan <prompt>` — 在 ultraplan 会话中起草计划，在浏览器中审查，然后远程执行或发回 | ✅ COMPLETE (已添加为 Model 标签中的 #45) |
| 4 | HIGH | 已移除 Command | 从 Config 标签中移除 `/vim` — 在 v2.1.92 中移除 (max-version: 2.1.91)，请改用 `/config` Editor mode | ✅ COMPLETE (已从 Config 标签中移除) |
| 5 | HIGH | 已移除 Command | 从 Project 标签中移除 `/pr-comments [PR]` — 在 v2.1.91 中移除 (max-version: 2.1.90)，请直接询问 Claude | ✅ COMPLETE (已从 Project 标签中移除) |
| 6 | MED | 描述变更 | 更新 `/release-notes` — 现为 "View the changelog in an interactive version picker. Select a specific version to see its release notes, or choose to show all versions." | ✅ COMPLETE (已更新 Debug 标签 #27 的描述) |

---

## [2026-04-08 09:35 PM PKT] Claude Code v2.1.96

无优先操作项 — 报告与官方文档完全同步 (13 个 frontmatter 字段，65 个内置 Command)。

---

## [2026-04-09 11:31 PM PKT] Claude Code v2.1.97

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新 Command | 在 Remote 标签中添加 `/autofix-pr [prompt]` — 生成一个 Web 会话，监视当前分支的 PR，并在 CI 失败或审查者留下评论时推送修复 | ✅ COMPLETE (已添加为 Remote 标签中的 #51，计数从 65 更新为 68) |
| 2 | HIGH | 新 Command | 在 Remote 标签中添加 `/teleport` — 将 Web 上的 Claude Code 会话拉入本终端。Alias: `/tp` | ✅ COMPLETE (已添加为 Remote 标签中的 #59) |
| 3 | HIGH | 新 Command | 在 Remote 标签中添加 `/web-setup` — 使用本地 `gh` CLI 凭证将 GitHub 账户连接到 Web 上的 Claude Code | ✅ COMPLETE (已添加为 Remote 标签中的 #60) |
| 4 | MED | 描述变更 | 更新 `/add-dir` — 官方文档现包含关于 `.claude/` 配置不会从添加的目录中被发现的注意事项 | ✅ COMPLETE (已更新 Project 标签 #46 的描述) |

---

## [2026-04-13 08:00 PM PKT] Claude Code v2.1.101

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新 Command | 在 Auth 标签中添加 `/setup-vertex` — 通过交互式向导配置 Google Vertex AI 认证、项目、区域和模型固定。仅在设置 `CLAUDE_CODE_USE_VERTEX=1` 时可见 | ✅ COMPLETE (已添加为 Auth 标签中的 #4，计数从 68 更新为 69) |

---

## [2026-04-14 11:13 PM PKT] Claude Code v2.1.107

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新字段 | 在 frontmatter 表中添加 `when_to_use` — Claude 何时应调用 Skill 的附加上下文，附加到列表中 `description` 之后 (计数 13 → 14) | ✅ COMPLETE (已添加在 `description` 字段之后，计数从 13 更新为 14) |
| 2 | HIGH | 新 Command | 在 Project 标签中添加 `/team-onboarding` — 从 Claude Code 使用历史生成团队入职指南 (计数 69 → 70) | ✅ COMPLETE (已添加为 Project 标签中的 #52，计数从 69 更新为 70) |
| 3 | MED | 范围决定 | 官方文档统一表中列出的 5 个捆绑 Skill (`/batch`, `/claude-api`, `/debug`, `/loop`, `/simplify`) 按报告当前范围声明排除 | ❌ INVALID (用户选择将报告范围限定为仅内置 Command — 保留免责声明) |
| 4 | MED | 描述变更 | 更新 `/doctor` — 添加 "Press `f` to have Claude fix any reported issues" | ✅ COMPLETE (在描述中添加了状态图标和 `f` 键修复详情) |
| 5 | MED | 描述变更 | 更新 `/schedule` — 术语从 "Cloud scheduled tasks" 改为 "routines" | ✅ COMPLETE (已更新描述中的术语) |

---

## [2026-04-16 08:20 PM PKT] Claude Code v2.1.110

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | MED | 新别名 | 为 `/rewind` 条目添加 `/undo` 别名 — 在 v2.1.108 中添加 | ✅ COMPLETE (已在 Session 标签 #70 中与现有 `/checkpoint` 别名一起添加 `/undo`) |
