# 跨模型（Claude Code + Codex）工作流

基于 [claude-code-best-practice](https://github.com/shanraisshan/claude-code-best-practice) 和 [codex-cli-best-practice](https://github.com/shanraisshan/codex-cli-best-practice)

## 工作流

```
┌─────────────────────────────────────────────────────────────────────────┐
│              跨模型 CLAUDE CODE + CODEX 工作流                          │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  步骤 1: 规划                                          Claude Code      │
│  ─────────────                                         Opus 4.6         │
│  在计划模式下打开 Claude Code（终端 1）。               Plan Mode        │
│  Claude 通过 AskUserQuestion 采访你。                                   │
│  生成带有测试门控的分阶段计划。                                          │
│                                                                         │
│  输出: plans/{feature-name}.md                                          │
│                                                                         │
│                              ▼                                          │
│                                                                         │
│  步骤 2: QA 审查                                       Codex CLI        │
│  ──────────────────                                    GPT-5.4          │
│  在另一个终端打开 Codex CLI（终端 2）。                                  │
│  Codex 对照实际代码库审查计划。                                          │
│  插入中间阶段（"Phase 2.5"）                                            │
│  并添加 "Codex Finding" 标题。                                          │
│  在计划中追加内容 —— 从不重写原有阶段。                                  │
│                                                                         │
│  输出: plans/{feature-name}.md（已更新）                                 │
│                                                                         │
│                              ▼                                          │
│                                                                         │
│  步骤 3: 实现                                          Claude Code      │
│  ──────────────────                                    Opus 4.6         │
│  启动新的 Claude Code 会话（终端 1）。                                   │
│  你逐阶段实现                                                           │
│  每个阶段都有测试门控。                                                  │
│                                                                         │
│                              ▼                                          │
│                                                                         │
│  步骤 4: 验证                                          Codex CLI        │
│  ────────────────                                      GPT-5.4          │
│  启动新的 Codex CLI 会话（终端 2）。                                     │
│  Codex 对照计划验证实现。                                                │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

## 跨模型工作流在生产中的实际样子

![跨模型工作流](assets/cross-model-workflow.png)

*最后更新：2026-03-06*
