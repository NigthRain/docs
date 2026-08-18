---
title: 一图看懂LangChain、LangGraph、LangSmith全家桶 - 知乎
author: 跟我学机器学习
source_url: https://zhuanlan.zhihu.com/p/2009551531867922595?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-02-24 08:54
content_type: Article
vote_up_count: 9
comment_count: 2
collected_at: 2026-08-18 10:32:50
index: 211/314
---

# 一图看懂LangChain、LangGraph、LangSmith全家桶 - 知乎

> 跟我学机器学习 | 2026-02-24 08:54

来源: https://zhuanlan.zhihu.com/p/2009551531867922595?utm_medium=openapi_platform&utm_source=1a2112

---

很多人学大模型开发，都会听到一个名字：LangChain。但真正开始做项目时，又会被一堆名词：LangChain、LangGraph、LangSmith、RAG、Tool Calling、Guardrails 绕晕。
那它们之间到底是什么关系呢？
今天我们就根据这张全景图，用一篇文章讲清楚——LangChain 生态到底是怎么分工协作的。
1. LangChain 生态的三层结构
如果用一句话概括：LangChain 负责“搭建能力”，LangGraph 负责“组织流程”，LangSmith 负责“观测优化”。
整套生态可以分成三大核心模块：
・LangChain —— 应用开发框架
・*LangGraph —— 工作流编排与状态管理
・LangSmith —— 可观测与评估系统**
它们构成了一个完整闭环：构建 AI 应用 → 编排复杂流程 → 监控与优化 → 持续迭代
这就是一个成熟 AI 应用的生产级架构。
2. 第一层：构建 AI Chains
LangChain 是整个构建 AI Chains 生态的基础，它本质是一个：大模型应用开发框架（Application Development Framework）。
2.1 核心能力
LangChain 帮我们解决了四件事：① Prompts（提示词管理）；② Models（模型封装）；③ LLMs（大模型调用）；④ API integrations（外部接口集成）。
我们可以理解为：它把“调用大模型 + 接入工具 + 组织逻辑”这件事进行了标准化。
2.2 它解决什么问题？
在没有 LangChain 之前：
・你要自己写模型调用代码
・自己拼 prompt
・自己管理上下文
・自己做工具调用
・自己做文档检索
而 LangChain 提供了：
・RAG 模块
・Tool Calling
・Agent
・Chain 抽象
一句话：LangChain 让你快速搭建 AI 应用。
但问题来了，当我们的应用开始复杂起来怎么办？
3. 第二层： 复杂工作流编排
当应用从“简单问答”升级为：
・多步骤任务
・条件判断
・状态流转
・多 Agent 协作
普通 Chain 就不够用了，这时候就需要 —— LangGraph。
3.1 LangGraph 是什么？
LangGraph 是一个：工作流编排引擎（Orchestration Engine）
它的核心能力包括：State Management（状态管理）、Conditional Branching（条件分支）和 Multi-Step Workflows（多步骤流程）。
