# Claude Code：用量、速率限制和额外用量

了解 Claude Code 中用量限制的工作方式以及如何在达到限制时继续工作。

[← 返回 Claude Code 最佳实践](../)

---

## 概述

订阅计划（Pro、Max 5x、Max 20x）上的 Claude Code 有滚动窗口重置的用量限制。三个内置斜杠命令帮助你监控和管理用量：

| 命令 | 描述 | 适用对象 |
|------|------|---------|
| `/usage` | 检查计划限制和速率限制状态 | Pro、Max 5x、Max 20x |
| `/extra-usage` | 配置达到限制时的按需溢出付费 | Pro、Max 5x、Max 20x |
| `/cost` | 显示当前会话的 token 用量和花费 | API 密钥用户 |

---

## `/usage` — 检查你的限制

显示当前计划的用量限制和速率限制状态。适合在达到限制前检查剩余容量。

---

## `/extra-usage` — 超出限制后继续工作

`/extra-usage` 命令配置**按需溢出计费**，使 Claude Code 在你达到计划的速率限制时无缝继续工作，而不是阻止你。

### 工作原理

1. 你达到了计划的速率限制（限制每 5 小时重置）
2. 如果启用了额外用量且有可用资金，Claude Code 不间断地继续
3. 溢出的 token 按**标准 API 费率**计费，与订阅费用分开

### 设置方法

CLI 中的 `/extra-usage` 命令会引导你完成配置。你也可以在 claude.ai 的 **Settings > Usage** 网页上配置：

1. 启用额外用量
2. 添加支付方式
3. 设置**月度消费上限**（或选择无限制）
4. 可选择添加**预付资金**，在余额低于阈值时自动充值

### 关键细节

| 细节 | 值 |
|------|-----|
| 每日兑换限额 | $2,000/天 |
| 计费 | 与订阅分开，按标准 API 费率 |
| 限制重置窗口 | 每 5 小时 |

### 已知问题

截至 2026 年 2 月，`/extra-usage` CLI 命令[未被文档记录](https://github.com/anthropics/claude-code/issues/12396)，可能会打开一个没有清晰配置选项的登录窗口。目前通过 **claude.ai 网页界面**配置是更可靠的方式。

---

## `/cost` — 会话花费（API 用户）

对于使用 API 密钥（非订阅计划）认证的用户，`/cost` 显示：

- 当前会话的总费用
- API 时长和墙钟时间
- Token 用量明细
- 代码更改

此命令与 Pro/Max 订阅用户无关。

---

## 快速模式与额外用量

快速模式（`/fast`）使用带更快输出的 Claude Opus 4.6。它与额外用量有特殊的计费关系：

- 快速模式的使用从第一个 token 起就**始终计入额外用量**
- 即使你的订阅计划还有剩余用量也是如此
- 快速模式不消耗你计划包含的速率限制

这意味着你需要启用并充值额外用量才能使用 `/fast`。

---

## CLI 启动标志

两个启动标志与用量预算相关（仅限 API 密钥用户，打印模式）：

| 标志 | 描述 |
|------|------|
| `--max-budget-usd <AMOUNT>` | API 调用在停止前的最大金额 |
| `--max-turns <NUMBER>` | 限制代理轮次数量 |

完整列表请参见 [CLI 启动标志参考](claude-cli-startup-flags.md)。

---

## 来源

- [付费 Claude 计划的额外用量 — Claude 帮助中心](https://support.claude.com/en/articles/12429409-extra-usage-for-paid-claude-plans)
- [使用 Pro 或 Max 计划的 Claude Code — Claude 帮助中心](https://support.claude.com/en/articles/11145838-using-claude-code-with-your-pro-or-max-plan)
- [/extra-usage 斜杠命令未被文档记录 — GitHub Issue #12396](https://github.com/anthropics/claude-code/issues/12396)
- [Claude Code CLI 参考](https://code.claude.com/docs/en/cli-reference)
