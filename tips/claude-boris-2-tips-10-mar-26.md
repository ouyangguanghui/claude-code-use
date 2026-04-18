# 代码审查与测试时间算力 — Boris Cherny 的技巧

Boris Cherny ([@bcherny](https://x.com/bcherny))，Claude Code 的创建者，于 2026 年 3 月 10 日分享的见解总结。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code 最佳实践</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## 1/ 介绍代码审查

Claude Code 新功能：**代码审查**。一个代理团队对每个 PR 进行深度审查。

- 首先为 Anthropic 自己的团队构建 — 今年每位工程师的代码产出增长了 **200%**，审查是瓶颈
- Boris 已经使用了几周，发现它捕获了许多他本不会注意到的真实 bug
- 当 PR 打开时，Claude 派出一个代理团队来寻找 bug

<a href="https://x.com/bcherny/status/2031089411820228645"><img src="assets/boris-26-3-10/0.png" alt="Boris Cherny 宣布代码审查" width="50%" /></a>

---

## 2/ 测试时间算力与多上下文窗口

大致上，你投入到编码问题中的 token 越多，结果就越好。Boris 称之为**测试时间算力**。

- 使用**独立的上下文窗口**会使结果更好 — 这就是子代理工作的原因，也是为什么一个代理可能造成 bug 而另一个（使用完全相同的模型）可以找到它们
- 类似于工程团队：如果 Boris 造成了一个 bug，他审查代码的同事可能比他自己更可靠地找到它
- 在极限情况下，代理可能会写出完美无 bug 的代码 — 在那之前，**多个不相关的上下文窗口**往往是一个好方法

<a href="https://x.com/bcherny/status/2031151689219321886"><img src="assets/boris-26-3-10/1.png" alt="Boris Cherny 关于测试时间算力" width="50%" /></a>

---

## 来源

- [Boris Cherny (@bcherny) on X — 2026 年 3 月 10 日](https://x.com/bcherny)
