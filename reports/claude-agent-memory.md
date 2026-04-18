# Claude Code：代理记忆前置元数据

子代理的持久化记忆 — 使代理能够跨会话学习、记住和积累知识。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code 最佳实践</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## 概述

在 **Claude Code v2.1.33**（2026 年 2 月）中引入，`memory` 前置元数据字段为每个子代理提供了自己的基于 Markdown 的持久化知识存储。在此之前，每次代理调用都从零开始。

```yaml
---
name: code-reviewer
description: Reviews code for quality and best practices
tools: Read, Write, Edit, Bash
model: sonnet
memory: user
---

You are a code reviewer. As you review code, update your agent memory with
patterns, conventions, and recurring issues you discover.
```

---

## 记忆作用域

| 作用域 | 存储位置 | 版本控制 | 共享 | 最佳用途 |
|--------|---------|---------|------|---------|
| `user` | `~/.claude/agent-memory/<agent-name>/` | 否 | 否 | 跨项目知识（推荐默认值） |
| `project` | `.claude/agent-memory/<agent-name>/` | 是 | 是 | 团队应共享的项目特定知识 |
| `local` | `.claude/agent-memory-local/<agent-name>/` | 否（git-ignored） | 否 | 个人的项目特定知识 |

这些作用域与设置层级一致（`~/.claude/settings.json` → `.claude/settings.json` → `.claude/settings.local.json`）。

---

## 工作原理

1. **启动时**：`MEMORY.md` 的前 200 行被注入代理的系统提示中
2. **工具访问**：`Read`、`Write`、`Edit` 自动启用，使代理可以管理其记忆
3. **执行期间**：代理自由读写其记忆目录
4. **整理**：如果 `MEMORY.md` 超过 200 行，代理会将详细内容移到主题特定文件中

```
~/.claude/agent-memory/code-reviewer/     # user 作用域示例
├── MEMORY.md                              # 主文件（前 200 行被加载）
├── react-patterns.md                      # 主题特定文件
└── security-checklist.md                  # 主题特定文件
```

---

## 代理记忆 vs 其他记忆系统

| 系统 | 谁写入 | 谁读取 | 作用域 |
|------|--------|--------|--------|
| **CLAUDE.md** | 你（手动） | 主 Claude + 所有代理 | 项目 |
| **自动记忆** | 主 Claude（自动） | 仅主 Claude | 每项目每用户 |
| **`/memory` 命令** | 你（通过编辑器） | 仅主 Claude | 每项目每用户 |
| **代理记忆** | 代理自身 | 仅该特定代理 | 可配置（user/project/local） |

这些系统是**互补的** — 代理同时读取 CLAUDE.md（项目上下文）和自己的记忆（代理特定知识）。

---

## 实际示例

```yaml
---
name: api-developer
description: Implement API endpoints following team conventions
tools: Read, Write, Edit, Bash
model: sonnet
memory: project
skills:
  - api-conventions
  - error-handling-patterns
---

Implement API endpoints. Follow the conventions from your preloaded skills.
As you work, save architectural decisions and patterns to your memory.
```

这将**技能**（启动时的静态知识）与**记忆**（随时间积累的动态知识）相结合。

---

## 提示

- **提示使用记忆** — 包含明确指令：`"在开始之前，查看你的记忆。完成后，用你学到的内容更新你的记忆。"`
- 调用代理时**请求记忆检查**：`"审查这个 PR，并检查你的记忆中之前见过的模式。"`
- **选择正确的作用域** — `user` 用于跨项目，`project` 用于团队共享，`local` 用于个人

---

## 来源

- [创建自定义子代理 — Claude Code 文档](https://code.claude.com/docs/en/sub-agents)
- [管理 Claude 的记忆 — Claude Code 文档](https://code.claude.com/docs/en/memory)
- [Claude Code v2.1.33 发布说明](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md)
