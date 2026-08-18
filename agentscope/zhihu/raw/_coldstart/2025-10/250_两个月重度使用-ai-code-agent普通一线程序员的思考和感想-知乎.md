---
title: 两个月重度使用 AI Code Agent:普通一线程序员的思考和感想 - 知乎
author: swananan
source_url: https://zhuanlan.zhihu.com/p/1966643596632523336?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-10-28 23:24
content_type: Article
vote_up_count: 484
comment_count: 34
collected_at: 2026-08-18 10:32:50
index: 250/314
---

# 两个月重度使用 AI Code Agent:普通一线程序员的思考和感想 - 知乎

> swananan | 2025-10-28 23:24

来源: https://zhuanlan.zhihu.com/p/1966643596632523336?utm_medium=openapi_platform&utm_source=1a2112

---

出活快的话，是因为我刚毕业，当时每个周末都在主动加班，不快就见鬼了😈。至于代码写的像模像样，我当时做的是 nginx 的 C 模块开发。因为优秀的 nginx 三方模块代码特别多，我每次在工作中要实现的很多功能点，本质上都是到处“借鉴”大佬们写的代码，我自己修修改改，做一做胶水和测试工作，代码就能健壮的跑起来了。所以，我老板在 review 我代码的时候，本质上是在 review 很多大佬们的智慧结晶😉。当我悟透这一点之后，我开始重度使用 code snippet 工具，记录下我读到过，写的很好的代码样例，来加速我搬砖的效率。
是的，之所以回忆这个事情，是因为我想“炫耀”一下，我在刚入行的时候，就领悟了写代码的本质😂: Ctrl + c 和 Ctrl + v，当然更准确的说，是知道在哪里 Ctrl + c，知道去哪里 Ctrl + v，并且能为功能的正确性兜底。我在刚接触到 Copilot 早期版本的时候，我一直觉得这是一个更高级的 code snippet 工具罢了。但是，chatGPT 出来之后，感觉很短的一段时间，AI 生成代码越来越流行，我大概是去年开始尝试使用 Cursor 和 Vscode Copilot 等工具来辅助编写代码，结结实实被 Cursor 的易用性给圈粉了，相比较而言，当时 Copilot 使用体验就差很多（不过最近一年 Copilot 体验开始追赶上来一些）。
虽然 Cursor 非常好用，也非常智能，但是我一直没有摆脱最早的一个固定思维，就是这只是一个加强版的 code snippet，具备 chatGPT 的能力，某种意义上具备了 stackoverflow 的功效，但是并没有翻天覆地的改变。当然，我现在这么说可能对 Cursor 不是很公平，考虑到我已经比较长一段时间没有使用 Cursor 了。
但是，在我最近两个月高强度使用了 Claude Code 和 Codex 之后，我发现 Code Agent 命令行工具整体上在任务的完成度和准确性上有了巨大的提升，基本上可以说是翻天覆地的变化。这一切，完全改变了我对 AI Coding 的看法，在这里，我直接抛出我版本更新后的观点：
AI 生成代码不仅仅只适合用于 POC 项目或者从零到一，在后续主流的开发中，AI Code Agent 大概率要全面接管代码生成，以后手写高级语言代码，就像是现在手写汇编一样，变成古法编程了（有存在的必要，但是越来越少见）
