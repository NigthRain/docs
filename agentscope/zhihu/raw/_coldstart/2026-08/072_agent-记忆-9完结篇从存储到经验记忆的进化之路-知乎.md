---
title: Agent 记忆 9(完结篇):从存储到经验——记忆的进化之路 - 知乎
author: 锤同学LikeMath
source_url: https://zhuanlan.zhihu.com/p/2067996046261850746?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-04 15:33
content_type: Article
vote_up_count: 0
comment_count: 0
collected_at: 2026-08-18 10:32:48
index: 72/314
---

# Agent 记忆 9(完结篇):从存储到经验——记忆的进化之路 - 知乎

> 锤同学LikeMath | 2026-08-04 15:33

来源: https://zhuanlan.zhihu.com/p/2067996046261850746?utm_medium=openapi_platform&utm_source=1a2112

---

记忆系列走到最后一篇。前面八篇，我们把记忆拆成了一个个零件：RAG、LoRA、KV cache、Mem0、Mem0g、Reflexion、MemGPT……但散落的零件不等于完整的图景。
今天这篇，把整个记忆系列收进一个进化框架。它来自一篇 ACL 2026 的综述：《From Storage to Experience》——作者认为，Agent 记忆的发展不是"存储越来越大"，而是沿着一条清晰的进化之路：
存储（Storage）→ 反思（Reflection）→ 经验（Experience）
论文信息
标题：From Storage to Experience: A Survey on the Evolution of LLM Agent Memory Mechanisms
作者：Jinghao Luo, Yuchen Tian 等（香港浸会大学等多机构）
发表：ACL 2026 Findings
arXiv：2605.06716
配套资源： http://http://github.com/FeishuLuo/Evolving-LLM-Agent-Memory-Surveyhttp://http://github.com/FeishuLuo/Evolving-LLM-Agent-Memory-Survey（140+ 论文、40+ benchmark）
进化框架：记忆的三个阶段
综述的核心观点：Agent 记忆的发展，是"信息密度"不断提升、"认知抽象"不断加深的过程。
阶段一：存储（Storage）——先"记住"
核心问题：怎么把信息存下来？
记忆系列对应	代表	存储了什么
记忆 2（RAG）	Lewis 2020	外部知识文档
记忆 5（Mem0）	Chhikara 2025	提炼后的用户事实
记忆 8（MemGPT）	Packer 2023	上下文的分级管理
记忆 4（KV cache）	—	推理的中间状态
这个阶段的特征：重点是"忠实记录"——信息被保存下来，但还是原始形态。就像人类婴儿时期，大脑开始记录经历，但还不会"分析"。
存储的三种形态（呼应记忆系列第 2-4 篇）：
・Token 级（RAG/Mem0）：文本 + 向量
・参数级（LoRA）：权重增量
・隐空间（KV cache）：隐藏状态
阶段二：反思（Reflection）——学会"管理"
核心问题：存储的信息，怎么筛选、更新、遗忘？
