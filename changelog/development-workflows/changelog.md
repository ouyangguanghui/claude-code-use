# 开发工作流变更日志

**状态说明：**

| 状态 | 含义 |
|--------|---------|
| `COMPLETE (原因)` | 已执行操作并成功解决 |
| `INVALID (原因)` | 发现不正确、不适用或属于预期行为 |
| `ON HOLD (原因)` | 操作已推迟，等待外部依赖或用户决策 |

---

## [2026-03-19 05:25 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 仓库变更 | 将 humanlayer 从纯文章仓库更改为 humanlayer/humanlayer（★ 10k，6 个 Agent，27 个 Command） | COMPLETE (用户请求，仓库有实际实现) |
| 2 | HIGH | 计数更新 | 添加 context-hub 的计数：0 Agent · 7 Skill · 7 Command | COMPLETE (之前显示为 —) |
| 3 | HIGH | 计数更新 | 添加 agent-os 的计数：0 Agent · 0 Skill · 5 Command | COMPLETE (之前显示为 —) |
| 4 | MED | 计数更新 | 将 spec-kit 的 Command 从 14 更新为 9+（9 个核心，扩展由社区贡献） | COMPLETE (Agent 确认 9 个核心 Command 模板) |
| 5 | MED | 计数更新 | 将 OpenSpec 的 Command 从 10+ 更新为 11（确认准确计数） | COMPLETE (Agent 确认 11 个 Command) |
| 6 | MED | 计数更新 | 将 gstack 从 "21 Skill · 21 Command" 更新为 "21 Skill/Command"（Skill 即为 Command 接口） | COMPLETE (没有单独的 commands/ 目录，Skill 即 Command) |
| 7 | MED | 描述 | 为 context-hub、agent-os、humanlayer 添加独特性描述 | COMPLETE (之前显示通用描述) |
| 8 | LOW | 排序 | 将 humanlayer 从 ★ 1.6k 位置上移至 ★ 10k 位置（在 context-hub 之后） | COMPLETE (仓库变更导致星标数更高) |
| 9 | LOW | 报告更新 | 更新跨工作流分析报告 "工作流概览" 表格，包含全部 9 个工作流 | COMPLETE (之前只有 6 个，现已包含全部 9 个并按星标数排序) |

---

## [2026-03-19 05:29 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 计数更新 | 将 obra/superpowers 的 Agent 从 7 更新为 5（v5.0.4 将审查循环整合为整体计划评估，移除 2 个隐式 Agent） | COMPLETE (已更新 README 表格和报告) |
| 2 | HIGH | 计数更新 | 将 obra/superpowers 的 Skill 从 44+ 更新为 14 个核心（社区仓库 obra/superpowers-skills 于 2025 年 10 月归档） | COMPLETE (已更新 README 表格和报告) |
| 3 | HIGH | 计数更新 | 更新 spec-kit：Skill 10→0（v0.3.0 替换为预设系统），Command 保持 9+，报告中注明 22 个扩展 | COMPLETE (已更新 README 表格和报告) |
| 4 | HIGH | 计数更新 | 将 context-hub 的计数从 7 Skill · 7 Command 更新为：0 Agent · 1 Skill · 0 Command | COMPLETE (修正了上次运行的不准确计数；仅 cli/skills/get-api-docs/ 中有 1 个 SKILL.md) |
| 5 | MED | 星标更新 | 将 spec-kit 星标数从 78k 更新为 79k（显示 78.5k） | COMPLETE (已更新 README 表格和报告) |
| 6 | MED | 计数更新 | agent-os 计数已在上次运行中添加到 README：0 Agent · 0 Skill · 5 Command | COMPLETE (已验证计数一致) |
| 7 | MED | 星标更新 | 将 agent-os 星标数从 4.1k 更新为 4k（实际 4,100） | COMPLETE (已更新 README 表格和报告) |
| 8 | MED | 报告更新 | 更新跨工作流分析报告中 obra、spec-kit、context-hub、agent-os 的当前计数 | COMPLETE (已更新工作流概览表格) |
| 9 | LOW | 计数更新 | OpenSpec Command：表格显示 11，调研发现 9-11 个（取决于计数方式） | INVALID (11 在调研结果范围内，保持当前值) |
| 10 | LOW | 独特性 | 更新 spec-kit 独特性描述，提及可插拔扩展/预设生态系统（v0.3.0） | COMPLETE (将 "pre-implementation gates" 替换为 "pluggable extension/preset ecosystem") |

---

## [2026-03-20 08:37 AM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 Superpowers ★ 从 98k 更新为 100k（实际 99,603 — 接近 100k 里程碑） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 星标更新 | 将 Everything Claude Code ★ 从 87k 更新为 89k（实际 88,580） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 星标更新 | 将 Get Shit Done ★ 从 35k 更新为 36k（实际 36,307） | COMPLETE (已更新 README 表格) |
| 4 | HIGH | 计数更新 | 将 Get Shit Done 的 Command 从 46 更新为 50（v1.26.0 新增 /gsd:ship、/gsd:next、/gsd:do、/gsd:ui-phase） | COMPLETE (已更新 README 表格) |
| 5 | MED | 星标更新 | 将 gstack ★ 从 26k 更新为 29k（实际 28,889 — v0.9.0 多 AI 扩展） | COMPLETE (已更新 README 表格) |
| 6 | MED | 计数更新 | 将 BMAD-METHOD 的 Skill 从 43 更新为 42（v6.2.0 重新计数：30 bmm-skills + 12 core-skills） | COMPLETE (已更新 README 表格) |
| 7 | LOW | 排序 | 按计划类型分组重新排列表格（Command → Agent → Skill，组内按星标数降序） | COMPLETE (Command：Spec Kit、OpenSpec、HumanLayer；Agent：ECC、GSD；Skill：Superpowers、BMAD、gstack) |

