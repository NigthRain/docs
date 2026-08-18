---
title: 详尽从零开始设计实现一个AI Agent框架 - 知乎
author: 腾讯技术工程
source_url: https://zhuanlan.zhihu.com/p/2027029874909397801?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-04-13 18:15
content_type: Article
vote_up_count: 191
comment_count: 6
collected_at: 2026-08-18 10:32:49
index: 184/314
---

# 详尽从零开始设计实现一个AI Agent框架 - 知乎

> 腾讯技术工程 | 2026-04-13 18:15

来源: https://zhuanlan.zhihu.com/p/2027029874909397801?utm_medium=openapi_platform&utm_source=1a2112

---

另外，Aman Madaan等受人类改进文本方式的启发，在 《Self-Refine: Iterative Refinement with Self-Feedback》论文提出了一种名Self-Refine的方法，通过迭代反馈和改进来提升 LLM 的初始输出：先让LLM输出，然后再根据输出提供反馈，不断迭代。在所有评估的任务中Self-Refine方法可以使得任务性能平均提升约 20%。
清华大学与微软联合发布的 《CRITIC: Large Language Models Can Self-Correct with Tool-Interactive Critiquing》论文则结合外部工具（如搜索引擎、代码执行器）验证输出，再基于验证结果自我修。
这些里程碑论文都是Reflection模式的理论基础，当前主流的Agent框架虽然有各种演绎与变形，也都是在ReAct提出之后发展出来的扩展和补充，Agent核心实践依旧离不开ReAct：将推理与执行结合起来。
1.2 主流 AI Agent 框架对比
当前主流Agent框架主要包含以下几种：
・LangChain - 最成熟和流行的框架之一，提供丰富的工具链和集成，适合快速构建复杂的AI应用。支持多种LLM、向量数据库和工具调用，有完善的文档和社区支持。
・LlamaIndex - 专注于数据索引和检索，特别擅长RAG（检索增强生成）场景。提供高效的文档处理和查询能力，适合知识密集型应用。
・AutoGPT/AutoGen - 微软推出的多Agent协作框架，支持多个Agent之间的对话和协作，可以处理更复杂的任务分解和执行。
・CrewAI - 专注于角色扮演型Agent的协作框架，每个Agent有明确的角色和目标，适合模拟团队协作场景。
・LangGraph - LangChain团队开发的状态图框架，提供更精细的流程控制，适合构建复杂的、需要明确状态管理的Agent应用。
・Semantic Kernel - 微软的轻量级框架，与Azure服务集成良好，支持多种编程语言，强调插件化设计。
选择建议
・如果是想快速出Agent原型，可以试试LangChain；
・如果是构建RAG应用，则强烈建议LlamaIndex；
・如果业务场景为多Agent协作，推荐AutoGen或CrewAI，它们是专为多智能体协作而生的；
・如果业务中涉及复杂的流程控制，建议使用LangGraph，通用性好，基于状态管理的workflow灵活性高；
・如果工作环境围绕.NET生态展开的，那搭配Semantic Kernel是最佳选项。
