---
title: AI Agent 架构三要素:Loop、Runtime与 Sandbox - 知乎
author: xnliu
source_url: https://zhuanlan.zhihu.com/p/2051723180298056592?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-06-30 18:21
content_type: Article
vote_up_count: 122
comment_count: 11
collected_at: 2026-08-18 10:32:48
index: 136/314
---

# AI Agent 架构三要素:Loop、Runtime与 Sandbox - 知乎

> xnliu | 2026-06-30 18:21

来源: https://zhuanlan.zhihu.com/p/2051723180298056592?utm_medium=openapi_platform&utm_source=1a2112

---

1 概述
1.1 核心定义
现代 AI Agent 系统从用户意图到最终结果的完整生命周期，由三个相互嵌套的核心概念共同承载：
・Agent Loop（智能体执行循环）：即 LLM 驱动的感知→推理→规划→执行→观察→评估的6步循环。决定 Agent 如何决策、迭代和自我纠正。
・Runtime（智能体运行时）：为 Loop 提供工具调用、记忆管理、多 Agent 协作、可观测性等基础设施。目前主流框架包括 LangChain、AutoGen、CrewAI 等。
・Sandbox（安全执行沙箱）：在代码执行、工具调用、文件操作等不可信行为发生前，提供进程、容器或虚拟机级别的隔离保护，防止宿主环境被逃逸或滥用。
1.2 三层架构
三者呈现严格的嵌套关系：
・Sandbox 在最外层：所有 Agent 行为最终都在某个隔离环境中执行
・Runtime 在中间层：为 Loop 提供运行所需的一切基础设施
・Agent Loop 在最内层：是 Runtime 中的一个逻辑循环，调用工具和 LLM

核心关系：
Agent Loop 定义做什么，Runtime 定义怎么做，Sandbox 定义在哪里做及在什么约束下做。三者共同构成一个既自主又安全的 AI Agent 系统。
2. Agent Loop -智能体执行循环
2.1 六步执行流程
标准 Agent Loop 包含以下 6 个步骤：
・Perceive（感知）：收集用户输入、环境状态、历史消息
・Reason（推理）：LLM 分析当前状态，决定下一步行动
・Plan（规划）：将复杂任务分解为子任务，生成行动序列
・Act（执行）：调用外部工具（搜索、代码执行、API 调用等）
・Observe（观察）：收集工具返回结果，更新上下文
・Evaluate（评估）：判断是否完成任务，或需要继续迭代
关键特性：
Loop 是"事件驱动"的——每次工具调用结果都会触发下一轮推理，而非一次性生成全部步骤。
设计陷阱：
Loop 中最常见的问题：死循环（工具永远失败但 LLM 一直重试）和 Token 爆炸（每轮把全部历史塞入 Context Window）。
工程上需设置 max_turns 上限 + 滑动窗口压缩 + 错误重试退避策略。