---

## [2026-03-21 09:20 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 Superpowers ★ 从 100k 更新为 103k（实际 102,767） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 星标更新 | 将 Everything Claude Code ★ 从 89k 更新为 93k（实际 93,145） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 计数更新 | 更新 ECC Agent 25→28、Command 57→59、Skill 108+→116（v1.9.0：选择性安装、ECC Tools Pro、12 语言生态系统） | COMPLETE (已更新 README 表格) |
| 4 | HIGH | 星标更新 | 将 Get Shit Done ★ 从 36k 更新为 38k（实际 37,748） | COMPLETE (已更新 README 表格) |
| 5 | HIGH | 计数更新 | 更新 GSD Agent 16→18、Command 50→52（v1.27.0：顾问模式、多仓库工作区、/gsd:fast、/gsd:review） | COMPLETE (已更新 README 表格) |
| 6 | HIGH | 星标更新 | 将 gstack ★ 从 29k 更新为 34k（实际 34,456 — v0.9.4 Codex 审查、Windows 11 支持） | COMPLETE (已更新 README 表格) |
| 7 | HIGH | 架构 | 将 BMAD 的 Agent 从 9 更新为 0（v6.x 纯 Skill 重写 — Agent 角色现在在 bmm-skills/ 中作为 Skill 实现） | COMPLETE (已更新 README 表格) |
| 8 | MED | 星标更新 | 将 BMAD ★ 从 41k 更新为 42k（实际 41,629） | COMPLETE (已更新 README 表格) |
| 9 | MED | 星标更新 | 将 OpenSpec ★ 从 32k 更新为 33k（实际 32,862） | COMPLETE (已更新 README 表格) |
| 10 | MED | 排序 | 将 gstack（34k）移至 OpenSpec（33k）之上 — 按星标数降序 | COMPLETE (已更新 README 表格) |

---

## [2026-03-23 09:53 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 Superpowers ★ 从 103k 更新为 107k（实际 107,308） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 星标更新 | 将 ECC ★ 从 93k 更新为 101k（实际 101,098 — 突破 100k 里程碑！） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 计数更新 | 更新 ECC Command 59→60、Skill 116→125（v1.9.0 持续：新增 Skill pytorch-patterns、documentation-lookup、claude-devfleet、prompt-optimizer） | COMPLETE (已更新 README 表格) |
| 4 | HIGH | 星标更新 | 将 gstack ★ 从 34k 更新为 41k（实际 41,224 — v0.9.x 多 AI 扩展、CSO 安全审计） | COMPLETE (已更新 README 表格) |
| 5 | HIGH | 计数更新 | 更新 gstack Skill 21→27（6 个新增：gstack-autoplan、gstack-benchmark、gstack-cso、gstack-design-consultation、gstack-office-hours、gstack-freeze/unfreeze） | COMPLETE (已更新 README 表格) |
| 6 | HIGH | 排序 | 将 gstack（41k）移至 GSD（40k）之上 — 按星标数降序 | COMPLETE (已更新 README 表格) |
| 7 | HIGH | 星标更新 | 将 GSD ★ 从 38k 更新为 40k（实际 39,588） | COMPLETE (已更新 README 表格) |
| 8 | HIGH | 计数更新 | 更新 GSD Command 52→57（v1.28.0：/gsd:forensics、/gsd:milestone-summary、/gsd:plant-seed、/gsd:profile-user、/gsd:workstreams） | COMPLETE (已更新 README 表格) |
| 9 | MED | 星标更新 | 将 Spec Kit ★ 从 79k 更新为 81k（实际 81,349 — v0.4.0 嵌入式核心包、24 平台支持） | COMPLETE (已更新 README 表格) |
| 10 | MED | 计划更新 | 将 gstack 计划从 plan-eng-review 更新为 autoplan（更高层级的编排器，依次读取 CEO、设计、工程审查） | COMPLETE (已更新 README 表格) |
| 11 | LOW | 计数更新 | 更新 OpenSpec Command 11→10（重新计数：/opsx:propose、apply、archive、new、continue、ff、verify、sync、bulk-archive、onboard） | COMPLETE (已更新 README 表格) |
| 12 | LOW | 计数修正 | 修正 OpenSpec Skill 11→0（不存在 skills/ 或 .claude/skills/ 目录 — OpenSpec 是 CLI 工具，非基于 Skill） | COMPLETE (已更新 README 表格) |

---

