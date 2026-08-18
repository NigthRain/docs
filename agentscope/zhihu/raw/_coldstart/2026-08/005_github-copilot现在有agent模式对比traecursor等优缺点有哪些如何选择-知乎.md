---
title: github copilot现在有agent模式,对比trae、cursor等优缺点有哪些?如何选择? - 知乎
author: 江小北
source_url: https://www.zhihu.com/question/1982450631047389962/answer/2071985109574722745?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-15 15:42
content_type: Answer
vote_up_count: 2
comment_count: 0
collected_at: 2026-08-18 10:32:47
index: 5/314
---

# github copilot现在有agent模式,对比trae、cursor等优缺点有哪些?如何选择? - 知乎

> 江小北 | 2026-08-15 15:42

来源: https://www.zhihu.com/question/1982450631047389962/answer/2071985109574722745?utm_medium=openapi_platform&utm_source=1a2112

---

模型：负责推理

CLI / Harness：负责读文件、修改代码、执行命令

控制面：负责管理任务、工作区、状态、成本和交付

过去大家关注最多的是第一层：

但真正进入工程实践后，问题开始变化。

模型能力当然重要，但每天开发过程中更烦人的事情，往往不是“不会写代码”。

而是：
• 这个 Agent 改到哪里了？
• 这个任务为什么卡住？
• 两个 Agent 同时修改代码会不会冲突？
• 哪个 Provider 消耗更多？
• 最终代码怎么合并？

这些问题，其实已经超出了模型本身。

T3 Code 做的事情，就是尝试把这些工程管理问题集中起来。

它不会替代 Codex 或 Claude Code，而是在上层管理：

Session
Worktree
Git
Terminal
文件变化
Agent 状态

然后通过 Provider Adapter 去连接不同 Coding Agent。

这让我想到一个趋势：

未来 AI Coding 工具竞争的重点，可能不会只是“谁的模型更聪明”。

还会包括： 谁能更好地组织这些 Agent 工作

最近几个提交，比官网文案更说明问题

看 T3 Code 最近的几个更新，会发现它关注的问题非常工程化。

比如 Worktree。

8 月 9 日，T3 Code 增加了项目级工作区选择。

任务可以直接使用当前 checkout，也可以进入独立 Worktree。

这个变化看起来不起眼，但对于多 Agent 场景非常关键。

因为多个 Agent 同时工作时，最大的风险不是模型不会写，而是：

它们可能同时修改同一份代码。

一个 Agent 在重构接口。

另一个 Agent 在修 Bug。

如果没有隔离，最后很容易进入混乱状态。

所以很多开发者讨论 Multi-Agent Coding 时，最后都会回到 Worktree。

代码隔离，其实比开几个聊天窗口重要得多。

另一个更新是 Subagent 状态展示。

以前启动多个 Agent 后，经常出现一种情况：

你不知道它是在运行。

还是等待输入。

还是已经失败。

对于单 Agent 来说，这不是问题。

但 Agent 数量增加以后，人需要一个“观察窗口”。

否则所谓智能协作，最后可能只是：

打开更多标签页。

T3 Code 还增加了 Usage 页面。


