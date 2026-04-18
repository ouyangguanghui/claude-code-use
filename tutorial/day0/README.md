# 第 0 天 — Claude Code 设置

本指南引导你在机器上安装 Claude Code 并完成身份验证，以便你可以开始使用它。

## 步骤 1：安装 Claude Code

选择你的操作系统：

| 操作系统 | 指南 |
|----------|------|
| Windows | [windows.md](windows.md) |
| Linux | [linux.md](linux.md) |
| macOS | [mac.md](mac.md) |

按照你的操作系统指南操作，然后返回这里进行身份验证。

---

## 步骤 2：验证安装

按照操作系统特定指南操作后，确认一切正常：

```bash
node --version    # 应显示 v18.x 或更高版本
claude --version  # 应显示已安装的 Claude Code 版本
```

---

## 步骤 3：登录

<img src="assets/login.png" alt="Claude Code 登录界面" width="50%">

在终端中运行 `claude`。首次启动时，它会要求你选择登录方式。

### 方式 1：订阅（Claude Pro / Max）

- 选择 **Claude.ai account**
- 浏览器打开 — 登录并授权
- 返回终端，你已登录

### 方式 2a：API 密钥（团队邀请）

团队管理员从 Anthropic 控制台邀请你。

- 你会收到一封**邀请邮件** — 接受并创建你的 Anthropic 账户
- 在终端中运行 `claude`
- 选择 **Anthropic API Key**
- 你的密钥在控制台上**自动生成** — 无需手动设置
- Claude Code 立即开始工作

### 方式 2b：API 密钥（你已有密钥）

如果有人通过 Slack、邮件等方式分享了密钥给你，或者你自己创建了密钥：

- 在终端中运行 `claude`
- 选择 **Anthropic API Key**
- 粘贴你的密钥（以 `sk-ant-` 开头）
- 密钥会被**永久存储** — 你不会再被要求输入

---