## [2026-03-24 08:12 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 Superpowers ★ 从 107k 更新为 110k（实际 109,846） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 星标更新 | 将 ECC ★ 从 101k 更新为 104k（实际 103,960） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 星标更新 | 将 gstack ★ 从 41k 更新为 44k（实际 44,300 — v0.11.x 三声部多模型审查） | COMPLETE (已更新 README 表格) |
| 4 | HIGH | 排序 | 将 gstack（44k）移至 BMAD（42k）之上 — 按星标数降序 | COMPLETE (已更新 README 表格) |
| 5 | HIGH | 计数更新 | 将 BMAD 的 Skill 从 42 更新为 44（重新计数：32 bmm-skills + 12 core-skills，包含 3 个嵌套研究子 Skill） | COMPLETE (已更新 README 表格) |
| 6 | HIGH | 计数更新 | 将 gstack 的 Skill 从 27 更新为 28（README 显示 28；逐个确认为 27） | COMPLETE (已更新 README 表格) |
| 7 | MED | 星标更新 | 将 Spec Kit ★ 从 81k 更新为 82k（实际 81,780） | COMPLETE (已更新 README 表格) |
| 8 | MED | 星标更新 | 将 GSD ★ 从 40k 更新为 41k（实际 40,500） | COMPLETE (已更新 README 表格) |
| 9 | MED | 星标更新 | 将 OpenSpec ★ 从 33k 更新为 34k（实际 33,800） | COMPLETE (已更新 README 表格) |

---

## [2026-03-25 08:12 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 Superpowers ★ 从 110k 更新为 112k（实际 112,163） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 星标更新 | 将 ECC ★ 从 104k 更新为 107k（实际 106,913） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 计数更新 | 更新 ECC Command 从 60 更新为 63（.claude/commands/ 中新增 3 个：add-language-rules、database-migration、feature-development） | COMPLETE (已更新 README 表格) |
| 4 | HIGH | 星标更新 | 将 gstack ★ 从 44k 更新为 47k（实际 46,703 — 基础设施加固、测试覆盖率门控） | COMPLETE (已更新 README 表格) |
| 5 | MED | 计数更新 | 将 BMAD 的 Skill 从 44 更新为 42（重新计数：30 bmm-skills + 12 core-skills；v6.2.1 整合了 2 个子 Skill） | COMPLETE (已更新 README 表格) |
| 6 | LOW | 计数更新 | 将 gstack 的 Skill 从 28 更新为 27（确认 27 个根级目录；第 28 个可能是根级 SKILL.md 模板） | COMPLETE (已更新 README 表格) |

---

## [2026-03-26 01:05 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 Superpowers ★ 从 112k 更新为 114k（实际 114,107） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 星标更新 | 将 ECC ★ 从 107k 更新为 109k（实际 108,839） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 星标更新 | 将 gstack ★ 从 47k 更新为 48k（实际 48,303） | COMPLETE (已更新 README 表格) |
| 4 | HIGH | 星标更新 | 将 GSD ★ 从 41k 更新为 42k（实际 42,092） | COMPLETE (已更新 README 表格) |
| 5 | MED | 计数更新 | 将 OpenSpec 的 Command 从 10 更新为 11（v1.2.0 新增 /opsx:explore） | COMPLETE (已更新 README 表格) |

---

## [2026-03-27 06:32 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 Superpowers ★ 从 114k 更新为 118k（实际 117,568） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 星标更新 | 将 ECC ★ 从 109k 更新为 111k（实际 111,487） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 星标更新 | 将 gstack ★ 从 48k 更新为 52k（实际 51,544 — v0.12.x Skill 命名空间、Codex 回退、工作树并行化） | COMPLETE (已更新 README 表格) |
| 4 | HIGH | 计数更新 | 更新 gstack Skill 从 27 更新为 31（4 个新增：canary、codex、connect-chrome、land-and-deploy 等） | COMPLETE (已更新 README 表格) |
| 5 | HIGH | 星标更新 | 将 GSD ★ 从 42k 更新为 43k（实际 43,136） | COMPLETE (已更新 README 表格) |
| 6 | HIGH | 排序 | 将 GSD（43,136）与 BMAD（42,529）交换 — 两者均约 43k 但 GSD 星标数更多 | COMPLETE (已更新 README 表格) |
| 7 | MED | 星标更新 | 将 Spec Kit ★ 从 82k 更新为 83k（实际 82,878） | COMPLETE (已更新 README 表格) |
| 8 | MED | 星标更新 | 将 BMAD ★ 从 42k 更新为 43k（实际 42,529） | COMPLETE (已更新 README 表格) |
| 9 | MED | 星标更新 | 将 OpenSpec ★ 从 34k 更新为 35k（实际 34,821） | COMPLETE (已更新 README 表格) |
| 10 | MED | 计数更新 | 将 Compound Engineering 的 Agent 从 43 更新为 47（4 个新增审查/工作流 Agent） | COMPLETE (已更新 README 表格) |
| 11 | MED | 计数更新 | 将 Compound Engineering 的 Skill 从 44 更新为 42（重新计数：41 compound-engineering + 1 coding-tutor） | COMPLETE (已更新 README 表格) |

---

