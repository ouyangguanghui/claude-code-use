# Claude Code 从零到精通 — 视觉/VLA/机器人算法工程师实战指南

> 基于 [claude-code-best-practice](https://github.com/anthropics/claude-code-best-practice) 仓库整理。
> 本教程面向有 Python/PyTorch/ROS 经验的算法工程师，所有示例围绕 ML 训练、模型评估、数据处理和机器人开发场景。

---

## 阅读指南

**适用人群**：使用 Python、PyTorch、CUDA、ROS 等工具的视觉/VLA/机器人算法工程师，希望将 Claude Code 融入日常开发流程。

**标记说明**：
- **[实战]** — 机器人/CV/ML 场景下的具体操作示例
- **[专家提示]** — 来自 Claude Code 创建者 Boris Cherny 或 Anthropic 工程师 Thariq 的实战经验
- **[陷阱]** — 常见错误和避免方法
- **[参考]** — 本仓库中的详细文档链接

**如何阅读**：按顺序渐进阅读，或直接跳到感兴趣的部分。每部分独立成章，但 Part 2（CLAUDE.md）和 Part 3（上下文管理）是后续所有内容的基础。

---

## 目录

- [Part 0: 准备工作 — 安装与首次启动](#part-0-准备工作--安装与首次启动)
- [Part 1: 基础对话 — 15 分钟到首次生产力](#part-1-基础对话--15-分钟到首次生产力)
- [Part 2: CLAUDE.md — 项目记忆系统](#part-2-claudemd--项目记忆系统)
- [Part 3: 上下文管理 — 驾驭百万 Token 窗口](#part-3-上下文管理--驾驭百万-token-窗口)
- [Part 4: 命令系统 — 你的快捷操作](#part-4-命令系统--你的快捷操作)
- [Part 5: 技能系统 — 可复用的专业能力](#part-5-技能系统--可复用的专业能力)
- [Part 6: 子代理系统 — 分身术](#part-6-子代理系统--分身术)
- [Part 7: MCP 服务器 — 能力扩展](#part-7-mcp-服务器--能力扩展)
- [Part 8: 钩子系统 — 事件驱动自动化](#part-8-钩子系统--事件驱动自动化)
- [Part 9: 设置与配置 — 精细调控](#part-9-设置与配置--精细调控)
- [Part 10: 工作流编排 — 组合一切](#part-10-工作流编排--组合一切)
- [Part 11: 高级技巧 — 来自创建者的实战经验](#part-11-高级技巧--来自创建者的实战经验)
- [Part 12: 实战项目 — 从零配置一个机器人项目](#part-12-实战项目--从零配置一个机器人项目)
- [附录 A: 命令速查表](#附录-a-命令速查表)
- [附录 B: 前置元数据字段参考](#附录-b-前置元数据字段参考)
- [附录 C: 常见问题与故障排除](#附录-c-常见问题与故障排除)
- [附录 D: 本仓库文件索引](#附录-d-本仓库文件索引)

---

## Part 0: 准备工作 — 安装与首次启动

### 安装

各平台的详细安装步骤请参考：
- **Linux**：[tutorial/day0/linux.md](day0/linux.md) — 含 fnm、包管理器、NodeSource 三种方式
- **macOS**：[tutorial/day0/mac.md](day0/mac.md) — 通过 Homebrew 一键安装
- **Windows**：[tutorial/day0/windows.md](day0/windows.md) — 通过 npm 安装

安装后验证：

```bash
node --version    # 需要 v18+
claude --version  # 确认 Claude Code 已安装
```

### 三种认证方式

| 方式 | 适用场景 | 命令 |
|------|---------|------|
| Claude Pro/Max 订阅 | 个人开发者，通过 claude.ai 订阅 | `claude` → 浏览器登录 |
| 团队 API 密钥 | 实验室/团队配额 | 从管理员获取邀请链接 |
| 个人 API 密钥 | 按量付费 | 设置 `ANTHROPIC_API_KEY` 环境变量 |

### 首次启动

```bash
cd ~/your-robot-project
claude
```

Claude 会自动扫描当前目录，识别项目结构。如果项目根目录有 `CLAUDE.md`，它会被立即加载为项目上下文。

> **[参考]** 完整安装指南：[tutorial/day0/README.md](day0/README.md)

---

## Part 1: 基础对话 — 15 分钟到首次生产力

### 概念回顾

Claude Code 有三个层次的使用方式（详见 [tutorial/day1/README.md](day1/README.md)）：

1. **提示（Prompts）** — 直接对话，像问一个知识渊博的朋友
2. **代理（Agents）** — 聘请专家，保证用固定方法完成任务
3. **技能（Skills）** — 培训手册，可复用的专业能力模块

本部分聚焦第一层：如何通过自然语言对话快速获得生产力。

### 直接提问

最简单的用法 — 直接用自然语言问代码相关问题：

```
> 解释一下 PyTorch 的 DataParallel 和 DistributedDataParallel 的区别
> 写一个计算 mAP (mean Average Precision) 的函数
> 这个 loss 为什么会变成 NaN？
```

### @-文件引用：精确提供上下文

这是 Claude Code 最实用的基础功能之一。用 `@` 引用具体文件，Claude 会自动读取并理解其内容：

**[实战] 机器人/CV 场景**：

```
> @model/backbone.py 这个 Vision Transformer 的前向传播流程是什么？
> @scripts/train.py 为什么训练到第 50 个 epoch 后 loss 突然震荡？
> @ros_ws/src/perception/scripts/detector.py 这个 ROS 节点订阅了哪些话题？
> @cuda_kernels/nms.cu 解释这个 CUDA kernel 的 shared memory 使用方式
```

你还可以引用特定行范围：

```
> @model/policy.py:45-80 这段 action head 的设计有什么问题？
```

### 阅读和理解代码库

对于一个陌生的代码库，你可以让 Claude 帮你建立全局理解：

```
> 这个项目的整体架构是什么？画一个模块依赖关系图
> 训练流程的数据流向是怎样的？从数据加载到 loss 计算
> 找到所有注册了 ROS 服务的节点，列出服务名称和功能
```

**[专家提示]** 来自 Boris（Claude Code 创建者）：
> 启用 "Explanatory" 输出风格（`/config` 中设置），Claude 会解释每次修改背后的"为什么"。让 Claude 生成 HTML 幻灯片或 ASCII 图表来可视化不熟悉的架构 — 它做的出人意料地好。
> — *[tips/claude-boris-10-tips-01-feb-26.md](../tips/claude-boris-10-tips-01-feb-26.md) 第 10 条*

**[陷阱]** 不要直接问泛泛的问题（"这段代码有什么问题"），而要提供具体上下文（"@train.py 第 120 行的梯度裁剪阈值设为 0.1，但我用的是 transformer 模型，这个值是不是太小了？"）。上下文越具体，回答越准确。

### 首次 15 分钟工作流

如果你是第一次使用 Claude Code，按这个顺序操作：

```bash
# 1. 进入项目目录并启动
cd ~/your-robot-project
claude

# 2. 让 Claude 理解项目（~2 分钟）
> 这个项目的整体架构是什么？主要模块和数据流向

# 3. 让 Claude 创建 CLAUDE.md（~3 分钟）
> /init

# 4. 做一个具体的小任务（~5 分钟）
> @scripts/train.py 这个训练脚本支持混合精度训练吗？如果不支持，帮我加上

# 5. 检查 Claude 的工作
> /diff

# 6. 如果满意，让 Claude 提交
> 提交这些更改
```

### 多文件引用

你可以在一条消息中引用多个文件，Claude 会综合理解：

```
> @models/backbone.py @models/policy.py 这两个模块之间的数据维度是否对齐？
  backbone 输出的 feature 维度和 policy 期望的输入维度是否一致？

> @configs/train.yaml @configs/eval.yaml 训练和评估配置有哪些关键差异？
```

### 代码生成与修改

Claude 不只回答问题，还能直接修改代码：

```
> @models/vla.py 给这个模型添加 gradient checkpointing 支持，减少显存占用
> 写一个 pytest 测试文件，覆盖 data_loader.py 的核心功能
> 将 scripts/train.py 中所有的 print() 替换为 logging，使用 WARNING 级别
```

Claude 会直接编辑文件，你可以用 `/diff` 查看更改，不满意就 `Esc Esc` 回退。

---

## Part 2: CLAUDE.md — 项目记忆系统

### 为什么 CLAUDE.md 是最重要的一步

类比：Claude 是一个每天都失忆的高级工程师。他技术能力很强，但每次开始新会话时，对你的项目一无所知。`CLAUDE.md` 就是你写给他的"员工手册" — 每次他"上班"时都会先读一遍。

没有 CLAUDE.md，Claude 每次都要从头理解你的项目；有了好的 CLAUDE.md，Claude 一开始就知道：
- 项目用什么框架和约定
- 哪些文件不能动
- 常见的坑在哪里

### CLAUDE.md 应该写什么

| 分类 | 内容 | 示例 |
|------|------|------|
| 项目概览 | 一句话描述项目做什么 | "自主移动机器人的视觉导航系统" |
| 技术栈 | 框架、语言、关键依赖 | PyTorch 2.1, ROS2 Humble, CUDA 12.1 |
| 架构约定 | 代码组织方式 | "所有模型定义在 `models/`，训练脚本在 `scripts/`" |
| 训练约定 | 训练相关的关键参数 | 默认 batch size、学习率策略、多卡训练方式 |
| 数据约定 | 数据集格式和位置 | "数据集使用 COCO 格式，存放在 /data/" |
| 危险区域 | 不要修改的文件或函数 | "不要改 `data_loader.py` 的 `collate_fn`" |
| 常用命令 | 日常开发命令 | `python train.py --config configs/default.yaml` |

### [实战] 机器人视觉导航项目的 CLAUDE.md 模板

```markdown
# CLAUDE.md — 机器人视觉导航项目

## 项目概览
自主移动机器人的视觉导航系统，使用 VLA (Vision-Language-Action) 模型
将相机图像和语言指令映射为机器人动作序列。

## 技术栈
- Python 3.10, PyTorch 2.1, CUDA 12.1
- ROS2 Humble（通讯框架）
- Docker: robotics-dev:latest
- 训练集群: 4x A100 80GB

## 模型架构
- Backbone: ViT-B/16 (ImageNet pretrained)
- Language Encoder: CLIP text encoder (frozen)
- Policy Head: MLP with 256-dim action discretization
- 输出: 7-DoF action (3 translation + 4 quaternion rotation)

## 训练约定
- 使用 PyTorch DDP 多卡训练，不要用 DataParallel
- 默认 batch size: 64 per GPU
- 学习率: cosine schedule, peak 3e-4, warmup 1000 steps
- 梯度裁剪: max_norm=1.0
- 混合精度训练 (AMP) 默认开启

## 数据集
- 训练集: /data/train/ (~50K episodes, RLDS format)
- 验证集: /data/val/ (~5K episodes)
- 每个 episode 包含: images/, actions.npy, language_instruction.txt

## 关键约定
- 所有坐标使用右手坐标系（ROS 约定），Z 轴向上
- 图像预处理: resize to 224x224, normalize with ImageNet stats
- Action 空间已归一化到 [-1, 1]

## 不要修改
- data_loader.py 的 collate_fn — 处理了可变长度序列的 padding
- configs/base.yaml — 其他 config 继承自此文件
- ros_ws/src/hardware_interface/ — 硬件驱动层，改了会烧电机

## 常用命令
# 训练
torchrun --nproc_per_node=4 scripts/train.py --config configs/vla_base.yaml

# 评估
python scripts/eval.py --checkpoint outputs/latest/model.pt --episodes 100

# ROS 启动
ros2 launch robot_bringup navigation.launch.py

# Docker 环境
docker run --gpus all -v /data:/data -it robotics-dev:latest
```

### 加载机制：单仓库中的层级

```
/your-monorepo/
├── CLAUDE.md              ← 启动时立即加载（祖先加载）
├── perception/
│   ├── CLAUDE.md          ← 读取 perception/ 文件时才加载（后代延迟加载）
│   └── detection/
│       └── CLAUDE.md      ← 读取 detection/ 文件时才加载
├── planning/
│   └── CLAUDE.md          ← 在 perception/ 工作时不会加载（同级隔离）
└── control/
    └── CLAUDE.md
```

**关键规则**：
- **祖先目录**的 CLAUDE.md 在启动时**立即加载**
- **子目录**的 CLAUDE.md **延迟加载**，只在接触相关文件时才加载
- **同级目录**的 CLAUDE.md **互不干扰**

还有两个特殊位置：
- `~/.claude/CLAUDE.md` — 全局个人偏好（适用于所有项目）
- `CLAUDE.local.md` — 个人项目偏好（不提交到 git）

**[专家提示]** 来自 Boris：
> 每次 Claude 犯错后，以此结束对话："更新你的 CLAUDE.md 这样你就不会再犯同样的错误了。" Claude 非常擅长为自己编写规则。持续迭代直到错误率明显下降。
> — *[tips/claude-boris-10-tips-01-feb-26.md](../tips/claude-boris-10-tips-01-feb-26.md) 第 3 条*

**[参考]** [best-practice/claude-memory.md](../best-practice/claude-memory.md)

### CLAUDE.md 的迭代改进

CLAUDE.md 不是写一次就完事的 — 它应该持续迭代。最有效的改进方式：

**犯错后更新**：
```
> 更新你的 CLAUDE.md，确保以后不会再犯这个错误
```

Claude 会自己分析刚才的错误，添加防范规则。例如：
- 错误地用了 `DataParallel` → 添加 "多卡训练必须使用 DDP，不要用 DataParallel"
- 改了 `collate_fn` 导致 crash → 添加到"不要修改"列表
- 忘了 `model.eval()` → 添加 "评估前必须调用 model.eval()"

**使用 /memory 快速编辑**：
```
> /memory
```

这会直接打开 CLAUDE.md 进行编辑，不需要手动找文件。

### CLAUDE.local.md — 个人项目笔记

`CLAUDE.local.md` 存放你个人的偏好和笔记，**不提交到 git**（已在 .gitignore 中）：

```markdown
# CLAUDE.local.md

## 我的开发环境
- 使用 conda 环境: robotics-env
- GPU: RTX 4090 (24GB) — 比实验室的 A100 显存小，batch size 减半
- 习惯用 vim 风格的快捷键

## 我的偏好
- 代码风格偏好 type hints
- 测试时习惯用 pytest -xvs
- 调试时喜欢用 ipdb 而不是 pdb

## 当前工作
- 在调试 VLA 模型的 action head 精度问题
- 下周要提交 ICRA 论文的实验结果
```

`~/.claude/CLAUDE.md` 则是跨所有项目的全局偏好：

```markdown
# ~/.claude/CLAUDE.md

## 通用偏好
- 回答用中文
- 代码注释用英文
- 使用 type hints
- 优先使用函数式编程风格
```

### 控制 CLAUDE.md 大小

**[陷阱]** CLAUDE.md 太长（超过 200 行）时，Claude 的遵循度会下降。控制策略：

1. **拆分**：将详细规范放到子目录的 CLAUDE.md 中（利用延迟加载）
2. **精简**：删掉 Claude 已经知道的通用知识（如 "Python 用 4 空格缩进"）
3. **分层**：核心约束放根目录，模块细节放子目录

```
robot-nav/
├── CLAUDE.md              # 20 行：项目概览 + 核心约束
├── models/
│   └── CLAUDE.md          # 30 行：模型架构约定
├── scripts/
│   └── CLAUDE.md          # 20 行：训练/评估脚本约定
└── ros_ws/
    └── CLAUDE.md          # 25 行：ROS 开发约定
```

---

## Part 3: 上下文管理 — 驾驭百万 Token 窗口

### 什么是上下文窗口

上下文窗口是 Claude 的"短期记忆"。它包含了 Claude 在生成回复时能"看到"的所有内容：系统提示、对话历史、每次工具调用及结果、每个被读取的文件。Claude Code 的上下文窗口为 **100 万个 token**。

### 上下文腐化：隐形的性能杀手

随着上下文增长，Claude 的性能会下降 — 注意力分散在更多 token 上，旧的无关内容开始干扰当前任务。这种现象叫**上下文腐化**（context corruption），大约在 **30-40 万 token** 时开始出现。

类比：想象一张桌子（上下文窗口）。刚开始桌面很干净，你找东西很快。但随着你不断堆文件、笔记、外卖盒…… 到某个临界点，桌面太乱了，你反而找不到重要的东西。

### 查看上下文使用情况

```
> /context
```

这会显示当前 token 使用量和按来源的分解（系统提示 / 工具 / 文件 / 对话），帮你判断是否需要清理。

### 每一轮结束后的五个选择

这是 Thariq（Anthropic 工程师）的核心框架。每次 Claude 完成一轮回复后，你有五个选择：

| 选择 | 操作 | 保留的上下文 | 何时使用 |
|------|------|-------------|---------|
| **继续** | 直接发送下一条消息 | 全部保留 | 同一任务，上下文仍然相关 |
| **回退** | 双击 Esc 或 `/rewind` | 回退点之前全部保留 | Claude 走了错误路径 |
| **压缩** | `/compact [指引]` | Claude 自动总结的摘要 | 会话膨胀但需保持势头 |
| **新会话** | `/clear` | 只有你写的简要说明 | 开始真正的新任务 |
| **子代理** | "启动子代理去做 X" | 主上下文 + 子代理结论 | 下一步会产生大量中间噪音 |

### 回退而不是纠正 — 最重要的习惯

**[专家提示]** 来自 Thariq：
> 如果要选一个代表良好上下文管理的习惯，那就是**回退**。

**纠正**（在失败尝试后说"不，试试 B"）会把失败留在上下文中：
> 上下文 = 文件读取 + 2 次失败 + 2 次纠正 + 修复 → 噪音堆积

**回退**（回到失败之前，用学到的知识重新提示）更干净：
> 上下文 = 文件读取 + 一个知情的提示 + 修复 → 干净利落

操作方式：**双击 Esc**（或 `/rewind`），回到之前的消息，用学到的信息重新提示。

**[实战]** 调试训练脚本场景：
Claude 读了五个文件，建议修改 loss 函数来解决 NaN 问题，但实际原因是梯度裁剪。

❌ 纠正："那个方法不对，问题不是 loss 函数，是梯度裁剪"
✅ 回退：双击 Esc → "NaN 的原因是梯度裁剪阈值太大，不是 loss 函数。把 `max_norm` 从 10.0 改到 1.0"

### /compact vs /clear 的选择

| 场景 | 推荐 | 原因 |
|------|------|------|
| 调试了半小时，要继续同一个问题 | `/compact 专注于 NaN loss 的发现，忽略数据加载调试` | 低成本，保持势头 |
| 调试完毕，要开始写新功能 | `/clear` 然后简要说明 | 零腐化，精确控制上下文 |
| 探索了一个大型代码库，找到了关键信息 | `/clear` + 把发现写在新消息中 | 高风险操作前，用最干净的上下文 |

**[陷阱]** `/compact` 的质量取决于时机。自动压缩在上下文很满时触发 — 此时 Claude 处于"最不聪明"的状态（因为上下文已腐化）。建议在上下文占用 50% 左右时**主动** `/compact`，并附上指引告诉 Claude 关注什么。

### 子代理作为上下文管理工具

心理测试：**"我还会需要中间过程，还是只需要结论？"**

如果答案是"只需要结论"，就用子代理。例如：

```
> 启动一个子代理，读取 perception/ 目录的所有代码，总结模型架构和数据流向，我只需要最终的架构总结
```

子代理获得自己干净的上下文窗口，做完所有探索后，只有最终报告返回到你的主上下文。20 次文件读取、12 次搜索、3 个死胡同 — 全部被"垃圾回收"。

**[参考]** 完整的上下文管理指南：[tips/claude-thariq-tips-16-apr-26.md](../tips/claude-thariq-tips-16-apr-26.md)

### 上下文管理决策流程图

当你在会话中工作时，用这个流程来决定下一步：

```
Claude 完成一轮回复
       │
       ▼
  上下文还相关吗？
  ├── 是 → 继续对话
  └── 否 → ┐
            ▼
      需要保持势头吗？
      ├── 是 → /compact [保留什么的指引]
      └── 否 → /clear + 新的说明
```

```
Claude 走错了方向
       │
       ▼
  需要从新角度看问题吗？
  ├── 是 → 回退（Esc Esc）+ 更好的提示
  └── 否 → 纠正（"不，应该用 X"）
```

```
下一步会产生很多中间噪音
       │
       ▼
  我需要看到中间过程吗？
  ├── 是 → 直接在主对话中做
  └── 否 → 子代理（"启动子代理去做 X"）
```

### [实战] 训练脚本调试的完整上下文管理策略

**场景**：你在调试一个训练脚本，loss 在第 50 个 epoch 后变成 NaN。

```
# 第 1 阶段：探索（~5% 上下文）
> @scripts/train.py 训练到第 50 epoch 后 loss 变 NaN 了，可能的原因有哪些？

# Claude 列出 5 个可能原因，你发现梯度爆炸最可能

# 第 2 阶段：深入调查（~15% 上下文）
> 启动一个 Explore 子代理，搜索所有梯度裁剪相关的代码

# 子代理返回：只在 transformer 模块裁剪了，CNN backbone 没有

# 第 3 阶段：修复（~20% 上下文）
> 在 CNN backbone 的 optimizer step 前也加上梯度裁剪，max_norm=1.0

# 修复完成，验证通过

# 第 4 阶段：清理上下文
> /compact 专注于 NaN 修复方案：CNN backbone 需要梯度裁剪

# 现在上下文只有修复摘要，可以继续下一个任务
```

**关键节奏**：探索用子代理（隔离噪音）→ 修复在主对话（需要交互）→ 完成后 compact（清理上下文）。

---

## Part 4: 命令系统 — 你的快捷操作

### 什么是命令

命令是以 `/` 开头的快捷操作。Claude Code 有 **70+ 个内置命令**，你也可以创建自定义命令。

类比：命令就像你终端里的 alias — 一个 `/train-debug` 背后可能是一整套诊断流程。

### 最常用的内置命令

按使用频率分组，最推荐先掌握这些：

**日常必备**：
| 命令 | 功能 |
|------|------|
| `/context` | 查看上下文使用情况（token 占用分布） |
| `/compact [指引]` | 压缩上下文，可附指引 |
| `/clear` | 清空开始新会话 |
| `/rewind` | 回退到之前的消息（也可以双击 Esc） |
| `/diff` | 查看未提交的更改 |
| `/plan [描述]` | 进入计划模式 |
| `/model` | 切换模型 |
| `/effort [级别]` | 设置努力程度（low/medium/high/max） |

**诊断排错**：
| 命令 | 功能 |
|------|------|
| `/doctor` | 诊断安装和设置问题 |
| `/cost` | 查看 token 使用和费用 |
| `/usage` | 查看计划限额和速率状态 |
| `/powerup` | 发现隐藏功能的互动教程 |

**扩展管理**：
| 命令 | 功能 |
|------|------|
| `/init` | 初始化项目（创建 CLAUDE.md） |
| `/agents` | 管理代理配置 |
| `/skills` | 列出可用技能 |
| `/mcp` | 管理 MCP 服务器 |
| `/hooks` | 查看钩子配置 |
| `/memory` | 编辑 CLAUDE.md 记忆文件 |

**[参考]** 完整 70+ 命令列表：[best-practice/claude-commands.md](../best-practice/claude-commands.md)

### 创建自定义命令

自定义命令是 `.claude/commands/` 目录下的 `.md` 文件。

**[实战]** 创建一个训练调试命令：

文件：`.claude/commands/train-debug.md`

```yaml
---
description: 诊断 PyTorch 训练失败，检查 loss、梯度、显存
model: sonnet
allowed-tools: Bash(python *), Bash(nvidia-smi *), Read(*)
---

# 训练调试命令

当训练出现问题时运行此命令，按以下步骤排查：

## 检查步骤

1. **检查训练日志** — 搜索最近的日志文件中是否有 NaN、Inf 或异常的 loss 值
2. **检查 GPU 状态** — 运行 `nvidia-smi` 检查显存使用和 GPU 利用率
3. **检查数据加载** — 验证 DataLoader 是否返回有效数据（无空 batch、无损坏文件）
4. **检查梯度** — 如果有 TensorBoard 日志，检查梯度范数是否爆炸或消失
5. **检查配置** — 对比当前 config 和 base config，找出可能导致问题的参数变更

## 输出格式

以结构化报告输出诊断结果：
- 问题分类（数据问题 / 梯度问题 / 配置问题 / 硬件问题）
- 根因分析
- 建议的修复方案
```

使用方式：

```
> /train-debug
```

### 命令前置元数据（14 个字段）

最关键的字段：

| 字段 | 作用 | ML 场景示例 |
|------|------|------------|
| `description` | Claude 根据它决定是否自动调用 | "诊断训练失败" |
| `model` | 运行时使用的模型 | `haiku`（快速诊断）或 `opus`（深度分析） |
| `allowed-tools` | 免权限提示的工具 | `Bash(python *)`, `Bash(nvidia-smi *)` |
| `context: fork` | 在隔离上下文中运行 | 不污染主对话 |

**[专家提示]** 来自 Boris：
> 如果你一天做某事超过一次，就把它变成技能或命令。
> — *[tips/claude-boris-10-tips-01-feb-26.md](../tips/claude-boris-10-tips-01-feb-26.md) 第 4 条*

**[参考]** 命令实现示例：[implementation/claude-commands-implementation.md](../implementation/claude-commands-implementation.md)

---

## Part 5: 技能系统 — 可复用的专业能力

### 什么是技能

技能是一个**文件夹**（不仅是一个 markdown 文件），可以包含脚本、参考数据、示例代码等资源。

类比：如果命令是"快捷方式"，技能就是"培训手册" — 一套完整的知识和工具，教 Claude 如何完成特定类型的任务。

### 两种使用模式

| 模式 | 触发方式 | 适用场景 |
|------|---------|---------|
| **用户调用** | `/skill-name` 或 Claude 自动发现 | 独立任务，如 `/evaluate-model` |
| **代理预加载** | 代理定义中 `skills:` 字段 | 代理的常备能力，如天气代理预加载天气获取技能 |

### 5 个官方内置技能

| 技能 | 功能 | ML 场景 |
|------|------|--------|
| `/simplify` | 审查代码，消除重复，改善质量 | 重构训练脚本中的冗余代码 |
| `/batch` | 批量对多个文件运行操作 | 批量更新所有 config 文件的学习率 |
| `/debug` | 调试失败的命令或代码 | 调查为什么 `torchrun` 崩溃 |
| `/loop` | 按间隔循环运行任务（最长 3 天） | 每 30 分钟检查训练进度 |
| `/claude-api` | 使用 Claude API 构建应用 | 构建模型评估的自动化脚本 |

### Thariq 的 9 种技能类别

Anthropic 内部将数百个技能分为 9 类。对应到 ML/机器人领域：

| # | 类别 | ML/机器人场景 | 示例技能名 |
|---|------|-------------|-----------|
| 1 | **库与 API 参考** | PyTorch/ROS API 最佳实践 | `pytorch-custom-ops` |
| 2 | **产品验证** | 模型评估与性能验证 | `evaluate-model` |
| 3 | **数据获取与分析** | 训练指标查询、W&B 数据分析 | `training-metrics` |
| 4 | **业务流程自动化** | 实验管理、论文写作流程 | `experiment-tracker` |
| 5 | **代码脚手架** | 新模型/数据集模板生成 | `new-ros-node` |
| 6 | **代码质量审查** | 模型代码审查、性能检查 | `gpu-perf-review` |
| 7 | **CI/CD 与部署** | 模型部署到机器人平台 | `deploy-model` |
| 8 | **运维手册** | 训练故障排查 | `training-debugger` |
| 9 | **基础设施运维** | GPU 集群管理 | `gpu-cluster-ops` |

### 创建自定义技能

**[实战]** 创建一个模型评估技能：

```
.claude/skills/evaluate-model/
├── SKILL.md              # 主技能文件
├── metrics/
│   ├── navigation.md     # 导航任务评估指标
│   └── manipulation.md   # 操作任务评估指标
└── scripts/
    └── eval_template.py  # 评估脚本模板
```

`SKILL.md` 内容：

```yaml
---
name: evaluate-model
description: 运行标准化模型评估流程，检查 checkpoint 性能
argument-hint: [checkpoint-path]
allowed-tools: Bash(python *), Read(*)
---

# 模型评估技能

## 步骤
1. 验证 checkpoint 文件存在且格式正确
2. 根据模型类型选择评估指标（参见 metrics/ 目录）
3. 运行评估脚本，收集结果
4. 生成结构化报告（含指标、可视化建议）

## 评估指标
- 导航任务: SPL (Success weighted by Path Length), SR (Success Rate)
- 操作任务: Grasp SR, Task Completion Rate
- 通用: Inference time (ms), GPU memory (MB)

## 陷阱
- 不要在 evaluation 中使用 dropout（确保 model.eval()）
- 检查 batch norm 的 running stats 是否正确加载
- 对比 checkpoint 的 config 和当前 config 是否一致
```

### Thariq 的 9 个制作技能提示

精选最实用的：

1. **不要说明显的事** — Claude 对编码已经很懂了，技能应关注你项目特有的知识
2. **建立"陷阱"章节** — 记录 Claude 常犯的错误，持续积累
3. **使用文件系统** — 技能是文件夹！把详细参考、脚本、示例拆到子文件中
4. **description 是给模型看的** — 不是摘要，而是"何时触发"的描述
5. **存储脚本** — 给 Claude 可直接运行的脚本，减少它重写样板的时间

**[参考]** 完整技能制作指南：[tips/claude-thariq-tips-17-mar-26.md](../tips/claude-thariq-tips-17-mar-26.md)
**[参考]** 技能前置元数据：[best-practice/claude-skills.md](../best-practice/claude-skills.md)
**[参考]** 技能实现示例：[implementation/claude-skills-implementation.md](../implementation/claude-skills-implementation.md)

### 渐进式披露（Progressive Disclosure）

技能系统使用渐进式披露来节省上下文空间：

1. **启动时**：只加载技能的 `description` 字段（不是全部内容），总预算约 15K 字符
2. **调用时**：才加载完整的 SKILL.md 内容和附属文件
3. **结束后**：释放技能上下文

这意味着你可以创建大量技能而不会让启动变慢 — Claude 只在需要时才读取完整内容。

### context: fork — 隔离技能

设置 `context: fork` 的技能在独立子代理中运行，不污染主对话上下文：

```yaml
---
name: heavy-analysis
description: 深度代码分析，生成详细报告
context: fork
agent: general-purpose
model: opus
---
```

**何时用**：
- 技能会读取大量文件（代码分析、项目审计）
- 技能的中间过程不重要，只需要结论
- 需要更高质量的输出（可以指定 `model: opus`）

**何时不用**：
- 需要跟技能交互式协作的场景
- 技能产出需要继续编辑的场景

### paths — 条件激活

`paths` 字段让技能只在匹配的文件被操作时才激活：

```yaml
---
name: cuda-reviewer
description: 审查 CUDA kernel 代码的性能和正确性
paths: "**/*.cu"
---
```

当 Claude 编辑或读取 `.cu` 文件时，这个技能自动可用。不操作 CUDA 文件时，它不会出现在建议中。

**[实战]** ML 项目中实用的路径匹配：
- `**/*.py` — Python 代码规范
- `configs/**/*.yaml` — 训练配置验证
- `ros_ws/**` — ROS 工作空间规范
- `docker/**` — Dockerfile 最佳实践

---

## Part 6: 子代理系统 — 分身术

### 什么是子代理

子代理是 Claude 的"分身" — 一个拥有独立上下文窗口的 Claude 实例，执行完任务后只将结论返回给"本体"。

类比：你是项目负责人，子代理是你派去调研的助手。你不需要知道助手查了多少资料、走了多少弯路 — 你只需要最终报告。

### 5 种官方子代理

| 代理 | 模型 | 用途 | ML 场景 |
|------|------|------|--------|
| `general-purpose` | 继承 | 复杂多步骤任务 | 研究新论文的实现方案 |
| `Explore` | haiku | 快速代码搜索 | "找到所有 loss 函数定义" |
| `Plan` | 继承 | 规划实现方案 | 规划模型重构的架构设计 |
| `statusline-setup` | sonnet | 配置状态栏 | — |
| `claude-code-guide` | haiku | 回答 Claude Code 问题 | "如何创建自定义技能？" |

### 创建自定义子代理

**[实战]** 创建一个数据集验证代理：

文件：`.claude/agents/dataset-validator.md`

```yaml
---
name: dataset-validator
description: "PROACTIVELY 验证数据集完整性 — 当用户操作训练数据时自动触发"
model: haiku
maxTurns: 20
permissionMode: acceptEdits
---

# 数据集验证代理

你是数据集质量检查员。当被调用时，执行以下检查：

## 检查清单
1. **文件完整性** — 扫描所有图像文件，检测损坏文件（尝试打开并解码）
2. **标注一致性** — 验证标注格式统一（JSON/COCO/VOC）
3. **类别分布** — 统计各类别样本数，标记严重不平衡
4. **训练/验证集重叠** — 检查是否有样本同时出现在两个集合
5. **数据规模** — 报告总样本数、总大小、各 split 比例

## 输出
以 markdown 表格输出检查结果，标记 PASS/WARN/FAIL。
```

### 关键前置元数据字段

| 字段 | 说明 | 常用值 |
|------|------|--------|
| `name` | 唯一标识符 | `dataset-validator` |
| `description` | 何时调用；加 `PROACTIVELY` 可自动触发 | 见上例 |
| `model` | 使用模型 | `haiku`（快速）/ `sonnet`（平衡）/ `opus`（深度） |
| `maxTurns` | 最大轮次 | 简单任务 5-10，复杂任务 20-30 |
| `skills` | 预加载的技能 | `[evaluate-model, dataset-check]` |
| `memory` | 跨会话记忆 | `project`（团队共享）/ `user`（个人） |
| `permissionMode` | 权限控制 | `acceptEdits`（自动批准编辑） |

### 何时使用子代理 vs 直接对话

Thariq 的心理测试：**"我还会需要中间过程，还是只需要结论？"**

| 场景 | 选择 | 原因 |
|------|------|------|
| 在一个大代码库中搜索特定模式 | 子代理 (Explore) | 搜索过程产生大量噪音 |
| 调试当前正在编辑的文件 | 直接对话 | 需要看到中间过程来引导方向 |
| 审查一个 PR 的代码改动 | 子代理 | 只需要审查结论 |
| 逐步实现一个新功能 | 直接对话 | 需要在每一步确认方向 |

**[专家提示]** 来自 Boris：
> 在任何你希望 Claude 投入更多算力的请求后面追加"使用子代理"。这会让 Claude 获得额外的干净上下文窗口来处理任务。
> — *[tips/claude-boris-10-tips-01-feb-26.md](../tips/claude-boris-10-tips-01-feb-26.md) 第 8 条*

**[参考]** 子代理元数据字段：[best-practice/claude-subagents.md](../best-practice/claude-subagents.md)
**[参考]** 子代理实现示例：[implementation/claude-subagents-implementation.md](../implementation/claude-subagents-implementation.md)

### 代理记忆持久化

子代理可以通过 `memory` 字段保存跨会话的学习记录：

| 作用域 | 存储位置 | 用途 |
|--------|---------|------|
| `user` | `~/.claude/agent-memory/<agent>/` | 个人经验（如你偏好的代码风格） |
| `project` | `.claude/agent-memory/<agent>/` | 项目知识（如已知 bug、架构决策） |
| `local` | `.claude/agent-memory-local/<agent>/` | 本地环境信息（不提交 git） |

**[实战]** 训练监控代理配置记忆：

```yaml
---
name: training-monitor
description: 监控训练日志，检测异常
model: haiku
memory: project
---
```

这个代理每次发现新的训练问题模式时，会自动记录到 `.claude/agent-memory/training-monitor/` 中。下次运行时，它就"记得"之前见过的问题类型，诊断更快更准。

### Explore 代理的高效使用

Explore 是专门为代码搜索优化的轻量代理（默认 haiku），特别适合"先探路再决策"的场景：

```
> 用 Explore 代理搜索所有使用 deprecated torch.nn.DataParallel 的地方
> 用 Explore 代理找到所有 ROS topic 的订阅者和发布者
> 用 Explore 代理统计代码库中所有的 TODO 和 FIXME
```

**关键优势**：Explore 代理的搜索结果不会污染你的主上下文 — 只有最终发现返回。

### 代理的工作树隔离

对于可能修改文件的代理，使用 `isolation: "worktree"` 在临时 git 工作树中运行：

```yaml
---
name: refactor-agent
description: 安全重构代码，不影响工作目录
isolation: "worktree"
---
```

代理在隔离的工作树中修改代码，如果结果不满意，工作树自动清理；满意的话，返回分支名称让你 merge。

---

## Part 7: MCP 服务器 — 能力扩展

### 什么是 MCP

MCP（Model Context Protocol）是给 Claude 装"工具箱"的协议。通过 MCP，Claude 可以连接外部工具、数据库和 API。

类比：Claude 本身只会"读代码"和"写代码"。MCP 就像给他配了额外的工具 — 浏览器、文档查询器、画图工具等。

### 推荐的 5 个 MCP 服务器

| MCP | 功能 | ML/机器人场景 |
|-----|------|-------------|
| **Context7** | 获取最新库文档 | 查 PyTorch 2.x 新 API（避免过时训练数据） |
| **Playwright** | 浏览器自动化 | 自动化检查 Weights & Biases 仪表盘 |
| **Claude in Chrome** | 连接真实 Chrome 浏览器 | 调试 Web 可视化界面 |
| **DeepWiki** | GitHub 仓库 wiki 生成 | 快速理解陌生的开源机器人框架 |
| **Excalidraw** | 生成架构图 | 画模型架构图和数据流程图 |

### 配置方法

在项目根目录创建 `.mcp.json`：

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp"]
    },
    "playwright": {
      "command": "npx",
      "args": ["-y", "@playwright/mcp"]
    },
    "deepwiki": {
      "command": "npx",
      "args": ["-y", "deepwiki-mcp"]
    }
  }
}
```

### MCP 作用域

| 级别 | 配置位置 | 用途 |
|------|---------|------|
| 项目 | `.mcp.json`（仓库根目录） | 团队共享的 MCP，提交到 git |
| 用户 | `~/.claude.json` | 个人使用的 MCP，跨项目 |
| 子代理 | 代理前置元数据 `mcpServers` | 限定于特定代理的 MCP |

**[专家提示]** 来自 Boris：
> 使用 Claude Code 最重要的技巧：**给 Claude 一种验证其输出的方式。** 给 Claude 一个浏览器（Chrome 扩展/Playwright），它会编写代码并迭代直到结果正确。
> — *[tips/claude-boris-15-tips-30-mar-26.md](../tips/claude-boris-15-tips-30-mar-26.md) 第 6 条*

**[参考]** [best-practice/claude-mcp.md](../best-practice/claude-mcp.md)

### [实战] MCP 在 ML 项目中的具体应用

**Context7 — 查最新 API 文档**：

Claude 的训练数据可能不包含最新版本的 PyTorch、ROS2 或 transformers 库的 API。Context7 MCP 可以实时获取最新文档：

```
> 用 Context7 查一下 PyTorch 2.x 的 torch.compile 的最新用法和限制
> 用 Context7 查 ROS2 Humble 的 lifecycle node 怎么用
> 查一下 transformers 库最新的 Trainer API 有没有新参数
```

**DeepWiki — 快速理解开源项目**：

```
> 用 DeepWiki 分析 https://github.com/huggingface/lerobot 的架构
> 用 DeepWiki 查 open-x-embodiment 的数据格式定义
```

DeepWiki 会为 GitHub 仓库生成 wiki 式的文档，帮你快速理解陌生的开源框架，不需要花数小时读代码。

**Playwright — 自动化浏览器操作**：

```
> 打开我的 W&B 项目，截图最新一次训练的 loss 曲线
> 在 Grafana 仪表盘上检查 GPU 利用率趋势
```

### MCP 加载机制

默认情况下，MCP 工具定义在启动时预加载到上下文中（每个工具约 1.5K token）。如果你有很多 MCP，可以使用延迟加载：

```json
{
  "mcpServers": {
    "large-tool-server": {
      "command": "npx",
      "args": ["-y", "some-mcp-server"],
      "defer_loading": true
    }
  }
}
```

设置 `defer_loading: true` 后，工具定义不会预加载，而是通过 Tool Search Tool 按需发现。适用于工具数量多但不常用的 MCP 服务器。

---

## Part 8: 钩子系统 — 事件驱动自动化

### 什么是钩子

钩子是 Claude 代理生命周期中的"事件监听器"。当特定事件发生时（比如 Claude 要运行命令、会话开始、工具调用完成），钩子可以自动执行你定义的逻辑。

类比：就像 Git 的 pre-commit hook — 但覆盖了 Claude 工作流程的 **27 个事件**。

### 最实用的 8 个钩子事件

| 事件 | 触发时机 | ML 场景 |
|------|---------|--------|
| `PreToolUse` | Claude 要调用工具之前 | 在 `git commit` 前自动运行 `ruff check` |
| `PostToolUse` | 工具调用完成后 | 记录所有 bash 命令到日志 |
| `SessionStart` | 会话启动时 | 自动激活 conda 环境 |
| `Stop` | Claude 完成当前任务时 | 自动运行 `mypy` 类型检查 |
| `UserPromptSubmit` | 用户发送消息前 | 自动补充项目上下文 |
| `Notification` | Claude 发送通知时 | 转发到 Slack/微信 |
| `SubagentStart` | 子代理启动时 | 记录子代理使用情况 |
| `PermissionRequest` | 请求权限批准时 | 路由到手机远程批准 |

### 4 种处理器类型

| 类型 | 描述 | 示例 |
|------|------|------|
| `command` | 运行 Shell 命令 | 播放声音、运行 lint |
| `prompt` | 单轮 Claude 模型决策 | 快速判断是否允许 |
| `agent` | 多轮子代理处理 | 复杂安全审查 |
| `http` | POST 到 Webhook | 发送到 Slack/Discord |

### [实战] 配置示例

在 `.claude/settings.json` 中配置：

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "type": "command",
        "command": "if echo \"$TOOL_INPUT\" | grep -q 'git commit'; then cd $CLAUDE_PROJECT_DIR && ruff check . && black --check .; fi",
        "async": false,
        "timeout": 10000
      }
    ],
    "SessionStart": [
      {
        "type": "command",
        "command": "echo 'source activate robotics-env' >> $CLAUDE_ENV_FILE",
        "async": true,
        "timeout": 5000
      }
    ],
    "Stop": [
      {
        "type": "command",
        "command": "cd $CLAUDE_PROJECT_DIR && python -m mypy src/ --ignore-missing-imports 2>&1 | tail -5",
        "async": true,
        "timeout": 30000
      }
    ]
  }
}
```

### 按需钩子（来自 Thariq）

技能可以包含仅在技能激活时才生效的钩子。两个实用模式：

- `/careful` — 通过 PreToolUse 阻止危险操作（`rm -rf`、`DROP TABLE`、`force-push`）
- `/freeze` — 阻止对指定目录之外的任何编辑

### 钩子匹配器

钩子可以通过 `matcher` 字段限定只对特定工具调用触发：

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash(git commit*)",
        "type": "command",
        "command": "cd $CLAUDE_PROJECT_DIR && ruff check . --select E,W,F",
        "async": false,
        "timeout": 15000
      }
    ]
  }
}
```

`matcher` 支持通配符：`Bash(git *)` 匹配所有 git 命令，`Edit(*.py)` 匹配所有 Python 文件编辑。

### [实战] ML 项目的完整钩子配置

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash(git commit*)",
        "type": "command",
        "command": "cd $CLAUDE_PROJECT_DIR && ruff check . && black --check .",
        "async": false,
        "timeout": 15000
      },
      {
        "matcher": "Bash(rm -rf*)",
        "type": "command",
        "command": "echo 'BLOCK: 不允许 rm -rf，请使用更安全的删除方式' && exit 1",
        "async": false
      }
    ],
    "SessionStart": [
      {
        "type": "command",
        "command": "echo 'source activate robotics-env' >> $CLAUDE_ENV_FILE && nvidia-smi --query-gpu=memory.used --format=csv,noheader | head -1",
        "async": true,
        "timeout": 5000
      }
    ],
    "Stop": [
      {
        "type": "command",
        "command": "cd $CLAUDE_PROJECT_DIR && python -m mypy src/ --ignore-missing-imports 2>&1 | tail -5",
        "async": true,
        "timeout": 30000
      }
    ],
    "Notification": [
      {
        "type": "command",
        "command": "echo \"$NOTIFICATION_MESSAGE\" | head -1",
        "async": true
      }
    ]
  }
}
```

### 钩子环境变量

钩子脚本中可以使用这些环境变量：

| 变量 | 说明 |
|------|------|
| `$CLAUDE_PROJECT_DIR` | 项目根目录 |
| `$CLAUDE_ENV_FILE` | 环境文件路径（写入的变量会被加载） |
| `$TOOL_NAME` | 当前工具名称（PreToolUse/PostToolUse） |
| `$TOOL_INPUT` | 工具输入（JSON 格式） |
| `$NOTIFICATION_MESSAGE` | 通知内容（Notification） |

**[参考]** 完整钩子文档：[.claude/hooks/HOOKS-README.md](../.claude/hooks/HOOKS-README.md)

---

## Part 9: 设置与配置 — 精细调控

### 5 层设置层级

从高到低优先级：

| 层级 | 位置 | 谁管理 | 版本控制 |
|------|------|--------|---------|
| 1. 托管设置 | `managed-settings.json` / MDM | 组织管理员 | N/A |
| 2. CLI 参数 | 命令行标志 | 当前会话 | 无 |
| 3. 项目本地 | `.claude/settings.local.json` | 个人 | .gitignore |
| 4. 团队共享 | `.claude/settings.json` | 团队 | 是 |
| 5. 全局默认 | `~/.claude/settings.json` | 个人 | 无 |

高层级覆盖低层级。

### 最重要的 15 个设置

**模型与性能**：
| 设置 | 值 | 说明 |
|------|-----|------|
| `model` | `"opus"` / `"sonnet"` | 默认模型 |
| `effort` | `"high"` / `"max"` | 推理努力程度 |

**权限管理**：
```json
{
  "permissions": {
    "allow": [
      "Edit(*)", "Write(*)", "Read(*)",
      "Bash(python *)", "Bash(nvidia-smi *)",
      "Bash(docker *)", "Bash(ros2 *)",
      "Bash(pip install *)", "Bash(conda *)",
      "mcp__context7__*", "mcp__playwright__*"
    ],
    "deny": [
      "Bash(rm -rf /*)"
    ]
  }
}
```

**环境变量**：
```json
{
  "env": {
    "CUDA_VISIBLE_DEVICES": "0,1",
    "ROS_DOMAIN_ID": "42",
    "WANDB_PROJECT": "robot-navigation"
  }
}
```

### [实战] 机器人实验室团队设置模板

`.claude/settings.json`（提交到 git，团队共享）：

```json
{
  "model": "sonnet",
  "permissions": {
    "allow": [
      "Edit(*)", "Write(*)", "Read(*)", "Glob(*)", "Grep(*)",
      "Bash(python *)", "Bash(torchrun *)",
      "Bash(nvidia-smi *)", "Bash(gpustat *)",
      "Bash(docker *)", "Bash(docker-compose *)",
      "Bash(ros2 *)", "Bash(colcon *)",
      "Bash(pip *)", "Bash(conda *)",
      "Bash(git *)",
      "mcp__context7__*", "mcp__deepwiki__*"
    ],
    "deny": [
      "Bash(rm -rf /*)","Bash(shutdown *)", "Bash(reboot *)"
    ]
  },
  "env": {
    "CUDA_VISIBLE_DEVICES": "0,1,2,3",
    "PYTHONPATH": "./src",
    "ROS_DOMAIN_ID": "42"
  },
  "enableAllProjectMcpServers": true,
  "respectGitignore": true
}
```

**[参考]** 完整设置参考：[best-practice/claude-settings.md](../best-practice/claude-settings.md)
**[参考]** CLI 启动参数：[best-practice/claude-cli-startup-flags.md](../best-practice/claude-cli-startup-flags.md)

### 进阶定制

除了核心设置，Claude Code 还提供多种个性化选项：

**状态栏定制**：
```
> /statusline
```
Claude 会根据你的 shell 配置生成自定义状态栏，显示模型、目录、剩余上下文、费用等信息。每个团队成员可以有不同的状态栏。

**键位绑定**：
```
> /keybindings
```
Claude Code 中的每个键位都可以自定义。设置实时加载，即时生效。

**沙箱模式**：
```
> /sandbox
```
在隔离沙箱中运行命令，提高安全性同时减少权限提示。支持文件和网络隔离。

**[实战]** ML 项目中，沙箱可以防止 Claude 意外删除训练数据或修改正在运行的实验配置。

**插件系统**：
```
> /plugin
```
从官方市场安装 LSP（语言服务器）、MCP、技能、代理和钩子。你也可以为团队创建自己的插件市场，将市场 URL 写入 `settings.json` 自动分发给团队成员。

**环境变量管理**：

在 `settings.json` 中使用 `"env"` 字段设置环境变量，比用 wrapper 脚本更优雅：

```json
{
  "env": {
    "CUDA_VISIBLE_DEVICES": "0,1,2,3",
    "PYTHONPATH": "./src:./lib",
    "ROS_DOMAIN_ID": "42",
    "WANDB_PROJECT": "robot-navigation",
    "TOKENIZERS_PARALLELISM": "false",
    "OMP_NUM_THREADS": "4"
  }
}
```

**[专家提示]** 来自 Boris：
> 将 `settings.json` 签入 git，这样团队所有人都能受益。配置支持多个层级 — 代码库、子文件夹、个人、企业策略。
> — *[tips/claude-boris-12-tips-12-feb-26.md](../tips/claude-boris-12-tips-12-feb-26.md) 第 12 条*

---

## Part 10: 工作流编排 — 组合一切

### 命令 → 代理 → 技能管道

这是 Claude Code 最强大的架构模式：

```
用户输入 /weather-orchestrator（命令）
    ↓
命令调用 weather-agent（代理）
    ↓
代理使用 weather-fetcher（预加载技能）获取数据
    ↓
命令调用 weather-svg-creator（技能）生成可视化
    ↓
输出结果
```

本仓库的天气系统就是这个模式的完整演示：
- 入口：[.claude/commands/weather-orchestrator.md](../.claude/commands/weather-orchestrator.md)
- 代理：[.claude/agents/weather-agent.md](../.claude/agents/weather-agent.md)
- 技能：[.claude/skills/weather-fetcher/SKILL.md](../.claude/skills/weather-fetcher/SKILL.md)

**[实战]** ML 场景下的管道：

```
/nightly-eval（命令 — 入口）
    ↓
调用 eval-agent（代理 — 预加载 evaluate-model 技能）
    ↓
eval-agent 拉取最新 checkpoint
    ↓
eval-agent 使用 evaluate-model 技能运行评估
    ↓
命令调用 report-generator 技能生成报告
    ↓
输出 markdown 报告 + 可选创建 PR
```

### 代理团队：并行多会话协作

代理团队不同于子代理 — 每个"队友"都是独立的 Claude Code 会话，有自己完整的上下文窗口，自动加载 CLAUDE.md、MCP 和技能。

使用方式：

```bash
tmux new -s dev
CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1 claude
```

然后你可以让 Claude 分配多个并行任务：
- 会话 A：重构模型架构
- 会话 B：编写对应的单元测试
- 会话 C：更新文档

**[参考]** [implementation/claude-agent-teams-implementation.md](../implementation/claude-agent-teams-implementation.md)

### /loop — 循环任务

```
> /loop 30m 检查最新训练进度，如果 validation loss 不再下降就通知我
> /loop 1h /nightly-eval
```

`/loop` 让 Claude 按间隔自动运行任务，最长持续 3 天。

**两种模式**：

| 模式 | 语法 | 特点 |
|------|------|------|
| 固定间隔 | `/loop 30m 检查训练进度` | 每 30 分钟执行一次 |
| 动态间隔 | `/loop 检查训练进度` | Claude 自行决定下次检查时间 |

**[专家提示]** 来自 Boris：
> 我本地运行着一堆循环：`/loop 5m /babysit` 自动处理代码审查；`/loop 30m /slack-feedback` 自动为反馈创建 PR。尝试把工作流转变为技能 + 循环。
> — *[tips/claude-boris-15-tips-30-mar-26.md](../tips/claude-boris-15-tips-30-mar-26.md) 第 3 条*

### /schedule — 持久化定时任务

`/schedule` 创建跨会话的定时任务（cron-based），即使 Claude 退出也会保留：

```
> /schedule 每天凌晨 2 点运行模型评估
> /schedule 每周一早上 9 点生成训练进度周报
```

**[实战]** ML 场景下的完整夜间评估管线：

```markdown
# .claude/commands/nightly-eval.md
---
description: 夜间模型评估全流程
model: sonnet
allowed-tools: Bash(python *), Bash(nvidia-smi *), Read(*), Write(*)
---

## 流程
1. 找到 outputs/ 下最新的 checkpoint
2. 启动 dataset-validator 代理验证测试数据
3. 运行标准化评估（调用 evaluate-model 技能）
4. 对比昨天的结果（读取 eval_history.json）
5. 生成 markdown 评估报告到 reports/
6. 如果性能下降超过 5%，在报告中用 ⚠️ 标记
```

设置定时：
```
> /schedule 每天凌晨 2 点 /nightly-eval
```

### Git 工作树隔离

工作树让你在同一仓库中运行多个独立的 Claude 会话：

```bash
claude -w    # 在新工作树中启动
```

**[专家提示]** 来自 Boris：
> 同时启动 3-5 个工作树，每个运行自己的 Claude 会话。这是最大的生产力提升。我始终运行着几十个 Claude。
> — *[tips/claude-boris-10-tips-01-feb-26.md](../tips/claude-boris-10-tips-01-feb-26.md) 第 1 条*

**[参考]** [implementation/claude-scheduled-tasks-implementation.md](../implementation/claude-scheduled-tasks-implementation.md)

---

## Part 11: 高级技巧 — 来自创建者的实战经验

### #1 给 Claude 验证方式（最重要的技巧）

Boris 反复强调的首要建议：

> "使用 Claude Code 最重要的技巧：**给 Claude 一种验证其输出的方式。** 一旦你这样做了，Claude 会迭代直到结果很好。"

在 ML 场景中的应用：
- 让 Claude 运行测试套件来验证代码正确性
- 让 Claude 运行评估脚本来验证模型性能
- 让 Claude 检查 GPU 状态来验证训练正常
- 给 Claude 浏览器 MCP 来验证可视化输出

### #2 每个复杂任务从计划模式开始

```
> /plan 重构整个 perception 模块，将单阶段检测器换成两阶段的
```

让 Claude 先分析代码、设计方案，你审核后再实施。有人还让第二个 Claude 以"高级工程师"身份审查计划。

### #3 努力程度调节

```
> /effort max     # 当前会话使用最大努力（仅 Opus 4.6）
> /effort low     # 快速任务用低努力节省时间
```

规律：代码审查用 `high`，简单修改用 `low`，架构设计用 `max`。

### #4 使用 /batch 批量修改

```
> /batch 将所有 Python 文件中的 print() 替换为 logging.info()
```

`/batch` 会先访谈你确认需求，然后扇出到多个工作树代理并行执行 — 可以同时修改几十甚至几百个文件。

### #5 语音输入

在终端中运行 `/voice`，然后按住空格键说话。你说话的速度是打字的 3 倍，提示会变得更加详细。Boris 大部分编码是通过对话完成的。

### #6 分叉会话

两种方式保存当前对话的"存档点"：

```
> /branch                    # 在会话内分叉
$ claude --resume <id> --fork-session  # 从 CLI 分叉
```

### #7 /powerup 发现隐藏功能

```
> /powerup
```

这会启动一系列带动画的互动教程，教你 10 个被忽视的功能。

### #8 跨仓库工作

```bash
claude --add-dir ~/other-repo    # 给 Claude 访问另一个仓库
```

### #9 自动模式 — 解放双手

自动模式让权限请求由一个基于模型的分类器自动判断是否安全：

```
Shift+Tab → 循环切换：请求权限 → 计划模式 → 自动模式
```

- 安全命令自动批准，危险命令暂停询问
- 配合工作树使用，你可以同时运行多个 Claude 而不用盯着看
- Max、Teams 和 Enterprise 用户可用

**[实战]** 训练场景：让 Claude 在自动模式下运行训练诊断脚本，你去泡杯咖啡回来看结果。

### #10 专注模式 — 只看结果

```
> /focus
```

隐藏所有中间工具调用，只显示最终结果。Boris 说他已经信任模型做正确的事，只看最终产出。

**何时用**：熟悉的代码库中做常规修改时。
**何时不用**：调试复杂问题时 — 你需要看中间过程。

### #11 代码审查 — 多代理找 bug

Claude Code 内置代码审查功能：当你打开 PR 时，Claude 派出一个代理团队做深度审查。

**[专家提示]** 来自 Boris：
> 你投入到问题中的 token 越多，结果越好 — 这就是**测试时间算力**。多个独立上下文窗口的组合特别有效：一个代理写代码，另一个审查 — 就像工程团队中的代码审查。
> — *[tips/claude-boris-2-tips-10-mar-26.md](../tips/claude-boris-2-tips-10-mar-26.md)*

### #12 保持 PR 小巧

Boris 一天提交 141 个 PR，中位数每个 118 行，全部使用 squash 合并：

| 指标 | 行数 | 含义 |
|------|------|------|
| p50 | 118 | 一半 PR 不到 118 行 |
| p90 | 498 | 90% 不到 500 行 |
| p99 | 2,978 | 几乎没有超过 3000 行的 |

**规律**：小 PR 更易审查、更快合并、更容易回滚。配合 squash 合并，每个 PR = 一个提交，`git bisect` 精准定位 bug。

### #13 /fewer-permission-prompts — 智能减少权限提示

```
> /fewer-permission-prompts
```

扫描你的会话历史，找到安全但频繁触发权限提示的命令，推荐添加到允许列表。

### #14 自定义输出风格

```
> /config → 输出风格
```

- **Explanatory** — 熟悉新代码库时推荐，Claude 会解释每次修改背后的原因
- **Learning** — 指导模式，Claude 教你做修改而不是替你做
- **Custom** — 完全自定义的语调和格式

### #15 远程控制 — 手机批准权限

```
> /remote-control
```

生成一个配对码，用手机扫码后可以远程批准 Claude 的权限请求。让 Claude 在工作站运行长任务，你在手机上批准关键操作。

**[参考]** Boris 全部技巧：
- [tips/claude-boris-10-tips-01-feb-26.md](../tips/claude-boris-10-tips-01-feb-26.md)
- [tips/claude-boris-15-tips-30-mar-26.md](../tips/claude-boris-15-tips-30-mar-26.md)
- [tips/claude-boris-6-tips-16-apr-26.md](../tips/claude-boris-6-tips-16-apr-26.md)
- [tips/claude-boris-12-tips-12-feb-26.md](../tips/claude-boris-12-tips-12-feb-26.md)
- [tips/claude-boris-13-tips-03-jan-26.md](../tips/claude-boris-13-tips-03-jan-26.md)
- [tips/claude-boris-2-tips-10-mar-26.md](../tips/claude-boris-2-tips-10-mar-26.md)
- [tips/claude-boris-2-tips-25-mar-26.md](../tips/claude-boris-2-tips-25-mar-26.md)

**[参考]** Thariq 全部技巧：
- [tips/claude-thariq-tips-16-apr-26.md](../tips/claude-thariq-tips-16-apr-26.md)
- [tips/claude-thariq-tips-17-mar-26.md](../tips/claude-thariq-tips-17-mar-26.md)

**[参考]** Power-Ups：[best-practice/claude-power-ups.md](../best-practice/claude-power-ups.md)

---

## Part 12: 实战项目 — 从零配置一个机器人项目

以下是一个完整的端到端演练：为一个"视觉导航机器人"项目配置 Claude Code 环境。

### 场景设定

你有一个机器人视觉导航项目，目录结构如下：

```
robot-nav/
├── configs/           # 训练配置 YAML
├── data/              # 数据集（不提交到 git）
├── models/            # 模型定义
│   ├── backbone.py    # ViT backbone
│   ├── policy.py      # Action prediction head
│   └── vla.py         # VLA 模型主入口
├── scripts/           # 训练/评估脚本
├── ros_ws/            # ROS2 工作空间
├── docker/            # Dockerfile
└── tests/             # 单元测试
```

### 步骤 1: 创建 CLAUDE.md

```bash
cd robot-nav
claude
> /init
```

或手动创建，内容参考 [Part 2 的模板](#实战-机器人视觉导航项目的-claudemd-模板)。

### 步骤 2: 配置设置

创建 `.claude/settings.json`（团队共享）：

```json
{
  "permissions": {
    "allow": [
      "Edit(*)", "Write(*)", "Read(*)", "Glob(*)", "Grep(*)",
      "Bash(python *)", "Bash(torchrun *)",
      "Bash(nvidia-smi *)", "Bash(docker *)",
      "Bash(ros2 *)", "Bash(colcon *)",
      "Bash(pip *)", "Bash(conda *)", "Bash(git *)",
      "mcp__context7__*", "mcp__deepwiki__*"
    ]
  },
  "env": {
    "CUDA_VISIBLE_DEVICES": "0,1,2,3",
    "PYTHONPATH": "./src",
    "ROS_DOMAIN_ID": "42"
  },
  "enableAllProjectMcpServers": true
}
```

创建 `.claude/settings.local.json`（个人偏好，不提交 git）：

```json
{
  "model": "opus",
  "env": {
    "WANDB_API_KEY": "your-key-here"
  }
}
```

### 步骤 3: 创建自定义命令

`.claude/commands/train-debug.md` — 训练调试（参考 [Part 4](#实战-创建一个训练调试命令)）

`.claude/commands/eval-quick.md`：

```yaml
---
description: 快速运行模型评估，用最新的 checkpoint
model: haiku
allowed-tools: Bash(python *)
---

# 快速评估

1. 找到 outputs/ 目录下最新的 checkpoint
2. 运行 `python scripts/eval.py --checkpoint <path> --episodes 50`
3. 输出关键指标（SPL, SR, 推理时间）
```

### 步骤 4: 创建自定义技能

创建 `.claude/skills/evaluate-model/SKILL.md`（参考 [Part 5](#实战-创建一个模型评估技能)）

创建 `.claude/skills/dataset-check/SKILL.md`：

```yaml
---
name: dataset-check
description: 检查数据集完整性和格式一致性
allowed-tools: Bash(python *), Read(*)
---

# 数据集检查技能

## 检查项
1. 扫描图像文件是否有损坏（使用 PIL 尝试打开）
2. 验证标注文件格式一致
3. 检查 train/val split 无重叠
4. 统计类别分布并可视化

## 陷阱
- 大数据集检查时间长，先对 100 个样本做抽检
- 注意文件路径编码问题（中文路径）
```

### 步骤 5: 创建自定义代理

创建 `.claude/agents/dataset-validator.md`（参考 [Part 6](#实战-创建一个数据集验证代理)）

创建 `.claude/agents/training-monitor.md`：

```yaml
---
name: training-monitor
description: 监控训练日志，检测 NaN/异常并报警
model: haiku
maxTurns: 10
skills:
  - evaluate-model
---

# 训练监控代理

监控训练日志文件，检测以下异常：
1. Loss 变为 NaN 或 Inf
2. Loss 连续 N 个 epoch 不下降
3. GPU 显存使用率异常（>95% 或突降）
4. 学习率异常值

发现问题时，分析可能的原因并给出修复建议。
```

### 步骤 6: 配置 MCP 服务器

创建 `.mcp.json`：

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp"]
    },
    "deepwiki": {
      "command": "npx",
      "args": ["-y", "deepwiki-mcp"]
    }
  }
}
```

### 步骤 7: 配置钩子

在 `.claude/settings.json` 中添加钩子配置：

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash(git commit*)",
        "type": "command",
        "command": "cd $CLAUDE_PROJECT_DIR && ruff check . --select E,W,F && black --check .",
        "async": false,
        "timeout": 15000
      }
    ],
    "SessionStart": [
      {
        "type": "command",
        "command": "echo 'source activate robotics-env' >> $CLAUDE_ENV_FILE",
        "async": true,
        "timeout": 5000
      }
    ]
  }
}
```

这样每次 Claude 提交代码前都会自动运行 ruff 和 black 检查，每次启动会话时自动激活 conda 环境。

### 步骤 8: 创建工作流编排

创建一个端到端的评估命令，串联代理和技能：

`.claude/commands/full-eval.md`：

```yaml
---
description: 完整模型评估流程 — 数据验证 → 模型评估 → 报告生成
model: sonnet
allowed-tools: Bash(python *), Read(*), Write(*), Agent(*)
---

# 完整评估流程

按以下顺序执行：

1. **数据验证** — 启动 dataset-validator 代理检查测试数据完整性
2. **模型评估** — 使用 evaluate-model 技能运行标准评估
3. **结果对比** — 读取 eval_history.json，与历史最优结果对比
4. **报告生成** — 写入 markdown 报告到 reports/eval-{date}.md

如果数据验证失败，停止并报告问题。如果性能下降超过 5%，用 ⚠️ 标记。
```

使用：
```
> /full-eval
```

### 步骤 9: 日常使用流程

```bash
# 开始新的一天
cd robot-nav
claude

# 查看项目状态
> /context

# 快速评估最新模型
> /eval-quick

# 调试训练问题
> /train-debug

# 理解陌生代码
> @models/vla.py 解释这个 VLA 模型的推理流程

# 用子代理搜索代码
> 启动一个 Explore 子代理，找到所有使用 deprecated API 的地方

# 批量修改
> /batch 将所有 Python 文件的 type hints 更新为最新语法

# 长时间任务用工作树
$ claude -w    # 在独立工作树中重构模型
```

### 最终项目结构

```
robot-nav/
├── .claude/
│   ├── settings.json          # 团队设置
│   ├── settings.local.json    # 个人设置 (.gitignore)
│   ├── commands/
│   │   ├── train-debug.md     # 训练调试命令
│   │   └── eval-quick.md      # 快速评估命令
│   ├── skills/
│   │   ├── evaluate-model/
│   │   │   ├── SKILL.md
│   │   │   ├── metrics/
│   │   │   └── scripts/
│   │   └── dataset-check/
│   │       └── SKILL.md
│   └── agents/
│       ├── dataset-validator.md
│       └── training-monitor.md
├── .mcp.json                  # MCP 服务器配置
├── CLAUDE.md                  # 项目记忆
├── CLAUDE.local.md            # 个人项目笔记 (.gitignore)
├── configs/
├── models/
├── scripts/
├── ros_ws/
└── ...
```

---

## 附录 A: 命令速查表

### 日常使用

| 命令 | 功能 | 快捷键 |
|------|------|--------|
| `/context` | 查看上下文使用 | — |
| `/compact [指引]` | 压缩上下文 | — |
| `/clear` | 开始新会话 | — |
| `/rewind` | 回退到之前消息 | Esc Esc |
| `/diff` | 查看未提交更改 | — |
| `/plan [描述]` | 进入计划模式 | — |
| `/model [名称]` | 切换模型 | — |
| `/effort [级别]` | 设置努力程度 | — |
| `/cost` | 查看使用费用 | — |
| `/usage` | 查看计划限额 | — |
| `/doctor` | 诊断安装问题 | — |
| `/btw [问题]` | 不中断地问旁问 | — |
| `/voice` | 语音输入 | — |
| `/branch` | 分叉当前会话 | — |
| `/batch` | 批量操作 | — |
| `/loop [间隔] [任务]` | 循环执行 | — |
| `/powerup` | 发现隐藏功能 | — |

### 扩展管理

| 命令 | 功能 |
|------|------|
| `/init` | 初始化项目 |
| `/memory` | 编辑 CLAUDE.md |
| `/agents` | 管理代理 |
| `/skills` | 列出技能 |
| `/mcp` | 管理 MCP |
| `/hooks` | 查看钩子 |
| `/permissions` | 管理权限 |
| `/config` | 打开设置 |

---

## 附录 B: 前置元数据字段参考

### 命令 / 技能共享字段 (14)

| 字段 | 类型 | 说明 |
|------|------|------|
| `name` | string | 显示名称和 /斜杠命令 |
| `description` | string | 功能描述（也用于自动发现） |
| `when_to_use` | string | 触发短语示例 |
| `argument-hint` | string | 自动补全提示 |
| `disable-model-invocation` | boolean | 防止自动调用 |
| `user-invocable` | boolean | 是否在 / 菜单显示 |
| `paths` | string/list | 激活条件的 glob 模式 |
| `allowed-tools` | string | 免权限的工具 |
| `model` | string | 运行模型 |
| `effort` | string | 努力程度 |
| `context` | string | `fork` = 隔离上下文 |
| `agent` | string | fork 时的子代理类型 |
| `shell` | string | bash 或 powershell |
| `hooks` | object | 作用域钩子 |

### 子代理额外字段 (16 总计)

| 字段 | 类型 | 说明 |
|------|------|------|
| `name` | string | 唯一标识符 |
| `description` | string | 何时调用（支持 PROACTIVELY） |
| `tools` / `disallowedTools` | string/list | 工具白名单/黑名单 |
| `model` | string | haiku/sonnet/opus/inherit |
| `permissionMode` | string | 权限模式 |
| `maxTurns` | integer | 最大轮次 |
| `skills` | list | 预加载技能 |
| `mcpServers` | list | MCP 服务器 |
| `hooks` | object | 作用域钩子 |
| `memory` | string | 记忆作用域 |
| `background` | boolean | 后台运行 |
| `effort` | string | 努力程度 |
| `isolation` | string | worktree 隔离 |
| `initialPrompt` | string | 自动首轮提示 |
| `color` | string | 显示颜色 |

---

## 附录 C: 常见问题与故障排除

| 问题 | 解决方案 |
|------|---------|
| Claude 不识别项目结构 | 检查 CLAUDE.md 是否存在且在正确位置 |
| 上下文溢出/性能下降 | `/context` 检查 → `/compact` 或 `/clear` |
| MCP 服务器启动超时 | `npx --yes @upstash/context7-mcp` 手动测试连接 |
| 权限提示太频繁 | 在 settings.json 的 `permissions.allow` 中添加常用工具，或运行 `/fewer-permission-prompts` |
| Claude 给出过时的 API | 确保 Context7 MCP 已配置并使用 |
| 安装问题 | 运行 `/doctor` 诊断 |
| 训练相关命令被拒绝 | 在 `permissions.allow` 中添加 `Bash(python *)`, `Bash(torchrun *)` |
| 子代理不被自动触发 | 检查 description 中是否包含 `PROACTIVELY` |
| 技能不在 / 菜单中显示 | 检查 `user-invocable` 不是 `false`，检查 `paths` 是否匹配 |
| 多卡训练时 Claude 操作太慢 | 用 `model: haiku` 做快速诊断，`model: opus` 做深度分析 |
| Claude 修改了不该动的文件 | 在 CLAUDE.md 中明确"不要修改"列表，或用 `permissions.deny` 禁止 |
| 会话中途 Claude 变"笨"了 | 上下文腐化，`/context` 检查后 `/compact` 或 `/clear` |
| 子代理运行时间太长 | 设置 `maxTurns` 限制，用 `model: haiku` 加速 |
| 钩子执行超时 | 检查 `timeout` 设置，async 钩子不阻塞主流程 |
| `/loop` 没有按预期运行 | 确认间隔格式正确（如 `30m`、`1h`），检查技能是否存在 |

### 键盘快捷键

| 快捷键 | 功能 |
|--------|------|
| `Enter` | 发送消息 |
| `Shift+Enter` | 换行（需先运行 `/terminal-setup`） |
| `Esc Esc` (双击) | 回退到上一条消息（同 `/rewind`） |
| `Shift+Tab` | 在权限模式间切换（请求权限 → 计划 → 自动） |
| `Tab` | 接受建议/自动补全 |
| `Ctrl+C` | 中断当前操作 |
| `Ctrl+D` | 退出 Claude Code |
| `Space`（/voice 中） | 按住说话 |

> **[专家提示]** 运行 `/keybindings` 可以自定义上述所有键位绑定，设置实时加载。

---

## 附录 D: 本仓库文件索引

| 目录 | 内容 | 最佳起读文件 |
|------|------|------------|
| `best-practice/` | 8 篇最佳实践（命令、技能、代理、设置、MCP、记忆、CLI、Power-ups） | `claude-memory.md` |
| `tips/` | 9 篇来自 Boris 和 Thariq 的实战提示 | `claude-boris-10-tips-01-feb-26.md` |
| `reports/` | 9 篇深度分析报告（高级工具使用、Agent SDK、浏览器自动化等） | `claude-agent-command-skill.md` |
| `implementation/` | 5 篇实现指南（命令、技能、代理、团队、计划任务） | `claude-commands-implementation.md` |
| `tutorial/` | 本教程 + day0 安装 + day1 概念入门 | 你在读的这个文件 |
| `.claude/commands/` | 8 个命令示例 | `weather-orchestrator.md` |
| `.claude/skills/` | 7 个技能示例 | `weather-fetcher/SKILL.md` |
| `.claude/agents/` | 11 个代理示例 | `weather-agent.md` |
| `.claude/hooks/` | 钩子系统（脚本、配置、音频文件） | `HOOKS-README.md` |
| `orchestration-workflow/` | 天气编排系统流程图和输出 | `orchestration-workflow.md` |

---

> **下一步**：从 Part 0 开始安装 Claude Code，然后按顺序阅读。到 Part 4 你就能开始创建自定义命令了。到 Part 12 你就有了完整的项目配置。
>
> 持续更新中 — 随着 Claude Code 版本迭代，本教程会同步更新。
