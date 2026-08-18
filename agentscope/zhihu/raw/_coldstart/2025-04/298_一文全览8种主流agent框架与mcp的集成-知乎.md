---
title: 一文全览:8种主流Agent框架与MCP的集成 - 知乎
author: AI大模型课程
source_url: https://zhuanlan.zhihu.com/p/1892980641903133254?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-04-08 18:09
content_type: Article
vote_up_count: 47
comment_count: 1
collected_at: 2026-08-18 10:32:51
index: 298/314
---

# 一文全览:8种主流Agent框架与MCP的集成 - 知乎

> AI大模型课程 | 2025-04-08 18:09

来源: https://zhuanlan.zhihu.com/p/1892980641903133254?utm_medium=openapi_platform&utm_source=1a2112

---

大模型Agents开发框架如今已经百花齐放，层出不穷。本文将盘点8种主流LLM Agents开发框架，并介绍如何在每种框架中集成当下备受关注的MCP Server，让Agents系统更方便的接入外部工具。包括：
・OpenAI Agents SDK
・LangGraph
・LlamaIndex
・AutoGen 0.4+
・Pydantic AI
・SmolAgents
・Camel
・CrewAI
01
Open AI Agents SDK
【框架简介】
OpenAI Agents SDK是OpenAI官方推出的轻量级Agent开发框架，旨在方便开发者构建多Agent协作的智能体系统。该SDK源于OpenAI内部实验项目Swarm，并在近期正式推出生产版本。OpenAI Agents SDK的特点是：简单易用、轻量级、专注在最小集功能，并支持转交（Handoffs）、护栏（Guardrails）等很有特点的功能。
【集成MCP】
以下代码演示了如何将OpenAI Agent实例连接到一个搜索的MCP Server，并将其中的工具集成Agent中：
有趣的是，在使用远程MCP Server时，Agents SDK提供了自动缓存工具列表的选项（通过设置cache_tools_list=True）。如果需要手动使缓存失效，可以调用MCP Server实例上的invalidate_tools_cache()方法 。
学习AI大模型是一项系统工程，需要时间和持续的努力。但随着技术的发展和在线资源的丰富，零基础的小白也有很好的机会逐步学习和掌握。
【完整版的大模型 AI 学习资料已经打包好，朋友们如果需要可以点击下方小卡片 100%免费】
02
LangGraph
【框架简介】
LangGraph来自著名的LangChain，是一个用于构建Agentic Workflow的强大框架，它将任务过程建模为有状态的Graph结构，从而可以实现更复杂和结构化的交互。在该框架内集成MCP Server可以在工作流程的各个阶段更精确地控制何时以及如何调用外部工具，从而实现复杂的Agentic系统。
LangGraph的特点是功能强大，你可以使用Prebuilt的接口快速创建Agent，也可以使用Graph定义复杂的Agentic工作流与多Agent系统；缺点是略显复杂。
【集成MCP】