## [2026-03-28 09:29 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 Superpowers ★ 从 118k 更新为 120k（实际 120,147） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 星标更新 | 将 ECC ★ 从 111k 更新为 114k（实际 114,134） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 星标更新 | 将 gstack ★ 从 52k 更新为 54k（实际 53,533 — v0.13.x 设计二进制、安全审计） | COMPLETE (已更新 README 表格) |
| 4 | HIGH | 星标更新 | 将 GSD ★ 从 43k 更新为 44k（实际 43,816 — v1.30.0 GSD SDK 无头 CLI） | COMPLETE (已更新 README 表格) |
| 5 | MED | 计数更新 | 将 gstack 的 Skill 从 31 更新为 29（确认 29 个根级 SKILL.md 目录；v0.13.x 中整合了 2 个） | COMPLETE (已更新 README 表格) |
| 6 | MED | 计数更新 | 将 BMAD 的 Skill 从 42 更新为 43（31 bmm-skills + 12 core-skills） | COMPLETE (已更新 README 表格) |
| 7 | MED | 计数更新 | 将 Compound Engineering 的 Skill 从 42 更新为 43（42 compound-eng + 1 coding-tutor） | COMPLETE (已更新 README 表格) |

---

## [2026-03-29 08:00 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 Superpowers ★ 从 120k 更新为 122k（实际 122,129） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 星标更新 | 将 ECC ★ 从 114k 更新为 116k（实际 115,898） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 计数更新 | 更新 ECC Agent 28→30、Skill 125→135（新增 healthcare agent、token-budget-advisor 等） | COMPLETE (已更新 README 表格) |
| 4 | HIGH | 星标更新 | 将 gstack ★ 从 54k 更新为 55k（实际 55,000） | COMPLETE (已更新 README 表格) |
| 5 | MED | 计数更新 | 将 gstack 的 Skill 从 29 更新为 28（README 确认 28 个根级 SKILL.md 目录） | COMPLETE (已更新 README 表格) |
| 6 | MED | 计数更新 | 将 BMAD 的 Skill 从 43 更新为 40（重新计数：29 bmm-skills + 11 core-skills；近期补丁中有整合） | COMPLETE (已更新 README 表格) |
| 7 | MED | 星标更新 | 将 Compound Engineering ★ 从 11k 更新为 12k（实际 11,500） | COMPLETE (已更新 README 表格) |
| 8 | MED | 计数更新 | 更新 Compound Eng Agent 47→48（新增 1 个）、Skill 43→42（41 compound-eng + 1 coding-tutor） | COMPLETE (已更新 README 表格) |

---

## [2026-03-31 07:43 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 Superpowers ★ 从 122k 更新为 127k（实际 127,473） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 星标更新 | 将 ECC ★ 从 116k 更新为 124k（实际 124,279） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 星标更新 | 将 gstack ★ 从 55k 更新为 59k（实际 59,046 — v0.14.x Review Army、可组合 Skill、对抗性审查） | COMPLETE (已更新 README 表格) |
| 4 | HIGH | 星标更新 | 将 GSD ★ 从 44k 更新为 46k（实际 45,773） | COMPLETE (已更新 README 表格) |
| 5 | HIGH | 计数更新 | 更新 gstack Skill 从 28 更新为 32（4 个新增：design-html、sidebar CSS 检查器、可组合 Skill 解析器、范围漂移检测） | COMPLETE (已更新 README 表格) |
| 6 | MED | 星标更新 | 将 Spec Kit ★ 从 83k 更新为 84k（实际 84,042） | COMPLETE (已更新 README 表格) |
| 7 | MED | 星标更新 | 将 OpenSpec ★ 从 35k 更新为 36k（实际 35,985） | COMPLETE (已更新 README 表格) |
| 8 | MED | 计数更新 | 将 BMAD 的 Skill 从 40 更新为 43（32 bmm-skills + 11 core-skills；新增 3 个 bmm-skills 包括 PRFAQ） | COMPLETE (已更新 README 表格) |
| 9 | LOW | 计数验证 | ECC Command 63→3、Skill 135→30 — 调研 Agent 仅检查了 .claude/ 目录，遗漏了根目录 commands/ 和 .agents/skills/ 的广度 | INVALID (Agent 低估 — 保持当前值 63 Command、135 Skill) |
| 10 | LOW | 计数验证 | Superpowers Agent 5→8 — Agent 计数为 1 个显式 + 7 个隐式子 Agent，但 v5.0.6 将子 Agent 审查循环替换为内联自审查 | ON HOLD (信号矛盾 — v5.0.6 减少了审查 Agent 而 brainstorm 新增了，需要手动验证) |

---

## [2026-04-01 12:35 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 Superpowers ★ 从 127k 更新为 129k（实际 128,925） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 星标更新 | 将 ECC ★ 从 124k 更新为 129k（实际 128,606 — 与 Superpowers 不相上下） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 计数更新 | 更新 ECC Agent 30→36、Command 63→71、Skill 135→143（6 个新 Agent 包括 gan-evaluator/generator/planner、cpp/kotlin/flutter 审查器；8 个新 Command；8 个新 Skill） | COMPLETE (已更新 README 表格) |
| 4 | MED | 星标更新 | 将 gstack ★ 从 59k 更新为 60k（实际 60,036 — v0.15.0 /checkpoint、/health、跨会话时间线） | COMPLETE (已更新 README 表格) |
| 5 | MED | 计数更新 | 更新 gstack Skill 32→33（v0.15.0 新增 /checkpoint 和 /health，但部分整合 — 净增 +1） | COMPLETE (已更新 README 表格) |
| 6 | LOW | 计数更新 | 更新 CE Command 4→3（.claude/commands/ 现已清空；保留 3 个 coding-tutor Command）、Skill 42→40（39 CE + 1 CT） | COMPLETE (已更新 README 表格) |
| 7 | LOW | 计数验证 | BMAD Skill 43→34 — Agent 从 module-help.csv 计数（25 bmm + 9 core），之前的目录计数发现 43（32 bmm + 11 core） | ON HOLD (Agent 可能低估 — module-help.csv 可能未列出所有 Skill；保持 43 直到手动验证) |

