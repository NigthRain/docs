---
title: agent记忆系统如何设计? - 知乎
author: 李源炳
source_url: https://www.zhihu.com/question/2052208211743265565/answer/2069325277793085355?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-08 07:33
content_type: Answer
vote_up_count: 1
comment_count: 0
collected_at: 2026-08-18 10:32:47
index: 48/314
---

# agent记忆系统如何设计? - 知乎

> 李源炳 | 2026-08-08 07:33

来源: https://www.zhihu.com/question/2052208211743265565/answer/2069325277793085355?utm_medium=openapi_platform&utm_source=1a2112

---

系列「企业级 AI Agent 实现拆解」E63 篇，Part 14 记忆篇第一章。 上一篇收完了 RAG——那解决的是「Agent 懂业务」。这篇开始讲记忆，解决的是「Agent 记得你」。
先给一个可能让你意外的事实：Eino 框架里没有官方的 memory 组件。记忆不是框架帮你做的事，是你自己拼出来的。这篇就把这十几行拼装代码拆开看。
先分清楚：记忆和 RAG 不是一回事
两者都是「存东西、查东西、拼进 prompt」，非常容易混。但它们回答的是不同的问题：
	RAG（知识库）	记忆
存的是什么	公司文档、产品手册——所有人共享	这个用户说过的话——一人一份
谁写进去的	管理员上传，离线索引	用户自己，每轮对话实时产生
怎么取	语义检索，取最相关的几片	按会话 ID 取，通常全都要
过期了怎么办	文档改版就重新索引	越久远越不重要，要衰减、要淘汰
答错的后果	答案不准	可能泄露别人的隐私
最后一行是记忆最要命的地方：RAG 检索错了只是答得不好，记忆串了是事故——把 A 用户的对话内容拼进了 B 用户的 prompt。
所以这一 Part 从第一篇起就要把「隔离」这件事放在心上。
读完这篇你会知道
・Eino 没有官方 memory 组件，官方示例里那个 MemoryStore 接口只有三个方法
・记忆的本质就三步：读出来、拼上去、写回去，没有任何框架魔法
・一个 40 行的 PostgreSQL 实现，以及每轮实际发给模型的消息列表长什么样
・官方示例用 Gob 而不是 JSON 序列化，实测它能完整保住 ToolCalls 和 ToolCallID
・Gob 的固定开销有多大：4 条消息 2647 字节，200 条消息才 15775 字节——每条从 662 字节降到 79 字节
・Write 是整体覆盖不是追加：实测两个并发请求各写一条，最后只剩一条
・100 轮对话 = 200 条消息，每一轮都要全部读出来、拼进 prompt、再全部写回
一、Eino 里没有 memory 组件
先把这个事实说清楚，省得你去翻文档找。
eino/components/ 下面有 model、tool、document、embedding、indexer、retriever、prompt——没有 memory。
仓库里能搜到两个远程分支叫 feat/auto_memory_mw，说明官方在做，但截至 v0.9.13 没有合进主干。
