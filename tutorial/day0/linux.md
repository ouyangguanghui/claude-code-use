# Linux 设置

[返回第 0 天](README.md)

## 前置条件

你需要 **Node.js v18 或更高版本** 和 **npm**。

## 步骤 1：安装 Node.js

### 选项 A：通过 nodejs.org 下载页面使用 fnm（推荐）

**fnm**（Fast Node Manager）是 Node.js 官方推荐的工具。它快速、轻量，并且在以后需要时可以轻松切换 Node 版本。

1. 打开浏览器，访问 [nodejs.org/en/download](https://nodejs.org/en/download)。

2. 你会看到一行下拉框，显示：**"Get Node.js® vXX.XX.X (LTS) for __ using __ with __"**。设置下拉框如下：

   | 下拉框 | 选择 |
   |--------|------|
   | Version | **vXX.XX.X (LTS)** — 保持默认的 LTS 版本，不要更改 |
   | OS | **Linux** |
   | Package Manager | **fnm**（在 "Recommended (Official)" 下） |
   | Package Format | **npm** — 保持默认 |

3. 页面会显示你需要运行的确切命令。打开终端并复制粘贴它们。大致如下：

   ```bash
   # 步骤 1 — 安装 fnm
   curl -fsSL https://fnm.vercel.app/install | bash

   # 步骤 2 — 重启终端或重新加载 shell 配置
   source ~/.bashrc   # 或者: source ~/.zshrc (如果你用 zsh)

   # 步骤 3 — 安装 Node.js
   fnm install 24   # 页面会显示确切的版本号
   ```

   > 版本号可能与上面不同 — 始终使用网站上显示的版本。

4. **关闭并重新打开终端**（或运行上面的 `source` 命令），使 `fnm`、`node` 和 `npm` 可用。

> **为什么选择 fnm？** 它在 Node.js 下载页面的 "Recommended (Official)" 分类中。像 nvm 一样，它将 Node 安装到你的主目录中，所以你永远不需要 `sudo` 来进行 npm 全局安装 — 但 fnm 明显更快（用 Rust 编写）且在 Windows、macOS 和 Linux 上工作方式相同。

### 选项 B：使用发行版的包管理器

这种方式更快，但可能安装较旧版本的 Node.js。**安装后检查版本** — 如果低于 v18，请使用选项 A。

**Ubuntu / Debian：**

```bash
sudo apt update
sudo apt install -y nodejs npm

# 检查版本
node --version   # 必须是 v18 或更高
```

**Fedora：**

```bash
sudo dnf install -y nodejs npm
```

**Arch Linux：**

```bash
sudo pacman -S nodejs npm
```

### 选项 C：NodeSource（通过 apt 获取最新 LTS，不使用 nvm）

适用于想要不使用 nvm 就获得最新 LTS 的 Ubuntu/Debian 用户：

```bash
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs
```

## 步骤 2：验证 Node.js

```bash
node --version
npm --version
```

两者都应打印版本号。`node --version` 必须显示 v18.x 或更高。

## 步骤 3：安装 Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

> **权限错误？**
> - 如果你使用了 **fnm** 或 **nvm**：这不应该发生。检查它是否已激活（`which node` 应指向你主目录内的路径，而非 `/usr/...`）。
> - 如果你使用了系统安装：可以使用 `sudo npm install -g @anthropic-ai/claude-code`，或修复 npm 全局目录权限：
>   ```bash
>   mkdir -p ~/.npm-global
>   npm config set prefix '~/.npm-global'
>   echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
>   source ~/.bashrc
>   ```

## 步骤 4：验证 Claude Code

```bash
claude --version
```

你应该看到 Claude Code 版本号打印出来。现在返回 [README.md](README.md) 进行身份验证设置。

---

## 注意事项

- **WSL（Windows Subsystem for Linux）：** 本指南在 WSL 中也适用。只需在 WSL 终端中按照这些步骤操作即可。
- **PATH 问题：** 如果安装后找不到 `claude`，确保 npm 的全局 bin 目录在你的 PATH 中。运行 `npm config get prefix` — 该路径的 `bin/` 子目录需要在你的 PATH 中。
