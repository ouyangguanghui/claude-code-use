# 验证清单 —— README CONCEPTS 部分

验证 CONCEPTS 表格准确性的规则。每次工作流运行时都会检查所有规则。

## 规则

### 1. 外部 URL 有效性
- **分类**: URL 准确性
- **检查内容**: CONCEPTS 表格中的每个外部 URL（文档链接）都返回有效页面
- **深度**: 获取每个 URL 并确认加载了预期页面（而非重定向到错误页面）
- **对比来源**: `https://code.claude.com/docs/llms.txt` 获取规范 URL 列表
- **添加日期**: 2026-03-02
- **来源**: 发现权限 URL `/iam` 重定向到认证页面而非权限页面

### 2. 锚点片段有效性
- **分类**: URL 准确性
- **检查内容**: 任何带有锚点片段（`#section-name`）的 URL 都匹配目标页面上的实际标题
- **深度**: 获取页面并验证标题存在且锚点正确
- **对比来源**: 获取的页面内容
- **添加日期**: 2026-03-02
- **来源**: Rules 锚点 `#modular-rules-with-clauderules` 已过时；章节重命名为 `#organize-rules-with-clauderules`

### 3. 缺失的文档页面
- **分类**: 缺失概念
- **检查内容**: 官方文档索引（`llms.txt`）中代表面向用户功能的每个页面都在 CONCEPTS 表格中有对应行
- **深度**: 将完整文档索引与 CONCEPTS 表格条目进行比较
- **对比来源**: `https://code.claude.com/docs/llms.txt`
- **添加日期**: 2026-03-02
- **来源**: 发现多个缺失概念（Agent Teams、Keybindings、Model Configuration 等）

### 4. 本地徽章链接有效性
- **分类**: 徽章准确性
- **检查内容**: CONCEPTS 表格中的每个徽章目标路径（`best-practice/*.md`、`implementation/*.md`、`.claude/*/`）指向存在的文件或目录
- **深度**: 使用 Read/Glob 验证文件存在性
- **对比来源**: 本地文件系统
- **添加日期**: 2026-03-02
- **来源**: 初始清单创建

### 5. 描述时效性
- **分类**: 描述准确性
- **检查内容**: 每个概念的描述准确反映当前官方文档描述
- **深度**: 将 README 描述与官方页面的元描述或第一段进行比较
- **对比来源**: 官方文档页面内容
- **添加日期**: 2026-03-02
- **来源**: Memory 描述缺少 auto memory；MCP Servers 位置缺少 `.mcp.json`

### 6. TIPS 部分 URL 一致性
- **分类**: URL 准确性
- **检查内容**: 当 CONCEPTS 或 Hot 表格中的 URL 被更新时，同时检查 TIPS 部分是否存在相同的过期 URL
- **深度**: 搜索 TIPS 部分（第 125-267 行）中是否存在 CONCEPTS/Hot 表格中标记的 URL
- **对比来源**: llms.txt 站点地图 + CONCEPTS 表格 URL
- **添加日期**: 2026-04-16
- **来源**: `web-scheduled-tasks` URL 在 Hot 表格中已修复（2026-04-14），但相同的过期 URL 仍存在于 TIPS 中（第 223 行）
