---
title: AI Agent 的工作原理和架构是什么? - 知乎
author: 手抓饼熊
source_url: https://www.zhihu.com/question/1928852201641579992/answer/2031457550042911468?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-04-25 19:40
content_type: Answer
vote_up_count: 54
comment_count: 1
collected_at: 2026-08-18 10:32:49
index: 175/314
---

# AI Agent 的工作原理和架构是什么? - 知乎

> 手抓饼熊 | 2026-04-25 19:40

来源: https://www.zhihu.com/question/1928852201641579992/answer/2031457550042911468?utm_medium=openapi_platform&utm_source=1a2112

---

推荐agent领域26年4月份最新的2篇论文。
 arxiv.org/pdf/2604.0822...
 arxiv.org/pdf/2604.1422...
Externalization in LLM Agents: A Unified Review of Memory, Skills, Protocols and Harness Engineering
这篇文章把“外部化”作为理解和设计 LLM Agent 的核心视角，认为近几年的关键进展不在于继续单点增强模型参数，而在于通过记忆系统、技能系统、交互协议以及统一的运行框架（harness）把原本由模型内部独立承担的认知负担迁移到可持久、可检查、可组合的外部结构上。
作者回顾了从“能力在权重”到“能力在上下文”再到“能力在基础设施”的演进路径，系统梳理了三种主要外部化形式：记忆将跨时间的状态存到可检索的存储中，从“回忆”变成“识别”；技能把程序性专长封装成可复用的操作包，从即兴生成变成组件化组合；协议则把人与工具、Agent 与 Agent 之间的交互固化为机器可读、可治理的契约，从临时 prompt 变成结构化协作。
三者在 harness 中被统一编排，并形成和模型内部参数能力之间的权衡关系：哪些能力适合放在权重里，哪些更适合外部化，从而在可靠性、可控性、可扩展性之间取得更好的工程平衡，同时也引出自进化框架、共享基础设施、评测与治理等未来研究方向
