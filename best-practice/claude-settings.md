# 设置最佳实践

![Last Updated](https://img.shields.io/badge/Last_Updated-Apr%2016%2C%202026%209%3A22%20PM%20PKT-white?style=flat&labelColor=555) ![Version](https://img.shields.io/badge/Claude_Code-v2.1.110-blue?style=flat&labelColor=555)<br>
[![Implemented](https://img.shields.io/badge/Implemented-2ea44f?style=flat)](../.claude/settings.json)

Claude Code `settings.json` 文件中所有可用配置选项的综合指南。截至 v2.1.110，Claude Code 提供 **60+ 个设置**和 **175+ 个环境变量**（使用 `settings.json` 中的 `"env"` 字段可避免包装脚本）。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code 最佳实践</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

## 目录

1. [设置层级](#设置层级)
2. [核心配置](#核心配置)
3. [权限](#权限)
4. [钩子](#钩子)
5. [MCP 服务器](#mcp-服务器)
6. [沙箱](#沙箱)
7. [插件](#插件)
8. [模型配置](#模型配置)
9. [显示与用户体验](#显示与用户体验)
10. [AWS 与云凭据](#aws-与云凭据)
11. [环境变量](#通过-env-配置环境变量)
12. [常用命令](#常用命令)

---

## 设置层级

设置按优先级从高到低应用：

| 优先级 | 位置 | 作用域 | 是否共享？ | 用途 |
|--------|------|--------|-----------|------|
| 1 | 托管设置 | 组织 | 是（由 IT 部署） | 不可覆盖的安全策略 |
| 2 | 命令行参数 | 会话 | 不适用 | 临时单次会话覆盖 |
| 3 | `.claude/settings.local.json` | 项目 | 否（已加入 git-ignore） | 个人项目特定 |
| 4 | `.claude/settings.json` | 项目 | 是（已提交） | 团队共享设置 |
| 5 | `~/.claude/settings.json` | 用户 | 不适用 | 全局个人默认设置 |

**托管设置**由组织强制执行，不能被任何其他级别覆盖，包括命令行参数。交付方式：
- **服务器托管**设置（远程交付）
- **MDM 配置文件** — macOS plist `com.anthropic.claudecode`
- **注册表策略** — Windows `HKLM\SOFTWARE\Policies\ClaudeCode`（管理员）和 `HKCU\SOFTWARE\Policies\ClaudeCode`（用户级，最低策略优先级）
- **文件** — `managed-settings.json` 和 `managed-mcp.json`（macOS：`/Library/Application Support/ClaudeCode/`，Linux/WSL：`/etc/claude-code/`，Windows：`C:\Program Files\ClaudeCode\`）
- **插件目录** — `managed-settings.d/` 位于 `managed-settings.json` 旁边，用于独立的策略片段（v2.1.83）。遵循 systemd 约定，`managed-settings.json` 首先作为基础合并，然后 drop-in 目录中的所有 `*.json` 文件按字母顺序排序并合并在上面。对于标量值，后面的文件覆盖前面的；数组连接并去重；对象深度合并。以 `.` 开头的隐藏文件被忽略。使用数字前缀控制合并顺序（例如 `10-telemetry.json`、`20-security.json`）

在托管层级内，优先级为：服务器托管 > MDM/OS 级策略 > 基于文件的（`managed-settings.d/*.json` + `managed-settings.json`）> HKCU 注册表（仅限 Windows）。仅使用一个托管源；源之间不跨层级合并。在基于文件的层级内，drop-in 文件和基础文件一起合并。

> **注意：** 从 v2.1.75 起，已弃用的 Windows 回退路径 `C:\ProgramData\ClaudeCode\managed-settings.json` 已被移除。请改用 `C:\Program Files\ClaudeCode\managed-settings.json`。

**重要**：
- `deny` 规则具有最高安全优先级，不能被较低优先级的 allow/ask 规则覆盖。
- 托管设置可能锁定或覆盖本地行为，即使本地文件指定了不同的值。
- 数组设置（例如 `permissions.allow`）在作用域间**连接并去重** — 所有级别的条目合并而非替换。

---

## 核心配置

### 通用设置

| 键 | 类型 | 默认值 | 描述 |
|----|------|--------|------|
| `$schema` | string | - | 用于 IDE 验证和自动补全的 JSON Schema URL（例如 `"https://json.schemastore.org/claude-code-settings.json"`） |
| `model` | string | `"default"` | 覆盖默认模型。接受别名（`sonnet`、`opus`、`haiku`）或完整模型 ID |
| `agent` | string | - | 设置主对话的默认代理。值为 `.claude/agents/` 中的代理名称。也可通过 `--agent` CLI 参数使用 |
| `language` | string | `"english"` | Claude 的首选响应语言。同时设置语音输入语言 |
| `cleanupPeriodDays` | number | `30` | 不活跃超过此期限的会话在启动时删除（最小值 1）。同时控制启动时自动移除孤立子代理工作树的年龄截止。设置为 `0` 会被验证错误拒绝。要在非交互模式（`-p`）下禁用记录写入，使用 `--no-session-persistence` 或 `persistSession: false` SDK 选项 |
| `autoUpdatesChannel` | string | `"latest"` | 发布渠道：`"stable"` 或 `"latest"` |
| `minimumVersion` | string | - | 防止自动更新程序降级到特定版本以下。在切换到稳定渠道并选择保持当前版本直到稳定版赶上时自动设置。与 `autoUpdatesChannel` 配合使用 |
| `alwaysThinkingEnabled` | boolean | `false` | 默认为所有会话启用扩展思考 |
| `skipWebFetchPreflight` | boolean | `false` | 获取 URL 前跳过 WebFetch 黑名单检查 *（在 JSON schema 中，但不在官方设置页面上）* |
| `availableModels` | array | - | 限制用户可通过 `/model`、`--model`、Config 工具或 `ANTHROPIC_MODEL` 选择的模型。不影响默认选项。示例：`["sonnet", "haiku"]` |
| `fastModePerSessionOptIn` | boolean | `false` | 要求用户每次会话选择加入快速模式 |
| `defaultShell` | string | `"bash"` | 输入框 `!` 命令的默认 shell。接受 `"bash"`（默认）或 `"powershell"`。设置 `"powershell"` 可在 Windows 上通过 PowerShell 路由交互式 `!` 命令。需要 `CLAUDE_CODE_USE_POWERSHELL_TOOL=1`（v2.1.84） |
| `includeGitInstructions` | boolean | `true` | 在 Claude 的系统提示词中包含内置的提交和 PR 工作流指令以及 git 状态快照。设置时 `CLAUDE_CODE_DISABLE_GIT_INSTRUCTIONS` 环境变量优先于此设置 |
| `voiceEnabled` | boolean | - | 启用按键说话语音输入。运行 `/voice` 时自动写入。需要 Claude.ai 账户 |
| `showClearContextOnPlanAccept` | boolean | `false` | 在计划接受界面显示"清除上下文"选项。设置为 `true` 以恢复该选项（自 v2.1.81 起默认隐藏） |
| `viewMode` | string | - | 启动时的默认记录查看模式：`"default"`、`"verbose"` 或 `"focus"`。设置时覆盖粘性的 Ctrl+O 选择 |
| `disableDeepLinkRegistration` | string | - | 设置为 `"disable"` 以防止 Claude Code 在启动时向操作系统注册 `claude-cli://` 协议处理程序。深度链接允许外部工具通过 `claude-cli://open?q=...` 打开带有预填提示的 Claude Code 会话。`q` 参数支持使用 URL 编码换行符（`%0A`）的多行提示。适用于协议处理程序注册受限或单独管理的环境 |
| `showThinkingSummaries` | boolean | `false` | 在交互式会话中显示扩展思考摘要。未设置或为 `false` 时（交互模式默认），思考块被 API 编辑并显示为折叠存根。编辑仅改变你看到的内容，不改变模型生成的内容 — 要减少思考消耗，降低预算或禁用思考。非交互模式（`-p`）和 SDK 调用者始终接收摘要，不受此设置影响 |
| `disableSkillShellExecution` | boolean | `false` | 禁用来自用户、项目、插件或附加目录来源的技能和自定义命令中 `` !`...` `` 和 `` ```! `` 块的内联 shell 执行。命令被替换为 `[shell command execution disabled by policy]` 而非执行。捆绑和托管技能不受影响（v2.1.91） |
| `forceRemoteSettingsRefresh` | boolean | `false` | **（仅限托管）** 阻止 CLI 启动直到远程托管设置被新获取。如果获取失败，CLI 退出（关闭失败）。用于企业环境中策略执行必须在任何会话开始前保持最新（v2.1.92） |
| `autoScrollEnabled` | boolean | - | 在全屏模式下禁用对话自动滚动。设置为 `false` 以防止自动滚动 *（在 v2.1.110 变更日志中，尚未在官方设置页面上）* |
| `tui` | string | - | 切换渲染模式。使用 `/tui fullscreen` 启用无闪烁渲染 *（在 v2.1.110 变更日志中，尚未在官方设置页面上）* |
| `feedbackSurveyRate` | number | - | 符合条件时会话质量调查出现的概率（0–1）。企业管理员可控制调查显示频率。示例：`0.05` = 5% 的符合条件会话 |

**示例：**
```json
{
  "model": "opus",
  "agent": "code-reviewer",
  "language": "japanese",
  "cleanupPeriodDays": 60,
  "autoUpdatesChannel": "stable",
  "alwaysThinkingEnabled": true
}
```

### 计划与记忆目录

将计划和自动记忆文件存储在自定义位置。

| 键 | 类型 | 默认值 | 描述 |
|----|------|--------|------|
| `plansDirectory` | string | `~/.claude/plans` | `/plan` 输出存储的目录 |
| `autoMemoryDirectory` | string | - | 自动记忆存储的自定义目录。接受 `~/` 扩展路径。不接受在项目设置（`.claude/settings.json`）中设置，以防止将记忆写入重定向到敏感位置；可在策略、本地和用户设置中使用 |

**示例：**
```json
{
  "plansDirectory": "./my-plans"
}
```

**使用场景：** 适用于将规划产出物与 Claude 内部文件分开组织，或将计划保存在共享团队位置。

### 工作树设置

配置 `--worktree` 创建和管理 git 工作树的方式。适用于减少大型单仓库的磁盘使用和启动时间。

| 键 | 类型 | 默认值 | 描述 |
|----|------|--------|------|
| `worktree.symlinkDirectories` | array | `[]` | 要从主仓库符号链接到每个工作树的目录，以避免在磁盘上复制大目录 |
| `worktree.sparsePaths` | array | `[]` | 通过 git sparse-checkout（锥形模式）在每个工作树中签出的目录。仅列出的路径被写入磁盘 |

**示例：**
```json
{
  "worktree": {
    "symlinkDirectories": ["node_modules", ".cache"],
    "sparsePaths": ["packages/my-app", "shared/utils"]
  }
}
```

### 署名设置

自定义 git 提交和拉取请求的署名消息。

| 键 | 类型 | 默认值 | 描述 |
|----|------|--------|------|
| `attribution.commit` | string | Co-authored-by | Git 提交署名（支持 trailer） |
| `attribution.pr` | string | 生成的消息 | 拉取请求描述署名 |
| `includeCoAuthoredBy` | boolean | `true` | **已弃用** - 请改用 `attribution` |

**示例：**
```json
{
  "attribution": {
    "commit": "Generated with AI\n\nCo-Authored-By: Claude <noreply@anthropic.com>",
    "pr": "Generated with Claude Code"
  }
}
```

**注意：** 设置为空字符串（`""`）可完全隐藏署名。

### 身份验证辅助

用于动态生成身份验证令牌的脚本。

| 键 | 类型 | 描述 |
|----|------|------|
| `apiKeyHelper` | string | 输出身份验证令牌的 shell 脚本路径（作为 `X-Api-Key` 头部发送） |
| `forceLoginMethod` | string | 限制登录方式为 `"claudeai"` 或 `"console"` 账户 |
| `forceLoginOrgUUID` | string \| array | 要求登录属于特定组织。接受单个 UUID 字符串（同时在登录时预选该组织）或 UUID 数组（接受任何列出的组织，不进行预选）。在托管设置中设置时，如果已认证账户不属于列出的组织则登录失败；空数组会失败关闭并以配置错误消息阻止登录 |

**示例：**
```json
{
  "apiKeyHelper": "/bin/generate_temp_api_key.sh",
  "forceLoginMethod": "console",
  "forceLoginOrgUUID": ["xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy"]
}
```

### 公司公告

在启动时向用户显示自定义公告（随机循环）。

| 键 | 类型 | 描述 |
|----|------|------|
| `companyAnnouncements` | array | 启动时显示的字符串数组 |

**示例：**
```json
{
  "companyAnnouncements": [
    "欢迎来到 Acme Corp！",
    "记得在提交前运行测试！",
    "查看 wiki 了解编码标准"
  ]
}
```

---

## 权限

控制 Claude 可以执行的工具和操作。

### 权限结构

```json
{
  "permissions": {
    "allow": [],
    "ask": [],
    "deny": [],
    "additionalDirectories": [],
    "defaultMode": "acceptEdits",
    "disableBypassPermissionsMode": "disable"
  }
}
```

### 权限键

| 键 | 类型 | 描述 |
|----|------|------|
| `permissions.allow` | array | 允许无需提示使用工具的规则 |
| `permissions.ask` | array | 需要用户确认的规则 |
| `permissions.deny` | array | 阻止工具使用的规则（最高优先级） |
| `permissions.additionalDirectories` | array | Claude 可访问的额外目录 |
| `permissions.defaultMode` | string | 默认权限模式。在远程环境中，仅 `acceptEdits` 和 `plan` 被执行（v2.1.70+） |
| `permissions.disableBypassPermissionsMode` | string | 防止绕过模式激活 |
| `permissions.skipDangerousModePermissionPrompt` | boolean | 通过 `--dangerously-skip-permissions` 或 `defaultMode: "bypassPermissions"` 进入绕过权限模式前跳过确认提示。在项目设置（`.claude/settings.json`）中设置时被忽略，以防止不受信任的仓库自动绕过提示 |
| `allowManagedPermissionRulesOnly` | boolean | **（仅限托管）** 仅应用托管权限规则；用户/项目的 `allow`、`ask`、`deny` 规则被忽略 |
| `allow_remote_sessions` | boolean | **（仅限托管）** 允许用户启动远程控制和 Web 会话。默认为 `true`。设置为 `false` 以阻止远程会话访问 *（不在官方文档中 — 官方权限页面说明"远程控制和 Web 会话的访问不由托管设置键控制。"在 Team 和 Enterprise 计划中，管理员通过 [Claude Code 管理设置](https://claude.ai/admin-settings/claude-code) 启用/禁用）* |
| `autoMode` | object | 自定义[自动模式](/en/permission-modes#eliminate-prompts-with-auto-mode)分类器阻止和允许的内容。包含 `environment`（受信任的基础设施描述）、`allow`（阻止规则的例外）和 `soft_deny`（阻止规则）— 均为描述性字符串数组。**不从共享项目设置**（`.claude/settings.json`）读取，以防止仓库注入。可在用户、本地和托管设置中使用。设置 `allow` 或 `soft_deny` **替换**该部分的整个默认列表。运行 `claude auto-mode defaults` 查看自定义前的内置规则 |
| `disableAutoMode` | string | 设置为 `"disable"` 以防止[自动模式](/en/permission-modes#eliminate-prompts-with-auto-mode)被激活。从 `Shift+Tab` 循环中移除 `auto` 并在启动时拒绝 `--permission-mode auto`。可在任何设置级别设置；在托管设置中最有用，因为用户无法覆盖 |
| `useAutoModeDuringPlan` | boolean | 计划模式是否在自动模式可用时使用自动模式语义。默认：`true`。不从共享项目设置（`.claude/settings.json`）读取。在 `/config` 中显示为"计划期间使用自动模式" |

### 权限模式

| 模式 | 行为 |
|------|------|
| `"default"` | 标准权限检查，带提示 |
| `"acceptEdits"` | 自动接受文件编辑而不询问 |
| `"askEdits"` | 每次操作前询问 *（不在官方文档中 — 未验证）* |
| `"dontAsk"` | 自动拒绝工具，除非通过 `/permissions` 或 `permissions.allow` 规则预批准 |
| `"viewOnly"` | 只读模式，不进行修改 *（不在官方文档中 — 未验证）* |
| `"bypassPermissions"` | 跳过所有权限检查（危险） |
| `"auto"` | 后台分类器替代手动提示（`--enable-auto-mode`）。研究预览 — 需要 Team 计划 + Sonnet/Opus 4.6。分类器自动批准只读和文件编辑；其他内容通过安全检查。连续 3 次或总计 20 次阻止后回退到提示。使用 `autoMode` 设置配置 |
| `"plan"` | 只读探索模式 |

### 工具权限语法

| 工具 | 语法 | 示例 |
|------|------|------|
| `Bash` | `Bash(command pattern)` | `Bash(npm run *)`、`Bash(* install)`、`Bash(git * main)` |
| `Read` | `Read(path pattern)` | `Read(.env)`、`Read(./secrets/**)` |
| `Edit` | `Edit(path pattern)` | `Edit(src/**)`、`Edit(*.ts)` |
| `Write` | `Write(path pattern)` | `Write(*.md)`、`Write(./docs/**)` |
| `NotebookEdit` | `NotebookEdit(pattern)` | `NotebookEdit(*)` |
| `WebFetch` | `WebFetch(domain:pattern)` | `WebFetch(domain:example.com)` |
| `WebSearch` | `WebSearch` | 全局 Web 搜索 |
| `Task` | `Task(agent-name)` | `Task(Explore)`、`Task(my-agent)` |
| `Agent` | `Agent(name)` | `Agent(researcher)`、`Agent(*)` — 权限限定于子代理生成 |
| `Skill` | `Skill(skill-name)` | `Skill(weather-fetcher)` |
| `MCP` | `mcp__server__tool` 或 `MCP(server:tool)` | `mcp__memory__*`、`MCP(github:*)` |

**评估顺序：** 规则按顺序评估：先 deny 规则，然后 ask，最后 allow。第一个匹配的规则生效。

**Read/Edit 路径模式：** `Read`、`Edit` 和 `Write` 的权限规则支持类似 gitignore 的模式，有四种前缀类型：

| 前缀 | 含义 | 示例 |
|------|------|------|
| `//` | 从文件系统根的绝对路径 | `Read(//Users/alice/file)` |
| `~/` | 相对于主目录 | `Read(~/.zshrc)` |
| `/` | 相对于项目根目录 | `Edit(/src/**)` |
| `./` 或无 | 相对路径（当前目录） | `Read(.env)`、`Read(*.ts)` |

**Bash 通配符说明：**
- `*` 可出现在**任何位置**：前缀（`Bash(* install)`）、后缀（`Bash(npm *)`）或中间（`Bash(git * main)`）
- **词边界：** `Bash(ls *)`（`*` 前有空格）匹配 `ls -la` 但不匹配 `lsof`；`Bash(ls*)`（无空格）两者都匹配
- `Bash(*)` 等同于 `Bash`（匹配所有 bash 命令）
- 权限规则支持输出重定向：`Bash(python:*)` 匹配 `python script.py > output.txt`
- 旧的 `:*` 后缀语法（例如 `Bash(npm:*)`）等同于 ` *` 但已弃用

**示例：**
```json
{
  "permissions": {
    "allow": [
      "Edit(*)",
      "Write(*)",
      "Bash(npm run *)",
      "Bash(git *)",
      "WebFetch(domain:*)",
      "mcp__*"
    ],
    "ask": [
      "Bash(rm *)",
      "Bash(git push *)"
    ],
    "deny": [
      "Read(.env)",
      "Read(./secrets/**)",
      "Bash(curl *)"
    ],
    "additionalDirectories": ["../shared-libs/"]
  }
}
```

---

## 钩子

钩子配置（事件、属性、匹配器、退出码、环境变量和 HTTP 钩子）在专门的仓库中维护：

> **[claude-code-hooks](https://github.com/shanraisshan/claude-code-hooks)** — 完整的钩子参考，包含声音通知系统、所有 25 个钩子事件、HTTP 钩子、匹配器模式、退出码和环境变量。

钩子相关设置键（`hooks`、`disableAllHooks`（同时禁用任何自定义状态栏）、`allowManagedHooksOnly`、`allowedHttpHookUrls`、`httpHookAllowedEnvVars`）在那里有文档记录。

官方钩子参考请参见 [Claude Code 钩子文档](https://code.claude.com/docs/en/hooks)。

---

## MCP 服务器

配置模型上下文协议服务器以获得扩展能力。

### MCP 设置

| 键 | 类型 | 作用域 | 描述 |
|----|------|--------|------|
| `enableAllProjectMcpServers` | boolean | 任意 | 自动批准所有 `.mcp.json` 服务器 |
| `enabledMcpjsonServers` | array | 任意 | 白名单指定服务器名称 |
| `disabledMcpjsonServers` | array | 任意 | 黑名单指定服务器名称 |
| `allowedMcpServers` | array | 仅限托管 | 带名称/命令/URL 匹配的白名单 |
| `deniedMcpServers` | array | 仅限托管 | 带匹配的黑名单 |
| `allowManagedMcpServersOnly` | boolean | 仅限托管 | 仅允许在托管白名单中明确列出的 MCP 服务器 |
| `channelsEnabled` | boolean | 仅限托管 | 为 Team 和 Enterprise 用户允许[频道](https://code.claude.com/docs/en/channels)。未设置或为 `false` 时，无论 `--channels` 参数如何，频道消息传递均被阻止 |
| `allowedChannelPlugins` | array | 仅限托管 | 可推送消息的频道插件白名单。设置时替换默认的 Anthropic 白名单。未定义 = 回退到默认，空数组 = 阻止所有频道插件。需要 `channelsEnabled: true`。每个条目是包含 `marketplace` 和 `plugin` 字段的对象（v2.1.84） |

### MCP 服务器匹配（托管设置）

```json
{
  "allowedMcpServers": [
    { "serverName": "github" },
    { "serverCommand": "npx @modelcontextprotocol/*" },
    { "serverUrl": "https://mcp.company.com/*" }
  ],
  "deniedMcpServers": [
    { "serverName": "dangerous-server" }
  ]
}
```

**示例：**
```json
{
  "enableAllProjectMcpServers": true,
  "enabledMcpjsonServers": ["memory", "github", "filesystem"],
  "disabledMcpjsonServers": ["experimental-server"]
}
```

---

## 沙箱

配置 bash 命令沙箱以提高安全性。

### 沙箱设置

| 键 | 类型 | 默认值 | 描述 |
|----|------|--------|------|
| `sandbox.enabled` | boolean | `false` | 启用 bash 沙箱 |
| `sandbox.failIfUnavailable` | boolean | `false` | 当沙箱已启用但无法启动时退出并报错，而不是在无沙箱状态下运行。适用于要求严格沙箱的企业策略（v2.1.83） |
| `sandbox.autoAllowBashIfSandboxed` | boolean | `true` | 在沙箱中时自动批准 bash |
| `sandbox.excludedCommands` | array | `[]` | 在沙箱外运行的命令 |
| `sandbox.allowUnsandboxedCommands` | boolean | `true` | 允许 `dangerouslyDisableSandbox`。设置为 `false` 时，逃生舱口完全禁用，所有命令必须在沙箱中运行（或在 `excludedCommands` 中）。适用于要求严格沙箱的企业策略 |
| `sandbox.ignoreViolations` | object | `{}` | 命令模式到路径数组的映射 — 抑制违规警告 *（在 JSON schema 中，但不在官方设置页面上）* |
| `sandbox.enableWeakerNestedSandbox` | boolean | `false` | **（仅限 Linux 和 WSL2）** 为非特权 Docker 环境启用较弱的沙箱（降低安全性） |
| `sandbox.network.allowUnixSockets` | array | `[]` | **（仅限 macOS）** 沙箱中可访问的特定 Unix 套接字路径。在 Linux 和 WSL2 上忽略，因为 seccomp 过滤器无法检查套接字路径；请改用 `allowAllUnixSockets` |
| `sandbox.network.allowAllUnixSockets` | boolean | `false` | 允许所有 Unix 套接字（覆盖 `allowUnixSockets`）。在 Linux 和 WSL2 上这是允许 Unix 套接字的唯一方式，因为它跳过了否则会阻止 `socket(AF_UNIX, ...)` 调用的 seccomp 过滤器 |
| `sandbox.network.allowLocalBinding` | boolean | `false` | 允许绑定到 localhost 端口（macOS） |
| `sandbox.network.allowedDomains` | array | `[]` | 沙箱的网络域名白名单 |
| `sandbox.network.deniedDomains` | array | `[]` | 沙箱的网络域名黑名单 *（不在官方文档中 — 未验证）* |
| `sandbox.network.httpProxyPort` | number | - | HTTP 代理端口 1-65535（自定义代理） |
| `sandbox.network.socksProxyPort` | number | - | SOCKS5 代理端口 1-65535（自定义代理） |
| `sandbox.network.allowManagedDomainsOnly` | boolean | `false` | 仅允许托管白名单中的域名（托管设置） |
| `sandbox.network.allowMachLookup` | array | `[]` | （仅限 macOS）沙箱可查找的额外 XPC/Mach 服务名称。支持单个尾部 `*` 进行前缀匹配。需要用于通过 XPC 通信的工具，如 iOS 模拟器或 Playwright。示例：`["com.apple.coresimulator.*"]` |
| `sandbox.filesystem.allowWrite` | array | `[]` | 沙箱命令可写入的额外路径。数组在所有设置作用域间合并。同时与 `Edit(...)` 允许权限规则的路径合并。前缀：`/`（绝对路径），`~/`（主目录），`./` 或无（项目设置中相对于项目，用户设置中相对于 `~/.claude`）。旧的 `//` 绝对路径前缀仍然有效。**注意：** 这与 [Read/Edit 权限规则](#工具权限语法) 不同，后者使用 `//` 表示绝对路径，`/` 表示相对于项目 |
| `sandbox.filesystem.denyWrite` | array | `[]` | 沙箱命令不可写入的路径。数组在所有设置作用域间合并。同时与 `Edit(...)` 拒绝权限规则的路径合并。路径前缀约定与 `allowWrite` 相同 |
| `sandbox.filesystem.denyRead` | array | `[]` | 沙箱命令不可读取的路径。数组在所有设置作用域间合并。同时与 `Read(...)` 拒绝权限规则的路径合并。路径前缀约定与 `allowWrite` 相同 |
| `sandbox.filesystem.allowRead` | array | `[]` | 在 `denyRead` 区域内重新允许读取访问的路径。优先于 `denyRead`。数组在所有设置作用域间合并。路径前缀约定与 `allowWrite` 相同 |
| `sandbox.filesystem.allowManagedReadPathsOnly` | boolean | `false` | **（仅限托管）** 仅使用托管设置中的 `allowRead` 路径。用户、项目和本地设置中的 `allowRead` 条目被忽略 |
| `sandbox.enableWeakerNetworkIsolation` | boolean | `false` | （仅限 macOS）允许访问系统 TLS 信任（`com.apple.trustd.agent`）；降低安全性 |

**示例：**
```json
{
  "sandbox": {
    "enabled": true,
    "autoAllowBashIfSandboxed": true,
    "excludedCommands": ["git", "docker", "gh"],
    "allowUnsandboxedCommands": false,
    "network": {
      "allowUnixSockets": ["/var/run/docker.sock"],
      "allowLocalBinding": true
    }
  }
}
```

---

## 插件

配置 Claude Code 插件和市场。

### 插件设置

| 键 | 类型 | 作用域 | 描述 |
|----|------|--------|------|
| `enabledPlugins` | object | 任意 | 启用/禁用特定插件 |
| `extraKnownMarketplaces` | object | 项目 | 添加自定义插件市场（通过 `.claude/settings.json` 团队共享） |
| `strictKnownMarketplaces` | array | 仅限托管 | 允许的市场白名单 |
| `skippedMarketplaces` | array | 任意 | 用户拒绝安装的市场 *（在 JSON schema 中，但不在官方设置页面上）* |
| `skippedPlugins` | array | 任意 | 用户拒绝安装的插件 *（在 JSON schema 中，但不在官方设置页面上）* |
| `pluginConfigs` | object | 任意 | 每个插件的 MCP 服务器配置（以 `plugin@marketplace` 为键） *（在 JSON schema 中，但不在官方设置页面上）* |
| `blockedMarketplaces` | array | 仅限托管 | 阻止特定插件市场 |
| `pluginTrustMessage` | string | 仅限托管 | 提示用户信任插件时显示的自定义消息 |

**市场源类型：** `github`、`git`、`directory`、`hostPattern`、`settings`、`url`、`npm`、`file`。使用 `source: 'settings'` 可内联声明一小组插件，无需设置托管市场仓库。

**示例：**
```json
{
  "enabledPlugins": {
    "formatter@acme-tools": true,
    "deployer@acme-tools": true,
    "experimental@acme-tools": false
  },
  "extraKnownMarketplaces": {
    "acme-tools": {
      "source": {
        "source": "github",
        "repo": "acme-corp/claude-plugins"
      }
    },
    "inline-tools": {
      "source": {
        "source": "settings",
        "name": "inline-tools",
        "plugins": [
          {
            "name": "code-formatter",
            "source": { "source": "github", "repo": "acme-corp/code-formatter" }
          }
        ]
      }
    }
  }
}
```

---

## 模型配置

### 模型别名

| 别名 | 描述 |
|------|------|
| `"default"` | 推荐给你账户类型的模型 |
| `"sonnet"` | 最新 Sonnet 模型（Claude Sonnet 4.6） |
| `"opus"` | 最新 Opus 模型（Claude Opus 4.6） |
| `"haiku"` | 快速 Haiku 模型 |
| `"sonnet[1m]"` | 带 1M token 上下文的 Sonnet |
| `"opus[1m]"` | 带 1M token 上下文的 Opus（自 v2.1.75 起在 Max、Team 和 Enterprise 上默认） |
| `"opusplan"` | 规划用 Opus，执行用 Sonnet |

**示例：**
```json
{
  "model": "opus"
}
```

### 模型覆盖

将 Anthropic 模型 ID 映射到 Bedrock、Vertex 或 Foundry 部署的特定提供商模型 ID。

| 键 | 类型 | 默认值 | 描述 |
|----|------|--------|------|
| `effortLevel` | string | - | 跨会话持久化努力程度。接受 `"low"`、`"medium"` 或 `"high"`。运行 `/effort low`、`/effort medium` 或 `/effort high` 时自动写入。在 Opus 4.6 和 Sonnet 4.6 上支持 |
| `modelOverrides` | object | - | 将模型选择器条目映射到特定提供商 ID（例如 Bedrock 推理配置文件 ARN）。每个键是模型选择器条目名称，每个值是提供商模型 ID |

**示例：**
```json
{
  "modelOverrides": {
    "claude-opus-4-6": "arn:aws:bedrock:us-east-1:123456789:inference-profile/anthropic.claude-opus-4-6-v1:0",
    "claude-sonnet-4-6": "arn:aws:bedrock:us-east-1:123456789:inference-profile/anthropic.claude-sonnet-4-6-v1:0"
  }
}
```

### 努力程度

`/model` 命令提供了一个**努力程度**控制，用于调整模型在每个响应中投入多少推理。在 `/model` UI 中使用 ← → 箭头键循环切换努力程度。

| 努力程度 | 描述 |
|---------|------|
| Max | 最大推理深度，仅限 Opus 4.6 |
| High（默认） | 完全推理深度，适合复杂任务 |
| Medium | 平衡推理，适合日常任务 |
| Low | 最少推理，最快响应 |

**使用方式：**
1. 运行 `/effort low`、`/effort medium` 或 `/effort high` 直接设置（v2.1.76+）
2. 或运行 `/model` → 选择模型 → 使用 **← →** 箭头键调整
3. 设置通过 `settings.json` 中的 `effortLevel` 键持久化

**注意：** 努力程度在 Max 和 Team 计划上对 Opus 4.6 和 Sonnet 4.6 可用。默认值在 v2.1.68 中从 High 改为 Medium，然后在 v2.1.94 中对 API 密钥、Bedrock/Vertex/Foundry、Team 和 Enterprise 用户改回 **High**。从 v2.1.75 起，Opus 4.6 的 1M 上下文窗口在 Max、Team 和 Enterprise 计划上默认可用。

### 模型环境变量

通过 `env` 键配置：

```json
{
  "env": {
    "ANTHROPIC_MODEL": "sonnet",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "custom-haiku-model",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "custom-sonnet-model",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "custom-opus-model",
    "CLAUDE_CODE_SUBAGENT_MODEL": "haiku",
    "MAX_THINKING_TOKENS": "10000"
  }
}
```

---

## 显示与用户体验

### 显示设置

| 键 | 类型 | 默认值 | 描述 |
|----|------|--------|------|
| `statusLine` | object | - | 自定义状态栏配置 |
| `outputStyle` | string | `"default"` | 输出样式（例如 `"Explanatory"`） |
| `spinnerTipsEnabled` | boolean | `true` | 等待时显示提示 |
| `spinnerVerbs` | object | - | 自定义加载动词，包含 `mode`（"append" 或 "replace"）和 `verbs` 数组 |
| `spinnerTipsOverride` | object | - | 自定义加载提示，包含 `tips`（字符串数组）和可选 `excludeDefault`（boolean） |
| `respectGitignore` | boolean | `true` | 在文件选择器中遵循 .gitignore |
| `prefersReducedMotion` | boolean | `false` | 减少 UI 中的动画和运动效果 |
| `fileSuggestion` | object | - | 自定义文件建议命令（见下方文件建议配置） |

### 全局配置设置（`~/.claude.json`）

这些显示偏好存储在 `~/.claude.json` 中，**而非** `settings.json`。将它们添加到 `settings.json` 会触发 schema 验证错误。

| 键 | 类型 | 默认值 | 描述 |
|----|------|--------|------|
| `autoConnectIde` | boolean | `false` | Claude Code 从外部终端启动时自动连接到运行中的 IDE。在从 VS Code 或 JetBrains 终端外部运行时，在 `/config` 中显示为**自动连接到 IDE（外部终端）** |
| `autoInstallIdeExtension` | boolean | `true` | 从 VS Code 终端运行时自动安装 Claude Code IDE 扩展。在 `/config` 中显示为**自动安装 IDE 扩展**。也可通过 `CLAUDE_CODE_IDE_SKIP_AUTO_INSTALL` 环境变量禁用 |
| `editorMode` | string | `"normal"` | 输入提示的键位绑定模式：`"normal"` 或 `"vim"`。在 `/config` 中显示为**编辑器模式** |
| `showTurnDuration` | boolean | `true` | 响应后显示轮次持续时间消息（例如"耗时 1 分 6 秒"）。直接编辑 `~/.claude.json` 更改 |
| `terminalProgressBarEnabled` | boolean | `true` | 在支持的终端中显示终端进度条（ConEmu、Ghostty 1.2.0+ 和 iTerm2 3.6.6+）。在 `/config` 中显示为**终端进度条** |
| `teammateMode` | string | `"auto"` | [代理团队](https://code.claude.com/docs/en/agent-teams)队友的显示方式：`"auto"`（在 tmux 或 iTerm2 中选择分屏面板，否则进程内），`"in-process"` 或 `"tmux"`。参见[选择显示模式](https://code.claude.com/docs/en/agent-teams#choose-a-display-mode) |

### 状态栏配置

```json
{
  "statusLine": {
    "type": "command",
    "command": "~/.claude/statusline.sh",
    "padding": 2,
    "refreshInterval": 5
  }
}
```

| 字段 | 描述 |
|------|------|
| `type` | 设置为 `"command"` 以运行 shell 脚本 |
| `command` | 生成状态栏输出的 shell 命令或脚本路径 |
| `padding` | 添加到状态栏内容的额外水平间距（字符数）。默认 `0`。控制超出界面内置间距的相对缩进 |
| `refreshInterval` | 除事件驱动更新外，每 N 秒重新运行命令。最小值 `1`。当状态栏显示基于时间的数据（例如时钟）或后台子代理在主会话空闲时更改 git 状态时很有用。不设置则仅在事件时运行（v2.1.97） |

**状态栏输入字段：**

状态栏命令在 stdin 上接收一个 JSON 对象。完整的 JSON schema 和示例请参见[状态栏文档](https://code.claude.com/docs/en/statusline)。

| 字段 | 描述 |
|------|------|
| `model.id`、`model.display_name` | 当前模型标识符和显示名称 |
| `cwd`、`workspace.current_dir` | 当前工作目录（两者包含相同值；推荐 `workspace.current_dir`） |
| `workspace.project_dir` | 启动 Claude Code 的目录（如果工作目录更改可能与 `cwd` 不同） |
| `workspace.added_dirs` | 通过 `/add-dir` 或 `--add-dir` 添加的额外目录 |
| `workspace.git_worktree` | 在使用 `git worktree add` 创建的链接工作树内时的 Git 工作树名称。在主工作树中不存在（v2.1.97） |
| `cost.total_cost_usd` | 会话总成本（美元） |
| `cost.total_duration_ms` | 会话开始以来的总挂钟时间（毫秒） |
| `cost.total_api_duration_ms` | 等待 API 响应的总时间（毫秒） |
| `cost.total_lines_added`、`cost.total_lines_removed` | 会话期间更改的代码行数 |
| `context_window.total_input_tokens`、`context_window.total_output_tokens` | 会话累计 token 计数 |
| `context_window.context_window_size` | 最大上下文窗口大小（token）（默认 200000，扩展上下文为 1000000） |
| `context_window.used_percentage` | 预计算的上下文窗口使用百分比 |
| `context_window.remaining_percentage` | 预计算的上下文窗口剩余百分比 |
| `context_window.current_usage` | 最后一次 API 调用的 token 计数（输入、输出、缓存 token） |
| `exceeds_200k_tokens` | 最近 API 响应的总 token 是否超过 200k（固定阈值） |
| `rate_limits.five_hour.used_percentage` | 五小时速率限制使用百分比（v2.1.80+） |
| `rate_limits.five_hour.resets_at` | 五小时速率限制重置时间戳（Unix 纪元秒） |
| `rate_limits.seven_day.used_percentage` | 七天速率限制使用百分比 |
| `rate_limits.seven_day.resets_at` | 七天速率限制重置时间戳（Unix 纪元秒） |
| `session_id` | 唯一会话标识符 |
| `session_name` | 通过 `--name` 或 `/rename` 设置的自定义会话名称。未设置自定义名称时不存在 |
| `transcript_path` | 对话记录文件路径 |
| `version` | Claude Code 版本 |
| `output_style.name` | 当前输出样式名称 |
| `vim.mode` | 启用 vim 模式时的当前 vim 模式（`NORMAL` 或 `INSERT`） |
| `agent.name` | 使用 `--agent` 参数或代理设置运行时的代理名称 |
| `worktree.name` | 活跃工作树的名称（仅在 `--worktree` 会话期间存在） |
| `worktree.path` | 工作树目录的绝对路径 |
| `worktree.branch` | 工作树的 Git 分支名称。基于钩子的工作树不存在 |
| `worktree.original_cwd` | 进入工作树前的目录 |
| `worktree.original_branch` | 进入工作树前签出的 Git 分支。基于钩子的工作树不存在 |

### 文件建议配置

文件建议脚本在 stdin 上接收一个 JSON 对象（例如 `{"query": "src/comp"}`），必须输出最多 15 个文件路径（每行一个）。

```json
{
  "fileSuggestion": {
    "type": "command",
    "command": "~/.claude/file-suggestion.sh"
  },
  "respectGitignore": true
}
```

**示例：**
```json
{
  "statusLine": {
    "type": "command",
    "command": "git branch --show-current 2>/dev/null || echo 'no-branch'"
  },
  "spinnerTipsEnabled": true,
  "spinnerVerbs": {
    "mode": "replace",
    "verbs": ["Cooking", "Brewing", "Crafting", "Conjuring"]
  },
  "spinnerTipsOverride": {
    "tips": ["在上下文约 50% 时使用 /compact", "复杂任务从计划模式开始"],
    "excludeDefault": true
  }
}
```

---

## AWS 与云凭据

### AWS 设置

| 键 | 类型 | 描述 |
|----|------|------|
| `awsAuthRefresh` | string | 刷新 AWS 认证的脚本（修改 `.aws` 目录） |
| `awsCredentialExport` | string | 输出带 AWS 凭据的 JSON 的脚本 |

**示例：**
```json
{
  "awsAuthRefresh": "aws sso login --profile myprofile",
  "awsCredentialExport": "/bin/generate_aws_grant.sh"
}
```

### OpenTelemetry

| 键 | 类型 | 描述 |
|----|------|------|
| `otelHeadersHelper` | string | 生成动态 OpenTelemetry 头部的脚本 |

**示例：**
```json
{
  "otelHeadersHelper": "/bin/generate_otel_headers.sh"
}
```

---

## 通过 env 配置环境变量

为所有 Claude Code 会话设置环境变量。

```json
{
  "env": {
    "ANTHROPIC_API_KEY": "...",
    "NODE_ENV": "development",
    "DEBUG": "true"
  }
}
```

### 常用环境变量

| 变量 | 描述 |
|------|------|
| `ANTHROPIC_API_KEY` | 身份验证的 API 密钥 |
| `ANTHROPIC_AUTH_TOKEN` | OAuth 令牌 |
| `CLAUDE_CODE_OAUTH_TOKEN` | Claude.ai 身份验证的 OAuth 访问令牌。SDK 和自动化环境中 `/login` 的替代方案。优先于密钥链存储的凭据 |
| `CLAUDE_CODE_OAUTH_REFRESH_TOKEN` | Claude.ai 身份验证的 OAuth 刷新令牌。设置时，`claude auth login` 直接交换此令牌而不打开浏览器。需要 `CLAUDE_CODE_OAUTH_SCOPES` |
| `CLAUDE_CODE_OAUTH_SCOPES` | 刷新令牌签发时的空格分隔 OAuth 作用域（例如 `"user:profile user:inference user:sessions:claude_code"`）。设置 `CLAUDE_CODE_OAUTH_REFRESH_TOKEN` 时必需 |
| `ANTHROPIC_BASE_URL` | 自定义 API 端点 |
| `ANTHROPIC_BEDROCK_BASE_URL` | 覆盖 Bedrock 端点 URL |
| `ANTHROPIC_BEDROCK_MANTLE_BASE_URL` | 覆盖 Bedrock Mantle 端点 URL。参见 [Mantle 端点](https://code.claude.com/docs/en/amazon-bedrock#use-the-mantle-endpoint) |
| `ANTHROPIC_VERTEX_BASE_URL` | 覆盖 Vertex AI 端点 URL |
| `ANTHROPIC_BETAS` | 逗号分隔的 Anthropic beta 头部值 |
| `ANTHROPIC_VERTEX_PROJECT_ID` | Vertex AI 的 GCP 项目 ID |
| `ANTHROPIC_CUSTOM_MODEL_OPTION` | 作为自定义条目添加到 `/model` 选择器中的模型 ID。用于使非标准或网关特定模型可选择而不替换内置别名 |
| `ANTHROPIC_CUSTOM_MODEL_OPTION_NAME` | `/model` 选择器中自定义模型条目的显示名称。未设置时默认为模型 ID |
| `ANTHROPIC_CUSTOM_MODEL_OPTION_DESCRIPTION` | `/model` 选择器中自定义模型条目的显示描述。未设置时默认为 `Custom model (<model-id>)` |
| `ANTHROPIC_CUSTOM_MODEL_OPTION_SUPPORTED_CAPABILITIES` | 覆盖自定义模型条目的能力检测。逗号分隔的值（例如 `effort,thinking`）。当自定义模型支持自动检测无法确认的功能时必需。参见[模型配置](https://code.claude.com/docs/en/model-config#customize-pinned-model-display-and-capabilities) |
| `ANTHROPIC_MODEL` | 使用的模型名称。接受别名（`sonnet`、`opus`、`haiku`）或完整模型 ID。覆盖 `model` 设置 |
| `ANTHROPIC_DEFAULT_HAIKU_MODEL` | 用自定义模型 ID 覆盖 Haiku 模型别名（例如用于第三方部署） |
| `ANTHROPIC_DEFAULT_HAIKU_MODEL_NAME` | 在 Bedrock/Vertex/Foundry 上使用固定模型时自定义 `/model` 选择器中 Haiku 条目的标签。默认为模型 ID |
| `ANTHROPIC_DEFAULT_HAIKU_MODEL_DESCRIPTION` | 自定义 `/model` 选择器中 Haiku 条目的描述。默认为 `Custom model (<model-id>)` |
| `ANTHROPIC_DEFAULT_HAIKU_MODEL_SUPPORTED_CAPABILITIES` | 覆盖固定 Haiku 模型的能力检测。逗号分隔的值（例如 `effort,thinking`）。当固定模型支持自动检测无法确认的功能时必需 |
| `CLAUDECODE` | 在 Claude Code 生成的 shell 环境中设置为 `1`（Bash 工具、tmux 会话）。不在钩子或状态栏命令中设置。用于检测脚本是否在 Claude Code shell 内运行 |
| `CLAUDE_CODE_SKIP_FAST_MODE_NETWORK_ERRORS` | 设置为 `1` 以在组织状态检查因网络错误失败时允许快速模式。当企业代理阻止状态端点时很有用 |
| `CLAUDE_CODE_USE_BEDROCK` | 使用 AWS Bedrock（`1` 启用） |
| `CLAUDE_CODE_USE_VERTEX` | 使用 Google Vertex AI（`1` 启用） |
| `CLAUDE_CODE_USE_FOUNDRY` | 使用 Microsoft Foundry（`1` 启用） |
| `CLAUDE_CODE_USE_MANTLE` | 使用 Bedrock [Mantle 端点](https://code.claude.com/docs/en/amazon-bedrock#use-the-mantle-endpoint)（`1` 启用） |
| `CLAUDE_CODE_USE_POWERSHELL_TOOL` | 设置为 `1` 以在 Windows 上启用 PowerShell 工具（选择加入预览）。启用后，Claude 可原生运行 PowerShell 命令而非通过 Git Bash 路由。仅在原生 Windows 上支持，不支持 WSL（v2.1.84） |
| `CLAUDE_CODE_REMOTE` | 只读。当 Claude Code 作为云会话运行时自动设置为 `true`。从钩子或设置脚本中读取以检测是否在云环境中 |
| `CLAUDE_CODE_REMOTE_SESSION_ID` | 只读。在云会话中自动设置为当前会话的 ID。读取此值以构建回到会话记录的链接 |
| `CLAUDE_REMOTE_CONTROL_SESSION_NAME_PREFIX` | 自动生成的远程控制会话名称前缀。默认为主机名 |
| `CLAUDE_CODE_ENABLE_TELEMETRY` | 启用/禁用遥测（`0` 或 `1`） |
| `DISABLE_ERROR_REPORTING` | 禁用错误报告（`1` 禁用） |
| `DISABLE_AUTOUPDATER` | 设置为 `1` 以禁用对 npm 注册表的自动更新检查。也可配置为仅启动时变量 — 参见 [CLI 启动参数](./claude-cli-startup-flags.md#环境变量) |
| `DISABLE_TELEMETRY` | 禁用遥测（`1` 禁用） |
| `MCP_TIMEOUT` | MCP 启动超时（毫秒） |
| `MAX_MCP_OUTPUT_TOKENS` | 最大 MCP 输出 token（默认：25000）。输出超过 10,000 token 时显示警告 |
| `API_TIMEOUT_MS` | API 请求超时（毫秒，默认：600000） |
| `BASH_MAX_TIMEOUT_MS` | Bash 命令超时 |
| `BASH_MAX_OUTPUT_LENGTH` | 最大 bash 输出长度 |
| `CLAUDE_AUTOCOMPACT_PCT_OVERRIDE` | 自动压缩阈值百分比（1-100）。默认约 95%。设置更低值（例如 `50`）以更早触发压缩。高于 95% 的值无效。使用 `/context` 监控当前使用率。示例：`CLAUDE_AUTOCOMPACT_PCT_OVERRIDE=50 claude` |
| `CLAUDE_CODE_MAX_CONTEXT_TOKENS` | 覆盖 Claude Code 为活跃模型假设的上下文窗口大小。仅在同时设置 `DISABLE_COMPACT` 时生效。当通过 `ANTHROPIC_BASE_URL` 路由到上下文窗口与内置大小不匹配的模型时使用 |
| `CLAUDE_BASH_MAINTAIN_PROJECT_WORKING_DIR` | 在 bash 调用间保持工作目录（`1` 启用） |
| `CLAUDE_CODE_DISABLE_BACKGROUND_TASKS` | 禁用后台任务（`1` 禁用） |
| `ENABLE_TOOL_SEARCH` | MCP 工具搜索阈值（例如 `auto:5`） |
| `ENABLE_PROMPT_CACHING_1H` | 选择加入 1 小时提示缓存 TTL。替换已弃用的 `ENABLE_PROMPT_CACHING_1H_BEDROCK` *（在 v2.1.108 变更日志中，尚未在官方环境变量页面上）* |
| `FORCE_PROMPT_CACHING_5M` | 强制 5 分钟提示缓存 TTL *（在 v2.1.108 变更日志中，尚未在官方环境变量页面上）* |
| `DISABLE_PROMPT_CACHING` | 禁用所有提示缓存（`1` 禁用） |
| `DISABLE_PROMPT_CACHING_HAIKU` | 禁用 Haiku 提示缓存 |
| `DISABLE_PROMPT_CACHING_SONNET` | 禁用 Sonnet 提示缓存 |
| `DISABLE_PROMPT_CACHING_OPUS` | 禁用 Opus 提示缓存 |
| `ENABLE_PROMPT_CACHING_1H_BEDROCK` | 在 Bedrock 上请求 1 小时缓存 TTL（`1` 启用） *（不在官方文档中 — 未验证；v2.1.108 变更日志说已弃用，被 `ENABLE_PROMPT_CACHING_1H` 替代）* |
| `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS` | 禁用实验性 beta 功能（`1` 禁用） |
| `CLAUDE_CODE_SHELL` | 覆盖自动 shell 检测 |
| `CLAUDE_CODE_FILE_READ_MAX_OUTPUT_TOKENS` | 覆盖默认文件读取 token 限制 |
| `CLAUDE_CODE_GLOB_HIDDEN` | 设置为 `false` 以在 Claude 调用 Glob 工具时从结果中排除点文件。默认包含。不影响 `@` 文件自动补全、`ls`、Grep 或 Read |
| `CLAUDE_CODE_GLOB_NO_IGNORE` | 设置为 `false` 以使 Glob 工具遵循 `.gitignore` 模式。默认情况下，Glob 返回所有匹配文件，包括被 gitignore 的文件。不影响 `@` 文件自动补全，后者有自己的 `respectGitignore` 设置 |
| `CLAUDE_CODE_GLOB_TIMEOUT_SECONDS` | Glob 文件发现超时（秒） |
| `CLAUDE_CODE_ENABLE_TASKS` | 设置为 `true` 以在非交互模式（`-p` 参数）中启用任务追踪。交互模式下默认启用 |
| `CLAUDE_CODE_SIMPLE` | 设置为 `1` 以使用最小系统提示词和仅 Bash、文件读取和文件编辑工具运行 |
| `CLAUDE_CODE_EXIT_AFTER_STOP_DELAY` | SDK 模式下空闲后自动退出的延迟（毫秒） |
| `CLAUDE_CODE_DISABLE_ADAPTIVE_THINKING` | 禁用自适应思考（`1` 禁用） |
| `CLAUDE_CODE_DISABLE_THINKING` | 强制禁用扩展思考（`1` 禁用） |
| `DISABLE_INTERLEAVED_THINKING` | 防止发送交错思考 beta 头部（`1` 禁用） |
| `CLAUDE_CODE_DISABLE_1M_CONTEXT` | 禁用 1M token 上下文窗口（`1` 禁用） |
| `CLAUDE_CODE_ACCOUNT_UUID` | 覆盖身份验证的账户 UUID |
| `CLAUDE_CODE_DISABLE_GIT_INSTRUCTIONS` | 禁用 git 相关的系统提示词指令 |
| `CLAUDE_CODE_NEW_INIT` | 设置为 `true` 以使 `/init` 运行交互式设置流程。在探索代码库之前询问要生成哪些文件（CLAUDE.md、技能、钩子）。不设置时，`/init` 自动生成 CLAUDE.md |
| `CLAUDE_CODE_PLUGIN_SEED_DIR` | 一个或多个只读插件种子目录的路径，Unix 上用 `:` 分隔，Windows 上用 `;` 分隔。将预填充的插件打包到容器镜像中。Claude Code 在启动时从这些目录注册市场并使用预缓存的插件而无需重新克隆 |
| `ENABLE_CLAUDEAI_MCP_SERVERS` | 启用 Claude.ai MCP 服务器 |
| `CLAUDE_CODE_EFFORT_LEVEL` | 设置努力程度：`low`、`medium`、`high`、`max`（仅限 Opus 4.6）或 `auto`（使用模型默认值）。优先于 `/effort` 和 `effortLevel` 设置 |
| `CLAUDE_CODE_MAX_TURNS` | 停止前的最大智能轮次 *（不在官方文档中 — 未验证）* |
| `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` | 等同于同时设置 `DISABLE_AUTOUPDATER`、`DISABLE_FEEDBACK_COMMAND`、`DISABLE_ERROR_REPORTING` 和 `DISABLE_TELEMETRY` |
| `CLAUDE_CODE_SKIP_SETTINGS_SETUP` | 跳过首次运行设置流程 *（不在官方文档中 — 未验证）* |
| `CLAUDE_CODE_PROMPT_CACHING_ENABLED` | 覆盖提示缓存行为 *（不在官方文档中 — 未验证）* |
| `CLAUDE_CODE_DISABLE_TOOLS` | 逗号分隔的要禁用的工具列表 *（不在官方文档中 — 未验证）* |
| `CLAUDE_CODE_DISABLE_MCP` | 禁用所有 MCP 服务器（`1` 禁用） *（不在官方文档中 — 未验证）* |
| `CLAUDE_CODE_MAX_OUTPUT_TOKENS` | 每个响应的最大输出 token。默认：32,000（从 v2.1.77 起 Opus 4.6 为 64,000）。上限：64,000（从 v2.1.77 起 Opus 4.6 和 Sonnet 4.6 为 128,000） |
| `CLAUDE_CODE_DISABLE_FAST_MODE` | 完全禁用快速模式（`1` 禁用） |
| `CLAUDE_CODE_DISABLE_NONSTREAMING_FALLBACK` | 设置为 `1` 以在流式请求中途失败时禁用非流式回退。流式错误传播到重试层。当代理或网关导致回退产生重复工具执行时很有用（v2.1.83） |
| `CLAUDE_ENABLE_STREAM_WATCHDOG` | 中止卡住的流（`1` 启用） |
| `CLAUDE_CODE_ENABLE_FINE_GRAINED_TOOL_STREAMING` | 启用细粒度工具流式传输（`1` 启用） |
| `CLAUDE_CODE_DISABLE_AUTO_MEMORY` | 禁用自动记忆（`1` 禁用） |
| `CLAUDE_CODE_DISABLE_FILE_CHECKPOINTING` | 禁用 `/rewind` 的文件检查点（`1` 禁用） |
| `CLAUDE_CODE_DISABLE_ATTACHMENTS` | 禁用附件处理（`1` 禁用） |
| `CLAUDE_CODE_DISABLE_CLAUDE_MDS` | 阻止加载 CLAUDE.md 文件（`1` 禁用） |
| `CLAUDE_CODE_RESUME_INTERRUPTED_TURN` | 如果上一会话在轮次中途结束则自动恢复（`1` 启用） |
| `CLAUDE_CODE_SKIP_PROMPT_HISTORY` | 设置为 `1` 以跳过将提示历史和会话记录写入磁盘。使用此变量启动的会话不会出现在 `--resume`、`--continue` 或上箭头历史中。适用于临时脚本会话 |
| `CLAUDE_CODE_USER_EMAIL` | 同步提供身份验证的用户电子邮件 |
| `CLAUDE_CODE_ORGANIZATION_UUID` | 同步提供身份验证的组织 UUID |
| `CLAUDE_CONFIG_DIR` | 自定义配置目录（覆盖默认 `~/.claude`） |
| `CLAUDE_CODE_TMPDIR` | 覆盖内部临时文件使用的临时目录。Claude Code 会在此路径后追加 `/claude/`。默认：Unix/macOS 上 `/tmp`，Windows 上 `os.tmpdir()` |
| `ANTHROPIC_CUSTOM_HEADERS` | API 请求的自定义头部（`Name: Value` 格式，多个头部用换行符分隔） |
| `ANTHROPIC_FOUNDRY_API_KEY` | Microsoft Foundry 身份验证的 API 密钥 |
| `ANTHROPIC_FOUNDRY_BASE_URL` | Foundry 资源的基础 URL |
| `ANTHROPIC_FOUNDRY_RESOURCE` | Foundry 资源名称 |
| `AWS_BEARER_TOKEN_BEDROCK` | Bedrock 身份验证的 API 密钥 |
| `ANTHROPIC_SMALL_FAST_MODEL` | **已弃用** — 请改用 `ANTHROPIC_DEFAULT_HAIKU_MODEL` |
| `ANTHROPIC_SMALL_FAST_MODEL_AWS_REGION` | 已弃用的 Haiku 类模型覆盖的 AWS 区域 |
| `CLAUDE_CODE_SHELL_PREFIX` | 前缀命令，附加到 bash 命令前 |
| `BASH_DEFAULT_TIMEOUT_MS` | 默认 bash 命令超时（毫秒） |
| `CLAUDE_CODE_SKIP_BEDROCK_AUTH` | 跳过 Bedrock 的 AWS 认证（`1` 跳过） |
| `CLAUDE_CODE_SKIP_FOUNDRY_AUTH` | 跳过 Foundry 的 Azure 认证（`1` 跳过） |
| `CLAUDE_CODE_SKIP_MANTLE_AUTH` | 跳过 Bedrock Mantle 的 AWS 认证（例如使用 LLM 网关时） |
| `CLAUDE_CODE_SKIP_VERTEX_AUTH` | 跳过 Vertex 的 Google 认证（`1` 跳过） |
| `CLAUDE_CODE_PROXY_RESOLVES_HOSTS` | 允许代理执行 DNS 解析 |
| `CLAUDE_CODE_API_KEY_HELPER_TTL_MS` | `apiKeyHelper` 的凭据刷新间隔（毫秒） |
| `CLAUDE_CODE_CLIENT_CERT` | mTLS 的客户端证书路径 |
| `CLAUDE_CODE_CLIENT_KEY` | mTLS 的客户端私钥路径 |
| `CLAUDE_CODE_CLIENT_KEY_PASSPHRASE` | 加密 mTLS 密钥的密码 |
| `CLAUDE_CODE_CERT_STORE` | 逗号分隔的 TLS 连接 CA 证书来源列表：`bundled`（Claude Code 附带的 Mozilla CA 集）和/或 `system`（OS 信任存储）。默认：`bundled,system`。系统存储集成需要原生二进制分发；在 Node.js 运行时上，无论此值如何都仅使用捆绑集（v2.1.101） |
| `CLAUDE_CODE_PLUGIN_GIT_TIMEOUT_MS` | 插件市场 git 克隆超时（毫秒，默认：120000） |
| `CLAUDE_CODE_PLUGIN_CACHE_DIR` | 覆盖插件根目录 |
| `CLAUDE_CODE_DISABLE_OFFICIAL_MARKETPLACE_AUTOINSTALL` | 跳过自动添加官方市场（`1` 禁用） |
| `CLAUDE_CODE_SYNC_PLUGIN_INSTALL` | 等待插件安装完成后再执行首次查询（`1` 启用） |
| `CLAUDE_CODE_SYNC_PLUGIN_INSTALL_TIMEOUT_MS` | 同步插件安装超时（毫秒） |
| `CLAUDE_CODE_PLUGIN_KEEP_MARKETPLACE_ON_FAILURE` | 设置为 `1` 以在 `git pull` 失败时保留现有市场缓存而不是清除并重新克隆。在离线或隔离环境中很有用，因为重新克隆会以相同方式失败 |
| `CLAUDE_CODE_HIDE_ACCOUNT_INFO` | 从 UI 隐藏电子邮件/组织信息 *（不在官方文档中 — 未验证）* |
| `CLAUDE_CODE_DISABLE_CRON` | 禁用计划/cron 任务（`1` 禁用） |
| `DISABLE_INSTALLATION_CHECKS` | 禁用安装警告 |
| `DISABLE_FEEDBACK_COMMAND` | 禁用 `/feedback` 命令。旧名称 `DISABLE_BUG_COMMAND` 也被接受 |
| `DISABLE_DOCTOR_COMMAND` | 隐藏 `/doctor` 命令（`1` 禁用） |
| `DISABLE_LOGIN_COMMAND` | 隐藏 `/login` 命令（`1` 禁用） |
| `DISABLE_LOGOUT_COMMAND` | 隐藏 `/logout` 命令（`1` 禁用） |
| `DISABLE_UPGRADE_COMMAND` | 隐藏 `/upgrade` 命令（`1` 禁用） |
| `DISABLE_EXTRA_USAGE_COMMAND` | 隐藏 `/extra-usage` 命令（`1` 禁用） |
| `DISABLE_INSTALL_GITHUB_APP_COMMAND` | 隐藏 `/install-github-app` 命令（`1` 禁用） |
| `DISABLE_NON_ESSENTIAL_MODEL_CALLS` | 禁用装饰性文本和非必要模型调用 *（不在官方文档中 — 未验证）* |
| `CLAUDE_CODE_DEBUG_LOGS_DIR` | 覆盖调试日志文件目录路径 |
| `CLAUDE_CODE_DEBUG_LOG_LEVEL` | 最低调试日志级别 |
| `CLAUDE_AUTO_BACKGROUND_TASKS` | 强制自动后台运行长任务（`1` 启用） |
| `CLAUDE_CODE_DISABLE_LEGACY_MODEL_REMAP` | 防止将 Opus 4.0/4.1 重映射到新模型（`1` 禁用） |
| `FALLBACK_FOR_ALL_PRIMARY_MODELS` | 为所有主要模型触发回退模型，而不仅仅是默认（`1` 启用） |
| `CCR_FORCE_BUNDLE` | 设置为 `1` 以强制 `claude --remote` 打包并上传本地仓库，即使有 GitHub 访问权限。也可配置为仅启动时变量 — 参见 [CLI 启动参数](./claude-cli-startup-flags.md#环境变量) |
| `CLAUDE_CODE_GIT_BASH_PATH` | 仅限 Windows：Git Bash 可执行文件（`bash.exe`）的路径。当 Git Bash 已安装但不在 PATH 中时使用 |
| `DISABLE_COST_WARNINGS` | 禁用成本警告消息 |
| `CLAUDE_CODE_SUBAGENT_MODEL` | 覆盖子代理模型（例如 `haiku`、`sonnet`） |
| `CLAUDE_CODE_SUBPROCESS_ENV_SCRUB` | 设置为 `1` 以从子进程环境（Bash 工具、钩子、MCP stdio 服务器）中清除 Anthropic 和云提供商凭据。当子进程不应继承 API 密钥时用于纵深防御（v2.1.83） |
| `CLAUDE_CODE_SCRIPT_CAPS` | JSON 对象，限制设置 `CLAUDE_CODE_SUBPROCESS_ENV_SCRUB` 时特定脚本每个会话可被调用的次数。键是与命令文本匹配的子字符串；值是整数调用限制。例如 `{"deploy.sh": 2}` 允许 `deploy.sh` 最多被调用两次。匹配基于子字符串；通过 `xargs` 或 `find -exec` 的运行时扩展不被检测 — 这是一个纵深防御控制 |
| `CLAUDE_CODE_PERFORCE_MODE` | 设置为 `1` 以启用 Perforce 感知的写保护。设置时，如果目标文件缺少所有者写入位，Edit、Write 和 NotebookEdit 会失败并提示 `p4 edit <file>`，因为 Perforce 在同步文件后清除该位直到 `p4 edit` 打开它们。防止 Claude Code 绕过 Perforce 变更追踪（v2.1.98） |
| `CLAUDE_CODE_MAX_RETRIES` | 覆盖 API 请求重试次数（默认：10） |
| `CLAUDE_CODE_MAX_TOOL_USE_CONCURRENCY` | 最大并行只读工具数（默认：10） |
| `CLAUDE_AGENT_SDK_DISABLE_BUILTIN_AGENTS` | 在 SDK 模式下禁用内置子代理类型（`1` 禁用） |
| `CLAUDE_AGENT_SDK_MCP_NO_PREFIX` | 在 SDK 模式下跳过 MCP 工具的 `mcp__<server>__` 前缀（`1` 启用） |
| `MCP_CONNECTION_NONBLOCKING` | 在 `-p` 模式下设置为 `true` 以完全跳过 MCP 连接等待。将 `--mcp-config` 服务器连接限制在 5 秒而不是阻塞在最慢的服务器上 *（在 v2.1.89 变更日志中，尚未在官方环境变量页面上）* |
| `CLAUDE_CODE_SESSIONEND_HOOKS_TIMEOUT_MS` | SessionEnd 钩子超时（毫秒）（替换硬编码的 1.5 秒限制） |
| `CLAUDE_CODE_DISABLE_FEEDBACK_SURVEY` | 禁用反馈调查提示（`1` 禁用） |
| `CLAUDE_CODE_DISABLE_TERMINAL_TITLE` | 禁用终端标题更新（`1` 禁用） |
| `CLAUDE_CODE_TMUX_TRUECOLOR` | 设置为 `1` 以允许在 tmux 内输出 24 位真彩色。默认情况下，当设置了 `$TMUX` 时 Claude Code 限制为 256 色，因为 tmux 不会传递真彩色转义序列除非已配置。在 `~/.tmux.conf` 中添加 `set -ga terminal-overrides ',*:Tc'` 后设置此项 |
| `CLAUDE_CODE_NO_FLICKER` | 设置为 `1` 以启用无闪烁的 alt-screen 渲染。消除全屏重绘时的视觉闪烁（v2.1.88） |
| `CLAUDE_CODE_SCROLL_SPEED` | 全屏渲染的鼠标滚轮滚动倍数。增加以加快滚动，减少以获得更精细的控制 |
| `CLAUDE_CODE_DISABLE_VIRTUAL_SCROLL` | 设置为 `1` 以在全屏渲染中禁用虚拟滚动并渲染记录中的每条消息。如果全屏模式下滚动显示空白区域时使用 |
| `CLAUDE_CODE_DISABLE_MOUSE` | 设置为 `1` 以在全屏渲染中禁用鼠标追踪。当鼠标事件干扰终端复用器或辅助功能工具时很有用 |
| `CLAUDE_CODE_ACCESSIBILITY` | 设置为 `1` 以保持原生终端光标可见，用于屏幕阅读器和辅助功能工具 |
| `CLAUDE_CODE_SYNTAX_HIGHLIGHT` | 设置为 `0` 以禁用 diff 输出中的语法高亮 |
| `CLAUDE_CODE_IDE_SKIP_AUTO_INSTALL` | 跳过自动 IDE 扩展安装（`1` 跳过） |
| `CLAUDE_CODE_AUTO_CONNECT_IDE` | 覆盖自动 IDE 连接行为 |
| `CLAUDE_CODE_IDE_HOST_OVERRIDE` | 覆盖连接的 IDE 主机地址 |
| `CLAUDE_CODE_IDE_SKIP_VALID_CHECK` | 跳过 IDE 锁文件验证（`1` 跳过） |
| `CLAUDE_CODE_OTEL_HEADERS_HELPER_DEBOUNCE_MS` | OTel 头部辅助脚本的防抖间隔（毫秒） |
| `CLAUDE_CODE_OTEL_FLUSH_TIMEOUT_MS` | OpenTelemetry 刷新超时（毫秒） |
| `CLAUDE_CODE_OTEL_SHUTDOWN_TIMEOUT_MS` | OpenTelemetry 关闭超时（毫秒） |
| `CLAUDE_ENABLE_BYTE_WATCHDOG` | 设置为 `1` 以强制启用字节级流式空闲看门狗，或 `0` 强制禁用。未设置时，默认为 Anthropic API 连接启用看门狗。字节看门狗在 `CLAUDE_STREAM_IDLE_TIMEOUT_MS` 设置的持续时间内没有字节到达时中止连接（最少 5 分钟），独立于事件级看门狗 |
| `CLAUDE_STREAM_IDLE_TIMEOUT_MS` | 流式空闲看门狗超时（毫秒）。应用两个看门狗：**字节级**（默认和最小 `300000` / 5 分钟，在没有字节到达时中止）和**事件级**（默认 `90000` / 90 秒，无最小值，在没有 SSE 事件到达时中止）。字节看门狗默认为 Anthropic API 连接启用；通过 `CLAUDE_ENABLE_BYTE_WATCHDOG` 控制。如果长时间运行的工具或慢速网络导致过早超时错误，增加事件超时 |
| `OTEL_LOG_TOOL_DETAILS` | 设置为 `1` 以在 OpenTelemetry 事件中包含 `tool_parameters`。出于隐私默认省略 *（在 v2.1.85 变更日志中，尚未在官方环境变量页面上）* |
| `CLAUDE_CODE_MCP_SERVER_NAME` | MCP 服务器名称，作为环境变量传递给 `headersHelper` 脚本，以便它们可以生成特定于服务器的认证头部 *（在 v2.1.85 变更日志中，尚未在官方环境变量页面上）* |
| `CLAUDE_CODE_MCP_SERVER_URL` | MCP 服务器 URL，作为环境变量与 `CLAUDE_CODE_MCP_SERVER_NAME` 一起传递给 `headersHelper` 脚本 *（在 v2.1.85 变更日志中，尚未在官方环境变量页面上）* |
| `ANTHROPIC_DEFAULT_OPUS_MODEL` | 覆盖 Opus 模型别名（例如 `claude-opus-4-6[1m]`） |
| `ANTHROPIC_DEFAULT_OPUS_MODEL_NAME` | 在 Bedrock/Vertex/Foundry 上使用固定模型时自定义 `/model` 选择器中 Opus 条目的标签。默认为模型 ID |
| `ANTHROPIC_DEFAULT_OPUS_MODEL_DESCRIPTION` | 自定义 `/model` 选择器中 Opus 条目的描述。默认为 `Custom model (<model-id>)` |
| `ANTHROPIC_DEFAULT_OPUS_MODEL_SUPPORTED_CAPABILITIES` | 覆盖固定 Opus 模型的能力检测。逗号分隔的值（例如 `effort,thinking`）。当固定模型支持自动检测无法确认的功能时必需 |
| `ANTHROPIC_DEFAULT_SONNET_MODEL` | 覆盖 Sonnet 模型别名（例如 `claude-sonnet-4-6`） |
| `ANTHROPIC_DEFAULT_SONNET_MODEL_NAME` | 在 Bedrock/Vertex/Foundry 上使用固定模型时自定义 `/model` 选择器中 Sonnet 条目的标签。默认为模型 ID |
| `ANTHROPIC_DEFAULT_SONNET_MODEL_DESCRIPTION` | 自定义 `/model` 选择器中 Sonnet 条目的描述。默认为 `Custom model (<model-id>)` |
| `ANTHROPIC_DEFAULT_SONNET_MODEL_SUPPORTED_CAPABILITIES` | 覆盖固定 Sonnet 模型的能力检测。逗号分隔的值（例如 `effort,thinking`）。当固定模型支持自动检测无法确认的功能时必需 |
| `MAX_THINKING_TOKENS` | 每个响应的最大扩展思考 token |
| `CLAUDE_CODE_AUTO_COMPACT_WINDOW` | 设置用于自动压缩计算的上下文容量（token）。默认为模型的上下文窗口（标准 200K，扩展上下文模型 1M）。在 1M 模型上使用较低值（例如 `500000`）将其视为 500K 进行压缩。上限为实际上下文窗口。`CLAUDE_AUTOCOMPACT_PCT_OVERRIDE` 作为此值的百分比应用。设置此项会将压缩阈值与状态栏的 `used_percentage` 脱钩 |
| `DISABLE_AUTO_COMPACT` | 禁用自动上下文压缩（`1` 禁用）。手动 `/compact` 仍然有效 |
| `DISABLE_COMPACT` | 禁用所有压缩 — 自动和手动（`1` 禁用） |
| `CLAUDE_CODE_ENABLE_PROMPT_SUGGESTION` | 启用提示建议 |
| `CLAUDE_CODE_PLAN_MODE_REQUIRED` | 要求会话使用计划模式 |
| `CLAUDE_CODE_TEAM_NAME` | 代理团队的团队名称 |
| `CLAUDE_CODE_TASK_LIST_ID` | 任务集成的任务列表 ID |
| `CLAUDE_ENV_FILE` | 自定义环境文件路径 |
| `FORCE_AUTOUPDATE_PLUGINS` | 强制插件自动更新（`1` 启用） |
| `HTTP_PROXY` | 网络请求的 HTTP 代理 URL |
| `HTTPS_PROXY` | 网络请求的 HTTPS 代理 URL |
| `NO_PROXY` | 逗号分隔的绕过代理的主机列表 |
| `MCP_TOOL_TIMEOUT` | MCP 工具执行超时（毫秒） |
| `MCP_CLIENT_SECRET` | MCP OAuth 客户端密钥 |
| `MCP_OAUTH_CALLBACK_PORT` | MCP OAuth 回调端口 |
| `IS_DEMO` | 启用演示模式 |
| `SLASH_COMMAND_TOOL_CHAR_BUDGET` | 斜杠命令工具输出的字符预算 |
| `VERTEX_REGION_CLAUDE_3_5_HAIKU` | Claude 3.5 Haiku 的 Vertex AI 区域覆盖 |
| `VERTEX_REGION_CLAUDE_3_7_SONNET` | Claude 3.7 Sonnet 的 Vertex AI 区域覆盖 |
| `VERTEX_REGION_CLAUDE_4_0_OPUS` | Claude 4.0 Opus 的 Vertex AI 区域覆盖 |
| `VERTEX_REGION_CLAUDE_4_0_SONNET` | Claude 4.0 Sonnet 的 Vertex AI 区域覆盖 |
| `VERTEX_REGION_CLAUDE_4_1_OPUS` | Claude 4.1 Opus 的 Vertex AI 区域覆盖 |

---

## 常用命令

| 命令 | 描述 |
|------|------|
| `/model` | 切换模型并调整 Opus 4.6 努力程度 |
| `/effort` | 直接设置努力程度：`low`、`medium`、`high`（v2.1.76+） |
| `/config` | 交互式配置 UI |
| `/memory` | 查看/编辑所有记忆文件 |
| `/agents` | 管理子代理 |
| `/mcp` | 管理 MCP 服务器 |
| `/hooks` | 查看已配置的钩子 |
| `/plugin` | 管理插件 |
| `/keybindings` | 配置自定义键盘快捷键 |
| `/skills` | 查看和管理技能 |
| `/permissions` | 查看和管理权限规则 |
| `--doctor` | 诊断配置问题 |
| `--debug` | 带钩子执行详情的调试模式 |

---

## 快速参考：完整示例

```json
{
  "$schema": "https://json.schemastore.org/claude-code-settings.json",
  "model": "sonnet",
  "agent": "code-reviewer",
  "language": "english",
  "cleanupPeriodDays": 30,
  "autoUpdatesChannel": "stable",
  "alwaysThinkingEnabled": true,
  "showThinkingSummaries": true,
  "viewMode": "default",
  "includeGitInstructions": true,
  "defaultShell": "bash",
  "plansDirectory": "./plans",
  "effortLevel": "medium",

  "worktree": {
    "symlinkDirectories": ["node_modules"],
    "sparsePaths": ["packages/my-app", "shared/utils"]
  },

  "modelOverrides": {
    "claude-opus-4-6": "arn:aws:bedrock:us-east-1:123456789:inference-profile/anthropic.claude-opus-4-6-v1:0"
  },

  "autoMode": {
    "environment": [
      "Source control: github.example.com/acme-corp and all repos under it",
      "Trusted internal domains: *.internal.example.com"
    ]
  },

  "permissions": {
    "allow": [
      "Edit(*)",
      "Write(*)",
      "Bash(npm run *)",
      "Bash(git *)",
      "WebFetch(domain:*)",
      "mcp__*",
      "Agent(*)"
    ],
    "deny": [
      "Read(.env)",
      "Read(./secrets/**)"
    ],
    "additionalDirectories": ["../shared/"],
    "defaultMode": "acceptEdits"
  },

  "enableAllProjectMcpServers": true,

  "sandbox": {
    "enabled": true,
    "excludedCommands": ["git", "docker"],
    "filesystem": {
      "denyRead": ["./secrets/"],
      "denyWrite": ["./.env"]
    }
  },

  "attribution": {
    "commit": "Generated with Claude Code",
    "pr": ""
  },

  "statusLine": {
    "type": "command",
    "command": "git branch --show-current"
  },

  "spinnerTipsEnabled": true,
  "spinnerTipsOverride": {
    "tips": ["自定义提示 1", "自定义提示 2"],
    "excludeDefault": false
  },
  "prefersReducedMotion": false,

  "env": {
    "NODE_ENV": "development",
    "CLAUDE_CODE_EFFORT_LEVEL": "medium"
  }
}
```

---

## 来源

- [Claude Code 设置文档](https://code.claude.com/docs/en/settings)
- [Claude Code 设置 JSON Schema](https://json.schemastore.org/claude-code-settings.json)
- [Claude Code 变更日志](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md)
- [Claude Code GitHub 设置示例](https://github.com/feiskyer/claude-code-settings)
- [Shipyard - Claude Code CLI 速查表](https://shipyard.build/blog/claude-code-cheat-sheet/)
- [Claude Code 环境变量参考](https://code.claude.com/docs/en/env-vars)
- [Claude Code 权限参考](https://code.claude.com/docs/en/permissions)
