---
title: 写在后 Langchain 时代 - 知乎
author: 相位
source_url: https://zhuanlan.zhihu.com/p/1984716911095861438?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-01-09 14:07
content_type: Article
vote_up_count: 449
comment_count: 34
collected_at: 2026-08-18 10:32:50
index: 224/314
---

# 写在后 Langchain 时代 - 知乎

> 相位 | 2026-01-09 14:07

来源: https://zhuanlan.zhihu.com/p/1984716911095861438?utm_medium=openapi_platform&utm_source=1a2112

---

为了解决复杂的逻辑问题，通常采用 CoT + ReAct 范式，它在循环中增加了“思考历史”的存储，让模型能够在行动前进行推理；
而针对长上下文或大规模任务，Map-Reduce 模式采用了系统领域的映射规约思想，通过“分而治之”将大任务拆解并行处理后再进行合并。
当系统需要处理非线性流程时，通用的 Agent 模式采用循环 + 分支结构，允许系统根据判断走向不同路径，包括调用工具，以及调用预定义流程的 sub-agent 并发异步完成任务。更复杂的 Multi-Agent 系统通常利用发布/订阅（Pub/Sub）机制实现多智能体协作，或者采用 Supervisor 模式，由一个上层管理者负责Plan and Execute，将复杂任务层层嵌套并分发给下级子 Agent 完成。
更多范式可以参考一个Github仓库 - Awesome Agentic Patterns
针对复杂的Agent范式和任务场景，从构建可落地、方便迭代管理的大型 Agent 系统角度出发，选择恰当的开发框架是有必要的，而具体框架的选择还需根据业务需求、开发语言和项目规模来定。以下列出一些典型的开发框架，供开新坑时参考选取。
具体的分类并不完全严谨，这里以各框架最突出的优势作为其分类的关键字。
全栈开发框架
涵盖 Agent 从开发、维护、监测、到前端落地的全栈开发框架
LangGraph
 https://http://github.com/langchain-ai/langgraphhttps://http://github.com/langchain-ai/langgraph
开发语言：Python
LangGraph 是由 Langchain 团队开发的一个基于图论的编排框架，其核心特性是将智能体流程建模为带有状态的有向循环图（StateGraph）。它支持循环逻辑、状态持久化和人在回路控制，允许开发者定义细粒度的分支与合并逻辑 。该框架适用于需要高度确定性控制、复杂错误恢复机制以及长时运行的生产级应用场景，如能够自动修正错误的编码助手 。其优势在于对复杂逻辑的精确控制，但需要开发者显式定义状态模式和图结构 。
基于图的 Agent 开发思路很新颖，将Agent 开发包装成了Graph 设计，比较符合直觉和逻辑，在Agent自由度（Agency）方面略有欠缺，学习成本依然较高。
通过 Langchain 家族的其他产品如 LangSmith 等实现具备监测和前端的生产级应用
