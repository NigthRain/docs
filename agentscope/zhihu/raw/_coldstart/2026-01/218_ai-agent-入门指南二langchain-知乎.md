---
title: AI Agent 入门指南(二):LangChain - 知乎
author: VoidOc
source_url: https://zhuanlan.zhihu.com/p/1992600416882537114?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-01-31 15:36
content_type: Article
vote_up_count: 141
comment_count: 4
collected_at: 2026-08-18 10:32:50
index: 218/314
---

# AI Agent 入门指南(二):LangChain - 知乎

> VoidOc | 2026-01-31 15:36

来源: https://zhuanlan.zhihu.com/p/1992600416882537114?utm_medium=openapi_platform&utm_source=1a2112

---

而且全新的统一文档站点（ Home - Docs by LangChain）也正式上线了！ 齐活儿！
LangSmith——Agent 构建平台
除此之外，LangChain 团队还做了 LangSmith。 LangSmith 是他们于 2023 年夏天就同期推出（beta 版）并且慢慢迭代的商业 SaaS 平台（也支持免费体验），可以理解为“调试器 + CI/CD + 监控仪表盘”（也支持自托管 self-host）。
LangSmith 专注于 LLM 应用的可观测性、测试、评估和部署，而且它可以解耦合于 LangChain ——也就是说，你可以不使用 LangChain 而直接使用 LangSmith（例如用纯 OpenAI API 或其他框架构建应用、甚至不用任何框架）。它对 LLM 中立，对底层框架中立，延续了团队“开放、可组合”的工具哲学。
生态关系总结
LangGraph：独立的 runtime 库，提供底层图执行引擎与状态管理；你可以完全不用 LangChain，只用 LangGraph + 原生 LLM 调用（如 OpenAI API）来构建智能体。官方示例中有大量“纯 LangGraph”项目（例如  langgraph-py/examples 中的 chatbot.py 只用了 @app.add 和自定义函数）。
LangChain：更上层的 Agent Framework，提供抽象层（如 ChatModel, LLM）、中间件、工具封装（Tools, Toolkits）等高层接口。从 LangChain 0.2+ 版本开始，其新一代 Agent 架构（如 create_react_agent, create_tool_calling_agent）底层默认使用 LangGraph 作为执行引擎。
但 LangChain 的其他部分（如 Chains、Retrievers）可以独立于 LangGraph 运行。
DeepAgents：是一个独立的 Agent 套件库，专为构建能处理深度、多步骤任务而设计。
它不修改底层运行时逻辑，而是基于 LangGraph 和 LangChain 的能力进行组合与增强。
DeepAgents 构建在 LangGraph 之上 + 深度集成了 LangChain 的组件生态，无需重复造轮子。
但它本身是一个可选的上层库。
LangChain 或 LangGraph 的用户可以选择是否引入 DeepAgents，就像选择是否使用某个高级 Agent 模板。