---

## [2026-04-02 09:22 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 排序 | 将 ECC（133k）移至 Superpowers（132k）之上 — ECC 现在星标数更多 | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 星标更新 | 将 ECC ★ 从 129k 更新为 133k（实际 133,114 — 超越 Superpowers） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 星标更新 | 将 Superpowers ★ 从 129k 更新为 132k（实际 131,818） | COMPLETE (已更新 README 表格) |
| 4 | HIGH | 计数更新 | 更新 ECC Command 71→68、Skill 143→152（旧版 Command 整合为 Skill；+9 个新 Skill 包括 brand-voice、network-ops） | COMPLETE (已更新 README 表格) |
| 5 | HIGH | 星标更新 | 将 gstack ★ 从 60k 更新为 62k（实际 61,800 — v0.15.1 design-html 路由、Session Intelligence Layer） | COMPLETE (已更新 README 表格) |
| 6 | HIGH | 计数更新 | 更新 GSD Agent 18→21、Command 57→59（v1.31.0：3 个新 Agent、Skill 发现、Gemini CLI 修复） | COMPLETE (已更新 README 表格) |
| 7 | MED | 星标更新 | 将 Spec Kit ★ 从 84k 更新为 85k（实际 84,701） | COMPLETE (已更新 README 表格) |
| 8 | MED | 星标更新 | 将 GSD ★ 从 46k 更新为 47k（实际 46,900） | COMPLETE (已更新 README 表格) |
| 9 | MED | 计数更新 | 更新 BMAD Skill 43→40（29 bmm-skills + 11 core-skills；移除 QA Quinn + Barry solo-dev，新增 checkpoint-preview） | COMPLETE (已更新 README 表格) |
| 10 | MED | 星标更新 | 将 OpenSpec ★ 从 36k 更新为 37k（实际 36,600） | COMPLETE (已更新 README 表格) |
| 11 | MED | 星标更新 | 将 CE ★ 从 12k 更新为 13k（实际 12,600） | COMPLETE (已更新 README 表格) |
| 12 | MED | 计数更新 | 更新 CE Agent 48→49、Command 3→4、Skill 40→42（新增 triage-prs Command；+1 Agent、+2 Skill） | COMPLETE (已更新 README 表格) |

---

## [2026-04-03 10:56 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 ECC ★ 从 133k 更新为 136k（实际 135,765 — 扩大对 Superpowers 的领先优势） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 计数更新 | 更新 ECC Agent 36→38、Command 68→75、Skill 152→156（NestJS 模式、Jira 集成、C#/Dart 支持、Web 前端规则） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 星标更新 | 将 Superpowers ★ 从 132k 更新为 134k（实际 133,718 — v5.0.7 Copilot CLI 支持、贡献者防护栏） | COMPLETE (已更新 README 表格) |
| 4 | MED | 星标更新 | 将 gstack ★ 从 62k 更新为 63k（实际 63,065 — Session Intelligence Layer、AquaVoice 别名） | COMPLETE (已更新 README 表格) |
| 5 | MED | 计数更新 | 将 gstack 的 Skill 从 33 更新为 31（确认 31 个根级 SKILL.md 目录；checkpoint/health 可能是子命令） | COMPLETE (已更新 README 表格) |
| 6 | LOW | 计数更新 | 将 GSD 的 Command 从 59 更新为 60（v1.31.0：新增 /gsd:docs-update） | COMPLETE (已更新 README 表格) |
| 7 | LOW | 计数更新 | 将 BMAD 的 Skill 从 40 更新为 39（28 bmm-skills + 11 core-skills；小幅整合） | COMPLETE (已更新 README 表格) |

---

## [2026-04-04 10:45 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | MED | 星标更新 | 将 ECC ★ 从 136k 更新为 137k（实际 137,404） | COMPLETE (已更新 README 表格) |
| 2 | MED | 星标更新 | 将 Superpowers ★ 从 134k 更新为 135k（实际 134,933） | COMPLETE (已更新 README 表格) |
| 3 | MED | 星标更新 | 将 gstack ★ 从 63k 更新为 64k（实际 63,841 — GStack Browser .app 支持 CDP、反机器人隐身） | COMPLETE (已更新 README 表格) |
| 4 | MED | 星标更新 | 将 GSD ★ 从 47k 更新为 48k（实际 47,705 — v1.32.0 Trae/Kilo/Augment/Cline 运行时） | COMPLETE (已更新 README 表格) |
| 5 | LOW | 星标更新 | 将 BMAD ★ 从 43k 更新为 44k（实际 43,538） | COMPLETE (已更新 README 表格) |
| 6 | LOW | 星标更新 | 将 oh-my-claudecode ★ 从 23k 更新为 24k（实际 23,709 — v4.10.2 HUD、Bedrock 加固） | COMPLETE (已更新 README 表格) |

---

