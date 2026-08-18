---
title: 大模型算法面经:Function Call、MCP、A2A - 知乎
author: 北方的郎
source_url: https://zhuanlan.zhihu.com/p/1898326676087223572?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-05-13 09:28
content_type: Article
vote_up_count: 320
comment_count: 8
collected_at: 2026-08-18 10:32:51
index: 290/314
---

# 大模型算法面经:Function Call、MCP、A2A - 知乎

> 北方的郎 | 2025-05-13 09:28

来源: https://zhuanlan.zhihu.com/p/1898326676087223572?utm_medium=openapi_platform&utm_source=1a2112

---

・LLM 收到来自用户的提示。
・LLM 决定它需要的工具。
・程序员实现过程以接受来自 LLM 的工具调用请求并准备函数调用。
・函数调用（带参数）将传递给将处理实际执行的后端服务。
MCP（即模型上下文协议,Model Context Protocol）试图标准化此过程。 MCP (Model Context Protocol):是一个开放协议和标准，旨在标准化AI 应用（MCP 客户端）如何发现、连接和与外部工具/数据源（实现为 MCP 服务器）进行交互。它关注的是系统间的通信和集成，解决 Function Calling 指令生成后，如何高效、安全、可扩展地执行这些调用。
Function Call侧重于模型想要做什么，而 MCP 侧重于如何使工具可被发现和可消费，尤其是在多个Agent、模型或平台之间。MCP 不是在每个应用程序或代理中硬连接工具，而是：
・标准化了工具的定义、托管和向 LLM 公开的方式。
・使 LLM 能够轻松发现可用工具、了解其架构并使用它们。
・在调用工具之前提供审批和审计工作流程。
・将工具实施的关注与消费分开。
关系:Function Calling 是 LLM 产生调用请求的能力，MCP 是标准化执行这些请求的协议框架。FC 生成指令，MCP 负责让这些指令能在各种工具间通用、可靠地传递和执行。它们是互补的，FC 是 MCP 架构中模型表达意图的方式之一。
具体参考： 北方的郎：LLMs的函数调用（Function Call）和MCP——直观的对比解释
5 MCP与A2A的关系
Agentic 应用需要同时使用 A2A 和 MCP。
・MCP 为智能体提供对工具的访问能力。
・而 A2A 则让智能体之间能够连接和协作组队。
简而言之：
・Agent2Agent（A2A）协议允许 AI 智能体连接其他智能体。
・Model Context Protocol（MCP）让 AI 智能体连接工具/API。
因此，使用 A2A 时，两个智能体可能正在互相对话……而他们本身也可能正在与 MCP 服务器通信。从这个意义上讲，它们并不互相冲突。
如下图所示，Agent2Agent（A2A）协议使多个 AI 智能体可以协同完成任务，而无需直接共享它们的内部记忆、思考或工具。
它们通过交换上下文、任务更新、指令和数据进行通信。
从本质上说，AI 应用可以将 A2A 智能体建模为 MCP 资源，这些资源由它们的 AgentCard（智能体卡片） 表示。

