# 命令最佳实践

![Last Updated](https://img.shields.io/badge/Last_Updated-Apr%2016%2C%202026%208%3A20%20PM%20PKT-white?style=flat&labelColor=555) ![Version](https://img.shields.io/badge/Claude_Code-v2.1.110-blue?style=flat&labelColor=555)<br>
[![Implemented](https://img.shields.io/badge/Implemented-2ea44f?style=flat)](../implementation/claude-commands-implementation.md)

Claude Code 命令 — 前置元数据字段和官方内置斜杠命令。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code 最佳实践</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## 前置元数据字段 (14)

| 字段 | 类型 | 必填 | 描述 |
|------|------|------|------|
| `name` | string | 否 | 显示名称和 `/斜杠命令` 标识符。省略时默认为目录名 |
| `description` | string | 推荐 | 命令的功能描述。显示在自动补全中，也被 Claude 用于自动发现 |
| `when_to_use` | string | 否 | Claude 何时应调用该技能的额外上下文 — 触发短语或请求示例。追加到 `description` 中，计入 1,536 字符上限 |
| `argument-hint` | string | 否 | 自动补全时显示的提示（例如 `[issue-number]`、`[filename]`） |
| `disable-model-invocation` | boolean | 否 | 设置为 `true` 以防止 Claude 自动调用此命令 |
| `user-invocable` | boolean | 否 | 设置为 `false` 以从 `/` 菜单中隐藏 — 命令仅作为背景知识 |
| `paths` | string/list | 否 | 限制技能何时激活的 glob 模式。接受逗号分隔的字符串或 YAML 列表。设置后，Claude 仅在处理匹配模式的文件时自动加载该技能 |
| `allowed-tools` | string | 否 | 此命令激活时无需权限提示即可使用的工具 |
| `model` | string | 否 | 此命令运行时使用的模型（例如 `haiku`、`sonnet`、`opus`） |
| `effort` | string | 否 | 调用时覆盖模型努力程度（`low`、`medium`、`high`、`max`） |
| `context` | string | 否 | 设置为 `fork` 以在隔离的子代理上下文中运行命令 |
| `agent` | string | 否 | 当设置 `context: fork` 时的子代理类型（默认：`general-purpose`） |
| `shell` | string | 否 | `` !`command` `` 块的 shell — 接受 `bash`（默认）或 `powershell`。需要 `CLAUDE_CODE_USE_POWERSHELL_TOOL=1` |
| `hooks` | object | 否 | 作用域限于此命令的生命周期钩子 |

---

## ![Official](../!/tags/official.svg) **(70)**

| # | 命令 | 标签 | 描述 |
|---|------|------|------|
| 1 | `/login` | ![Auth](https://img.shields.io/badge/Auth-2980B9?style=flat) | 登录 Anthropic 账户 |
| 2 | `/logout` | ![Auth](https://img.shields.io/badge/Auth-2980B9?style=flat) | 退出 Anthropic 账户 |
| 3 | `/setup-bedrock` | ![Auth](https://img.shields.io/badge/Auth-2980B9?style=flat) | 通过交互式向导配置 Amazon Bedrock 身份验证、区域和模型固定。仅在设置 `CLAUDE_CODE_USE_BEDROCK=1` 时可见。首次 Bedrock 用户也可从登录界面访问此向导 |
| 4 | `/setup-vertex` | ![Auth](https://img.shields.io/badge/Auth-2980B9?style=flat) | 通过交互式向导配置 Google Vertex AI 身份验证、项目、区域和模型固定。仅在设置 `CLAUDE_CODE_USE_VERTEX=1` 时可见。首次 Vertex AI 用户也可从登录界面访问此向导 |
| 5 | `/upgrade` | ![Auth](https://img.shields.io/badge/Auth-2980B9?style=flat) | 打开升级页面切换到更高级别的计划 |
| 6 | `/color [color\|default]` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 设置当前会话的提示栏颜色。可用颜色：`red`、`blue`、`green`、`yellow`、`purple`、`orange`、`pink`、`cyan`。使用 `default` 重置 |
| 7 | `/config` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 打开设置界面调整主题、模型、输出样式和其他偏好。别名：`/settings` |
| 8 | `/keybindings` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 打开或创建键位绑定配置文件 |
| 9 | `/permissions` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 管理工具权限的允许、询问和拒绝规则。打开交互式对话框，可按作用域查看规则、添加或删除规则、管理工作目录以及查看最近的自动模式拒绝记录。别名：`/allowed-tools` |
| 10 | `/privacy-settings` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 查看和更新隐私设置。仅限 Pro 和 Max 计划订阅者 |
| 11 | `/sandbox` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 切换沙箱模式。仅在支持的平台上可用 |
| 12 | `/statusline` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 配置 Claude Code 的状态栏。描述你想要的内容，或不带参数运行以从 shell 提示符自动配置 |
| 13 | `/stickers` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 订购 Claude Code 贴纸 |
| 14 | `/terminal-setup` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 配置 Shift+Enter 和其他快捷键的终端键位绑定。仅在需要的终端中可见，如 VS Code、Alacritty 或 Warp |
| 15 | `/theme` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 更改颜色主题。包含浅色和深色变体、色盲适配（达尔顿化）主题，以及使用终端调色板的 ANSI 主题 |
| 16 | `/voice` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 切换按键说话语音输入。需要 Claude.ai 账户 |
| 17 | `/context` | ![Context](https://img.shields.io/badge/Context-8E44AD?style=flat) | 以彩色网格可视化当前上下文使用情况。显示上下文占用大户的工具优化建议、记忆膨胀和容量警告 |
| 18 | `/cost` | ![Context](https://img.shields.io/badge/Context-8E44AD?style=flat) | 显示 token 使用统计。查看成本追踪指南了解订阅详情 |
| 19 | `/extra-usage` | ![Context](https://img.shields.io/badge/Context-8E44AD?style=flat) | 配置额外用量以在达到速率限制时继续工作 |
| 20 | `/insights` | ![Context](https://img.shields.io/badge/Context-8E44AD?style=flat) | 生成分析 Claude Code 会话的报告，包括项目领域、交互模式和摩擦点 |
| 21 | `/stats` | ![Context](https://img.shields.io/badge/Context-8E44AD?style=flat) | 可视化每日使用量、会话历史、连续使用天数和模型偏好 |
| 22 | `/status` | ![Context](https://img.shields.io/badge/Context-8E44AD?style=flat) | 打开设置界面（状态标签页），显示版本、模型、账户和连接状态。在 Claude 响应时也可使用，无需等待当前响应完成 |
| 23 | `/usage` | ![Context](https://img.shields.io/badge/Context-8E44AD?style=flat) | 显示计划用量限制和速率限制状态 |
| 24 | `/doctor` | ![Debug](https://img.shields.io/badge/Debug-E74C3C?style=flat) | 诊断并验证 Claude Code 安装和设置。结果以状态图标显示。按 `f` 让 Claude 修复报告的问题 |
| 25 | `/feedback [report]` | ![Debug](https://img.shields.io/badge/Debug-E74C3C?style=flat) | 提交关于 Claude Code 的反馈。别名：`/bug` |
| 26 | `/help` | ![Debug](https://img.shields.io/badge/Debug-E74C3C?style=flat) | 显示帮助和可用命令 |
| 27 | `/powerup` | ![Debug](https://img.shields.io/badge/Debug-E74C3C?style=flat) | 通过带动画演示的快速交互课程发现 Claude Code 功能 |
| 28 | `/release-notes` | ![Debug](https://img.shields.io/badge/Debug-E74C3C?style=flat) | 在交互式版本选择器中查看变更日志。选择特定版本查看其发布说明，或选择显示所有版本 |
| 29 | `/tasks` | ![Debug](https://img.shields.io/badge/Debug-E74C3C?style=flat) | 列出和管理后台任务。别名：`/bashes` |
| 30 | `/copy [N]` | ![Export](https://img.shields.io/badge/Export-7F8C8D?style=flat) | 将最后一条助手响应复制到剪贴板。传入数字 `N` 可复制倒数第 N 条响应：`/copy 2` 复制倒数第二条。当存在代码块时，显示交互式选择器以选择单个代码块或完整响应。在选择器中按 `w` 可将选择写入文件而非剪贴板，这在 SSH 场景下很有用 |
| 31 | `/export [filename]` | ![Export](https://img.shields.io/badge/Export-7F8C8D?style=flat) | 将当前对话导出为纯文本。带文件名时直接写入该文件。不带时打开对话框选择复制到剪贴板或保存到文件 |
| 32 | `/agents` | ![Extensions](https://img.shields.io/badge/Extensions-16A085?style=flat) | 管理代理配置 |
| 33 | `/chrome` | ![Extensions](https://img.shields.io/badge/Extensions-16A085?style=flat) | 配置 Claude in Chrome 设置 |
| 34 | `/hooks` | ![Extensions](https://img.shields.io/badge/Extensions-16A085?style=flat) | 查看工具事件的钩子配置 |
| 35 | `/ide` | ![Extensions](https://img.shields.io/badge/Extensions-16A085?style=flat) | 管理 IDE 集成并显示状态 |
| 36 | `/mcp` | ![Extensions](https://img.shields.io/badge/Extensions-16A085?style=flat) | 管理 MCP 服务器连接和 OAuth 身份验证 |
| 37 | `/plugin` | ![Extensions](https://img.shields.io/badge/Extensions-16A085?style=flat) | 管理 Claude Code 插件 |
| 38 | `/reload-plugins` | ![Extensions](https://img.shields.io/badge/Extensions-16A085?style=flat) | 重新加载所有活跃插件以应用待处理的更改而无需重启。报告每个重新加载组件的计数并标记加载错误 |
| 39 | `/skills` | ![Extensions](https://img.shields.io/badge/Extensions-16A085?style=flat) | 列出可用技能 |
| 40 | `/memory` | ![Memory](https://img.shields.io/badge/Memory-3498DB?style=flat) | 编辑 `CLAUDE.md` 记忆文件，启用或禁用自动记忆，查看自动记忆条目 |
| 41 | `/effort [low\|medium\|high\|max\|auto]` | ![Model](https://img.shields.io/badge/Model-E67E22?style=flat) | 设置模型努力程度。`low`、`medium` 和 `high` 跨会话持久化。`max` 仅适用于当前会话且需要 Opus 4.6。`auto` 重置为模型默认值。不带参数时显示当前级别。无需等待当前响应完成即可生效 |
| 42 | `/fast [on\|off]` | ![Model](https://img.shields.io/badge/Model-E67E22?style=flat) | 切换快速模式开关 |
| 43 | `/model [model]` | ![Model](https://img.shields.io/badge/Model-E67E22?style=flat) | 选择或更换 AI 模型。对于支持的模型，使用左/右箭头键调整努力程度。更改立即生效，无需等待当前响应完成 |
| 44 | `/passes` | ![Model](https://img.shields.io/badge/Model-E67E22?style=flat) | 与朋友分享一周免费 Claude Code。仅在账户符合条件时可见 |
| 45 | `/plan [description]` | ![Model](https://img.shields.io/badge/Model-E67E22?style=flat) | 直接从提示进入计划模式。传入可选描述以进入计划模式并立即开始该任务，例如 `/plan 修复认证 bug` |
| 46 | `/ultraplan <prompt>` | ![Model](https://img.shields.io/badge/Model-E67E22?style=flat) | 在 ultraplan 会话中起草计划，在浏览器中审查，然后远程执行或发送回终端 |
| 47 | `/add-dir <path>` | ![Project](https://img.shields.io/badge/Project-27AE60?style=flat) | 添加当前会话期间可访问文件的工作目录。从添加的目录中不会发现大多数 `.claude/` 配置 |
| 48 | `/diff` | ![Project](https://img.shields.io/badge/Project-27AE60?style=flat) | 打开交互式 diff 查看器，显示未提交的更改和逐轮 diff。使用左/右箭头在当前 git diff 和单独的 Claude 轮次间切换，上/下浏览文件 |
| 49 | `/init` | ![Project](https://img.shields.io/badge/Project-27AE60?style=flat) | 使用 `CLAUDE.md` 指南初始化项目。设置 `CLAUDE_CODE_NEW_INIT=1` 可启用交互式流程，同时引导设置技能、钩子和个人记忆文件 |
| 50 | `/review` | ![Project](https://img.shields.io/badge/Project-27AE60?style=flat) | 已弃用。请改为安装 `code-review` 插件：`claude plugin install code-review@claude-plugins-official` |
| 51 | `/security-review` | ![Project](https://img.shields.io/badge/Project-27AE60?style=flat) | 分析当前分支上待处理更改中的安全漏洞。审查 git diff 并识别注入、认证问题和数据泄露等风险 |
| 52 | `/team-onboarding` | ![Project](https://img.shields.io/badge/Project-27AE60?style=flat) | 从 Claude Code 使用历史生成团队入职指南。分析过去 30 天的会话、命令和 MCP 服务器使用情况 |
| 53 | `/autofix-pr [prompt]` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 在 Web 上启动 Claude Code 会话，监视当前分支的 PR，在 CI 失败或审查者留下评论时推送修复。通过 `gh pr view` 检测已签出分支的开放 PR；要监视其他 PR，请先签出其分支。需要 `gh` CLI 和 Claude Code Web 访问权限 |
| 54 | `/desktop` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 在 Claude Code 桌面应用中继续当前会话。仅限 macOS 和 Windows。别名：`/app` |
| 55 | `/install-github-app` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 为仓库设置 Claude GitHub Actions 应用。引导你选择仓库并配置集成 |
| 56 | `/install-slack-app` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 安装 Claude Slack 应用。打开浏览器完成 OAuth 流程 |
| 57 | `/mobile` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 显示二维码以下载 Claude 移动应用。别名：`/ios`、`/android` |
| 58 | `/remote-control` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 使此会话可从 claude.ai 远程控制。别名：`/rc` |
| 59 | `/remote-env` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 配置使用 `--remote` 启动 Web 会话的默认远程环境 |
| 60 | `/schedule [description]` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 创建、更新、列出或运行例程。Claude 以对话方式引导你完成设置 |
| 61 | `/teleport` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 将 Claude Code Web 会话拉取到此终端：打开选择器，然后获取分支和对话。也可用作 `/tp`。需要 claude.ai 订阅 |
| 62 | `/web-setup` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 使用本地 `gh` CLI 凭据将 GitHub 账户连接到 Claude Code Web。如果 GitHub 未连接，`/schedule` 会自动提示此操作 |
| 63 | `/branch [name]` | ![Session](https://img.shields.io/badge/Session-4A90D9?style=flat) | 在此处创建当前对话的分支。别名：`/fork` |
| 64 | `/btw <question>` | ![Session](https://img.shields.io/badge/Session-4A90D9?style=flat) | 提一个不会添加到对话中的快速旁问 |
| 65 | `/clear` | ![Session](https://img.shields.io/badge/Session-4A90D9?style=flat) | 清除对话历史并释放上下文。别名：`/reset`、`/new` |
| 66 | `/compact [instructions]` | ![Session](https://img.shields.io/badge/Session-4A90D9?style=flat) | 压缩对话，可带可选的聚焦指令 |
| 67 | `/exit` | ![Session](https://img.shields.io/badge/Session-4A90D9?style=flat) | 退出 CLI。别名：`/quit` |
| 68 | `/rename [name]` | ![Session](https://img.shields.io/badge/Session-4A90D9?style=flat) | 重命名当前会话并在提示栏显示名称。不带名称时从对话历史自动生成 |
| 69 | `/resume [session]` | ![Session](https://img.shields.io/badge/Session-4A90D9?style=flat) | 通过 ID 或名称恢复对话，或打开会话选择器。别名：`/continue` |
| 70 | `/rewind` | ![Session](https://img.shields.io/badge/Session-4A90D9?style=flat) | 将对话和/或代码回退到之前的某个点，或从选定消息开始摘要。参见检查点功能。别名：`/checkpoint`、`/undo` |

捆绑技能如 `/debug` 也可能出现在斜杠命令菜单中，但它们不是内置命令。

---

## 来源

- [Claude Code 斜杠命令](https://code.claude.com/docs/en/slash-commands)
- [Claude Code 交互模式](https://code.claude.com/docs/en/interactive-mode)
- [Claude Code 变更日志](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md)
