---
title: Vibe Coding怎么这么火?——一篇讲透从生态、技术到核心瓶颈 - 知乎
author: 嗟嗟
source_url: https://zhuanlan.zhihu.com/p/1969081946723291915?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-11-04 21:29
content_type: Article
vote_up_count: 28
comment_count: 2
collected_at: 2026-08-18 10:32:50
index: 245/314
---

# Vibe Coding怎么这么火?——一篇讲透从生态、技术到核心瓶颈 - 知乎

> 嗟嗟 | 2025-11-04 21:29

来源: https://zhuanlan.zhihu.com/p/1969081946723291915?utm_medium=openapi_platform&utm_source=1a2112

---

“氛围编码”（vibe coding）这是一个新概念，是今年近期火起来的一个概念，但这并非近期才有的技术/范式。实质上，这就是AI Copilot在Coding任务上的表现形式，早年提出的MetaGPT，以及很早就用大模型训练的GithubCopilot，其实都是vibe coding的早期形态。
1. 什么是Vibe Coding
Vibe Coding（氛围编码）是一种软件开发方法，其中开发人员严重依赖LLM来创建代码。然而，其核心特征并非简单地“使用”AI，而在于开发者与 AI 之间的交互模式。
 Vibe Coding 的关键特征是，开发者通过自然语言设定目标、点评结果、触发重试与迭代，而刻意不做逐行代码审查或完整理解，更关注可运行性与迭代速度。该范式显著降低了原型/MVP 门槛，使非程序员也能做出可用软件，但默认的“代码不审查”前提也带来可预期的工程风险。这是目前学界与业界关于 Vibe Coding 的共同描述。
从何而来？
Vibe Coding 的理念基础可以追溯到 Andrej Karpathy 在 2023 年的断言：“最热门的新编程语言是英语”。
“Vibe Coding”这一术语似乎由 Andrej Karpathy 在 2025 年 2 月正式提出。
这个术语（“Vibe”，即“氛围”或“感觉”）精准地捕捉到了这种开发模式的非精确性、直觉驱动和非结构化的本质，代表了一种根本性的范式转变：从传统编程所要求的精确、有条理、基于逻辑的实践，转向一种动态、会话式、以问题为先的方法。开发者不再需要精确地知道如何实现，只需要大致传达他们想要的“感觉”或意图。
最新的一些参考资料
2. Vibe Coding 生态
1. GitHub Copilot
GitHub Copilot 是 Vibe Coding 浪潮的开创者。Copilot 最初（2021年）的角色是“打字助手” 和代码补全。它在早期由 OpenAI Codex 模型驱动——一个在数十亿行公共代码上微调的 GPT-3 变体。记得在模型刚出现的时候还引起了不少的争议，被说是“抄袭代码”、“不尊重程序员”，但现在发现，这才是未来。
现在，Copilot 已经从依赖单一的 Codex 模型演变为一个复杂的多模型平台。
其当前架构的核心是一个“智能层”，这种动态路由机制会根据任务的复杂性自动选择模型：例如，它可能会使用轻量级、低延迟的模型 (如 o4-mini) 来进行即时的自动补全，同时为 Copilot Chat 中复杂的代码分析或多步推理任务（如“重构这个类”）保留更强大的高端推理模型 (如 GPT-5, o3)。
