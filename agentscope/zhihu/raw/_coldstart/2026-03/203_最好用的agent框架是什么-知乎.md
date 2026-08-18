---
title: 最好用的Agent框架是什么? - 知乎
author: 零一猴子
source_url: https://www.zhihu.com/question/1962250618908410064/answer/2012904944932504463?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-03-05 23:22
content_type: Answer
vote_up_count: 1158
comment_count: 669
collected_at: 2026-08-18 10:32:49
index: 203/314
---

# 最好用的Agent框架是什么? - 知乎

> 零一猴子 | 2026-03-05 23:22

来源: https://www.zhihu.com/question/1962250618908410064/answer/2012904944932504463?utm_medium=openapi_platform&utm_source=1a2112

---

关于技术选型，我也让 Claude Code 做了个简单总结：
如果是个人项目，想快速上手，可以选择 pi-mono(Pi)；如果想开发 Web 端的 AI Agent，可以选择 Vercel AI SDK 或者 Mastra；如果想开发一个类似 Claude Code 的本地 Agent 应用，可以选择 Claude Agent SDK；如果想开发企业级的复杂 Agent 应用，可以选择 LangChain/LangGraph。另外如果是 Python 开发者，想快速开发，可以选 Pydantic AI 或者 Agno。
二、框架介绍
接下来简单介绍下上面提到的这些框架。
1. LangChain 和 LangGraph
LangChain 和 LangGraph 都是 LangChain 官方开发的框架，前者出现得更早，大概是在 2022 年，而后者大概是在2024 年诞生的。
LangChain 顾名思义，旨在通过“链式”组合来简化大语言模型（LLM）应用的开发，像早期的 AI 聊天机器人，就通常用 LangChain 来开发。
不过由于 LangChain 是“链式”的线性逻辑，比较难处理需要循环逻辑和复杂状态管理的智能体。为了解决这些痛点，LangChain 官方推出了 LangGraph 作为 LangChain 的扩展库。
相比 LangChain，LangGraph 可以实现复杂的流程编排（循环/分支/重试），支持多智能体协作，支持并行任务，方便实现人机交互。
LangGraph 也是 LangChain 官方目前首推的 Agent 开发框架。不过 LangGraph 通常会和 LangChain 搭配起来使用。如果场景比较简单，LangChain 也够用。
具体如何选择，建议看看官方文档： docs.langchain.com/oss/...
需要注意的是，LangChain 和 LangGraph 诞生得比较早，但由于概念比较多，且 LangGraph 是偏底层（low-level）的框架，学习成本会比较高。
2. Claude Agent SDK
Claude Agent SDK 最早叫 Claude Code SDK，因为能力越来越通用，最近才改了名字。
从它原来的名字（Claude Code SDK）就可以看出，Claude Agent SDK 诞生自 Claude Code，包含了 Claude Code 的底层核心能力。
