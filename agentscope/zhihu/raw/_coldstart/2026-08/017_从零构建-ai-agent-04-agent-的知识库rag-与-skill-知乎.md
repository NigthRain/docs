---
title: 从零构建 AI Agent 04 | Agent 的知识库——RAG 与 Skill - 知乎
author: starLxin
source_url: https://zhuanlan.zhihu.com/p/2070834357166675636?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-12 11:30
content_type: Article
vote_up_count: 0
comment_count: 0
collected_at: 2026-08-18 10:32:47
index: 17/314
---

# 从零构建 AI Agent 04 | Agent 的知识库——RAG 与 Skill - 知乎

> starLxin | 2026-08-12 11:30

来源: https://zhuanlan.zhihu.com/p/2070834357166675636?utm_medium=openapi_platform&utm_source=1a2112

---

给 Agent 装上一个"笔记本"和一个"顾问"，告别胡说八道
上一篇：03 | Agent 的超能力——工具调用。如果你还没理解 Function Calling 的参数推理机制，先回去看第 3 讲。
前面三讲，我们的旅行助手已经能查天气、搜航班、找酒店了。但有一个致命问题——它会编造信息。
你问"杭州西湖要门票吗？"，它可能煞有介事地回答"西湖门票 120 元，学生票半价"——实际上西湖是免费开放的。
这一讲做两件事：用 RAG 给 Agent 装上事实知识库，用 Skill 给 Agent 装上专业知识包。顺便说清楚 Tool、Skill、RAG 三者的区别——这是很多教程避而不谈的。
Agent 最大的毛病：幻觉
LLM 的知识有两个硬伤：
1.截止日期：训练数据停在某个时间点，之后的事一概不知
2.记不精准：它记住的是概率分布，不是精确事实。"西湖门票 120 元"——它不是在撒谎，是真的"记错了"
RAG（Retrieval-Augmented Generation，检索增强生成）就是解法：Agent 回答之前，先去知识库里查一下。就像一个考试可以翻书的 AI——不是靠记忆答题，是靠查资料答题。
普通 RAG vs Agentic RAG
类型	流程	谁决定检索
普通 RAG	用户问 → 检索 → LLM 回答	程序员写死：每次都搜
Agentic RAG	用户问 → LLM 判断 → 需要才搜 → 搜完再判断 → 不够就换个关键词再搜 → 回答	Agent 自己决定：何时搜、搜什么、搜几次
普通 RAG 的问题是：用户说"你好"，它也去知识库搜一轮——浪费。
Agentic RAG 的好处：Agent 自己判断"这个问题需要查知识库吗？"，检索结果不够时自动换关键词重试。检索本身也成了 Agent 行动循环的一环。
第一步：搭建知识库
我们用 Chroma 做向量数据库——轻量、本地运行、免费：
然后灌入 10 条杭州旅游攻略：
💡 为什么是 10 条而不是 1000 条？ 学习阶段，10 条足够展示 RAG 的核心机制。生产环境用几千条也不在话下——Chroma 切换一下 embedding 模型就行。
第二步：把检索包装为 Agent 工具
还记得第 3 讲的套路吗？用 @tool 装饰器把函数变成 Agent 可用的工具。检索也不例外：
关键在 docstring——它定义了 LLM 何时调用这个工具。