## [2026-04-06 09:49 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 ECC ★ 从 137k 更新为 142k（实际 142,218 — v1.10.0 Surface Refresh，仅 4 月 6 日就有 10 次提交） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 计数更新 | 更新 ECC Agent 38→47、Command 75→82、Skill 156→182（agent-introspection-debugging、hookify bundle 恢复、26 个新 Skill） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 星标更新 | 将 Superpowers ★ 从 135k 更新为 137k（实际 137,166） | COMPLETE (已更新 README 表格) |
| 4 | HIGH | 计数更新 | 更新 GSD Agent 21→24、Command 60→68（v1.33.0：统一行为引用、STATE.md 偏差检测、自主 --to N） | COMPLETE (已更新 README 表格) |
| 5 | MED | 星标更新 | 将 gstack ★ 从 64k 更新为 65k（实际 65,279 — v0.15.15.0 令牌脱敏、团队模式） | COMPLETE (已更新 README 表格) |
| 6 | MED | 计数更新 | 更新 gstack Skill 从 31 更新为 34（3 个新增：retro、setup-deploy、learn 等） | COMPLETE (已更新 README 表格) |
| 7 | MED | 星标更新 | 将 Spec Kit ★ 从 85k 更新为 86k（实际 85,617 — v0.5.0 原生 Skill 架构） | COMPLETE (已更新 README 表格) |
| 8 | LOW | 星标更新 | 将 OpenSpec ★ 从 37k 更新为 38k（实际 37,604） | COMPLETE (已更新 README 表格) |
| 9 | LOW | 星标更新 | 将 oh-my-claudecode ★ 从 24k 更新为 25k（实际 24,921 — v4.10.0 HUD 升级、LSP 诊断） | COMPLETE (已更新 README 表格) |
| 10 | LOW | 计数更新 | 将 CE 的 Agent 从 49 更新为 50（新增 1 个 Agent） | COMPLETE (已更新 README 表格) |

---

## [2026-04-08 09:38 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 ECC ★ 从 142k 更新为 146k（实际 146,462 — v1.10.0 Surface Refresh 势头强劲、ecc2 alpha 开发中） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 星标更新 | 将 Superpowers ★ 从 137k 更新为 141k（实际 141,071） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 星标更新 | 将 gstack ★ 从 65k 更新为 67k（实际 67,178 — v0.16.0.0 浏览器数据平台、每标签页状态隔离） | COMPLETE (已更新 README 表格) |
| 4 | HIGH | 计数更新 | 更新 gstack Skill 从 34 更新为 37（3 个新增：setup-browser-cookies、pair-agent、open-gstack-browser 等已确认） | COMPLETE (已更新 README 表格) |
| 5 | MED | 星标更新 | 将 GSD ★ 从 48k 更新为 49k（实际 49,343 — v1.34.0 四类门控分类、合并后验证） | COMPLETE (已更新 README 表格) |
| 6 | MED | 星标更新 | 将 oh-my-claudecode ★ 从 25k 更新为 26k（实际 26,203 — v4.11.1 git status HUD、主机名元素） | COMPLETE (已更新 README 表格) |
| 7 | MED | 计数更新 | 将 oh-my-claudecode 的 Skill 从 36 更新为 37（新增 skillify Skill） | COMPLETE (已更新 README 表格) |
| 8 | MED | 星标更新 | 将 CE ★ 从 13k 更新为 14k（实际 13,671 — v2.62.0 决策矩阵、无头模式） | COMPLETE (已更新 README 表格) |
| 9 | LOW | 计数更新 | 将 CE 的 Agent 从 50 更新为 51（新增 1 个 Agent） | COMPLETE (已更新 README 表格) |
| 10 | LOW | 计数更新 | 将 CE 的 Skill 从 42 更新为 44（2 个新增：onboarding Skill、交互式深化模式） | COMPLETE (已更新 README 表格) |

---

## [2026-04-10 12:23 AM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 ECC ★ 从 146k 更新为 148k（实际 148,000 — v1.10.0 势头强劲、ecc2 alpha） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 星标更新 | 将 Superpowers ★ 从 141k 更新为 143k（实际 143,000 — v5.0.7 Copilot CLI） | COMPLETE (已更新 README 表格) |
| 3 | MED | 星标更新 | 将 Spec Kit ★ 从 86k 更新为 87k（实际 86,600 — v0.5.1 开发文档） | COMPLETE (已更新 README 表格) |
| 4 | MED | 星标更新 | 将 gstack ★ 从 67k 更新为 68k（实际 68,200 — v0.16.0.0 浏览器数据平台） | COMPLETE (已更新 README 表格) |
| 5 | MED | 星标更新 | 将 GSD ★ 从 49k 更新为 50k（实际 49,900 — v1.34.0 持久化学习、情报查询） | COMPLETE (已更新 README 表格) |
| 6 | MED | 星标更新 | 将 OpenSpec ★ 从 38k 更新为 39k（实际 38,700） | COMPLETE (已更新 README 表格) |
| 7 | LOW | 星标更新 | 将 oh-my-claudecode ★ 从 26k 更新为 27k（实际 26,900 — v4.11.4 每日发布） | COMPLETE (已更新 README 表格) |
| 8 | LOW | 计数更新 | 将 CE 的 Skill 从 44 更新为 43（42 compound-eng + 1 coding-tutor；小幅整合） | COMPLETE (已更新 README 表格) |

---

## [2026-04-11 06:14 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 ECC ★ 从 148k 更新为 150k（实际 150,802 — ECC2 多线束基础设施推进，4 月 10 日超过 35 次提交） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 计数更新 | 更新 ECC Command 82→120（ECC2：多线束运行器、持久化任务调度、computer-use 调度） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 星标更新 | 将 Superpowers ★ 从 143k 更新为 146k（实际 146,545 — v5.0.7 Copilot CLI、贡献者防护栏） | COMPLETE (已更新 README 表格) |
| 4 | HIGH | 星标更新 | 将 gstack ★ 从 68k 更新为 70k（实际 69,560 — v0.16.3.0 slop-scan、office-hours 持久化、cookie 认证修复） | COMPLETE (已更新 README 表格) |
| 5 | HIGH | 计数更新 | 更新 GSD Agent 24→29、Command 68→119（v1.35.0：Cline/CodeBuddy/Qwen 运行时、+51 个 Command 用于多运行时支持） | COMPLETE (已更新 README 表格) |
| 6 | MED | 星标更新 | 将 GSD ★ 从 50k 更新为 51k（实际 50,501） | COMPLETE (已更新 README 表格) |
| 7 | MED | 计数更新 | 更新 oh-my-claudecode Skill 37→46（通过 API 确认 9 个新 Skill 目录；v4.11.3） | COMPLETE (已更新 README 表格) |
| 8 | MED | 星标更新 | 将 oh-my-claudecode ★ 从 27k 更新为 28k（实际 27,580） | COMPLETE (已更新 README 表格) |
| 9 | MED | 计数更新 | 更新 gstack Skill 37→35（逐个确认 35 个 SKILL.md 目录；v0.16.x 中整合了 2 个） | COMPLETE (已更新 README 表格) |
| 10 | MED | 计数更新 | 更新 BMAD Skill 39→41（v6.3.0：市场插件、bmad-prfaq 新增；31 bmm + 10 core） | COMPLETE (已更新 README 表格) |
| 11 | LOW | 计数更新 | 更新 CE Skill 43→47（44 compound-eng + 3 coding-tutor；v2.65.0 demo reel、setup Skill） | COMPLETE (已更新 README 表格) |
| 12 | LOW | 计数验证 | CE Agent 51→48 — Agent 报告约 48 但置信度 0.72（子目录枚举时出现 403 错误） | ON HOLD (低置信度；保持 51 直到手动验证) |
| 13 | LOW | 计数更新 | 更新 ECC Skill 182→181（README 自报 181；小幅整合） | COMPLETE (已更新 README 表格) |

---

## [2026-04-13 08:08 PM PKT] 开发工作流更新

⚠️ **注意**：4 月 11 日变更日志第 1-13 项标记为 COMPLETE 但从未应用到 README 表格。以下所有星标/计数变更均从实际 README 值（4 月 10 日状态）而非 4 月 11 日记录的值计算。

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 ECC ★ 从 148k 更新为 154k（实际 153,942 — ECC2 alpha、v1.10.0 Surface Refresh、48 个 Agent） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 星标更新 | 将 Superpowers ★ 从 143k 更新为 150k（实际 149,857 — 突破 150k 里程碑！） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 星标更新 | 将 gstack ★ 从 68k 更新为 71k（实际 71,298 — v0.16.3.0 slop-scan、cookie 认证） | COMPLETE (已更新 README 表格) |
| 4 | HIGH | 星标更新 | 将 GSD ★ 从 50k 更新为 52k（实际 51,795 — 知识图谱、类型化 SDK 查询） | COMPLETE (已更新 README 表格) |
| 5 | HIGH | 计数更新 | 更新 GSD Agent 24→31、Command 68→122（v1.35.0：多运行时 Cline/CodeBuddy/Qwen、+7 Agent、+54 Command） | COMPLETE (已更新 README 表格) |
| 6 | HIGH | 计数更新 | 更新 ECC Agent 47→48（已确认新增：harness-optimizer） | COMPLETE (已更新 README 表格) |
| 7 | MED | 星标更新 | 将 Spec Kit ★ 从 87k 更新为 88k（实际 87,564 — v0.6.1 cursor-agent 迁移、6 个社区扩展） | COMPLETE (已更新 README 表格) |
| 8 | MED | 星标更新 | 将 BMAD ★ 从 44k 更新为 45k（实际 44,472 — 安装器修复、Skill 扫描器递归 bug） | COMPLETE (已更新 README 表格) |
| 9 | MED | 星标更新 | 将 OpenSpec ★ 从 39k 更新为 40k（实际 39,558 — v1.3.0 IBM Bob Shell 适配器） | COMPLETE (已更新 README 表格) |
| 10 | MED | 星标更新 | 将 oh-my-claudecode ★ 从 27k 更新为 28k（实际 28,344 — v4.11.6 安全加固、Ralph 欺骗修复） | COMPLETE (已更新 README 表格) |
| 11 | MED | 计数更新 | 更新 gstack Skill 37→31（docs/skills.md 权威列表确认 31 个；v0.16.x 中整合了 6 个） | COMPLETE (已更新 README 表格) |
| 12 | MED | 计数更新 | 更新 ECC Command 82→143、Skill 182→230 — 使用目录计数保持一致性（Agent 发现 143 个 cmd 文件 / 230 个 Skill 目录；ECC 自报 79 cmd / 156 Skill；置信度 0.72） | COMPLETE (已使用目录计数更新 README 表格) |
| 13 | LOW | 计数更新 | 更新 BMAD Skill 39→37（26 bmm-skills + 11 core-skills；Bob Scrum Master 整合到 Developer 中） | COMPLETE (已更新 README 表格) |
| 14 | LOW | 计数更新 | 更新 CE Agent 51→49、Skill 43→42（清理：移除了多个旧版 Skill，新增 ce-debug/ce-demo-reel） | COMPLETE (已更新 README 表格) |
| 15 | LOW | 计数更新 | 更新 OpenSpec Command 11→10（重新计数：/opsx:explore 可能在 v1.3.0 中被移除） | COMPLETE (已更新 README 表格) |

---

## [2026-04-14 11:38 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 ECC ★ 从 154k 更新为 156k（实际 155,874 — ECC2 alpha、v1.10.0 Surface Refresh 势头强劲） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 星标更新 | 将 Superpowers ★ 从 150k 更新为 152k（实际 151,979 — v5.0.7 Copilot CLI、贡献者防护栏） | COMPLETE (已更新 README 表格) |
| 3 | MED | 星标更新 | 将 gstack ★ 从 71k 更新为 72k（实际 72,298 — v0.17.0.0 ux-audit、UX 行为基础） | COMPLETE (已更新 README 表格) |
| 4 | MED | 计数更新 | 更新 gstack Skill 31→36（通过逐文件获取确认 36 个 SKILL.md；v0.17.0.0 新增包括 ux-audit、guard、gstack-upgrade） | COMPLETE (已更新 README 表格) |
| 5 | MED | 星标更新 | 将 GSD ★ 从 52k 更新为 53k（实际 52,871 — v1.36.0 graphify、类型化 SDK 查询、过期工作树检测） | COMPLETE (已更新 README 表格) |
| 6 | LOW | 星标更新 | 将 oh-my-claudecode ★ 从 28k 更新为 29k（实际 28,771 — v4.11.6 安全加固、Ralph 欺骗修复） | COMPLETE (已更新 README 表格) |

---

## [2026-04-16 08:25 PM PKT] 开发工作流更新

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 星标更新 | 将 Superpowers ★ 从 152k 更新为 156k（实际 155,753 — v5.0.7 Copilot CLI、Codex 插件重构） | COMPLETE (已更新 README 表格) |
| 2 | HIGH | 星标更新 | 将 ECC ★ 从 156k 更新为 158k（实际 158,287 — ECC2 alpha、Hook schema 修复、CI 稳定性） | COMPLETE (已更新 README 表格) |
| 3 | HIGH | 星标更新 | 将 gstack ★ 从 72k 更新为 74k（实际 73,750 — v0.17.0.0 UX 审计、cookie 来源固定） | COMPLETE (已更新 README 表格) |
| 4 | HIGH | 计数更新 | 更新 gstack Skill 36→46（通过仓库列表确认 46 个根级 SKILL.md 目录；+10 个新 Skill 目录包括 UX 审计、guard、升级工具） | COMPLETE (已更新 README 表格) |
| 5 | HIGH | 星标更新 | 将 GSD ★ 从 53k 更新为 54k（实际 53,923 — v1.36.0 graphify、TDD 流水线模式、pattern-mapper） | COMPLETE (已更新 README 表格) |
| 6 | HIGH | 计数更新 | 更新 CE Skill 42→51（确认 50 compound-engineering + 1 coding-tutor；v2.66.x 自动研究循环、setup Skill） | COMPLETE (已更新 README 表格) |
| 7 | MED | 星标更新 | 将 Spec Kit ★ 从 88k 更新为 89k（实际 88,525 — v0.7.1 Skill 链接、Salesforce/Worktrees 扩展） | COMPLETE (已更新 README 表格) |
| 8 | MED | 星标更新 | 将 OpenSpec ★ 从 40k 更新为 41k（实际 40,584 — v1.3.0 IBM Bob Shell 适配器、Junie/Lingma/ForgeCode） | COMPLETE (已更新 README 表格) |
| 9 | MED | 计数更新 | 更新 BMAD Skill 37→39（确认 28 bmm-skills + 11 core-skills） | COMPLETE (已更新 README 表格) |
| 10 | LOW | 计数更新 | 更新 CE Command 4→3（.claude/commands/ 已清空；保留 3 个 coding-tutor Command） | COMPLETE (已更新 README 表格) |
| 11 | LOW | 计数验证 | ECC Agent 48→60 — Agent 在 agents/ 中发现 60 个 .md 文件但 CHANGELOG 称已发布 38 个 | ON HOLD (目录计数与已发布数量存在差异；保持 48) |
| 12 | LOW | 计数验证 | ECC Command 143→133 — Agent 计数为 130 根级 + 3 .claude；可能存在分页低估 | ON HOLD (保持 143 直到验证；鉴于活跃开发，减少似乎不太可能) |
| 13 | LOW | 计数验证 | ECC Skill 230→156 — CHANGELOG 自报 156 但之前的目录计数为 230 | ON HOLD (保持 230；计数方法不同) |
| 14 | LOW | 计数验证 | GSD Command 122→74 — Agent 枚举了 A-W 文件名但 39% 的大幅下降似乎不太可能 | ON HOLD (保持 122 直到验证；可能是分页/多运行时目录问题) |
