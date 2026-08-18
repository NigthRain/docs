---
title: AI学习Agent系列篇1:Agent本质与自主性设计——从LLM到自主决策系统 - 知乎
author: 无边的界
source_url: https://zhuanlan.zhihu.com/p/2068108038150567398?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-04 22:59
content_type: Article
vote_up_count: 1
comment_count: 0
collected_at: 2026-08-18 10:32:47
index: 65/314
---

# AI学习Agent系列篇1:Agent本质与自主性设计——从LLM到自主决策系统 - 知乎

> 无边的界 | 2026-08-04 22:59

来源: https://zhuanlan.zhihu.com/p/2068108038150567398?utm_medium=openapi_platform&utm_source=1a2112

---

LLM已经能写代码、做推理、通过司法考试——但”让LLM自己决定下一步做什么”仍然是一个未解决的工程难题。模型足够聪明，问题出在”聪明”到”可靠”之间：工具调用可能幻觉参数，记忆可能被污染，规划可能在第三步走偏。Agent不是”加了工具的ChatBot”，而是一套把LLM的推理能力工程化为可靠决策系统的架构。本文拆解这套架构的核心矛盾、四模块设计、全链路循环、自主性光谱与Human-in-the-Loop工程模式。
一、Agent不是什么——四概念边界精确辨析
理解Agent的第一步，不是”Agent是什么”，而是”Agent不是什么”。工业界对Agent、ChatBot、Workflow、Copilot四个概念的混用，导致了大量架构设计错误。
1.1 ChatBot：被动问答
ChatBot的核心特征是无状态的单轮或多轮对话。用户发一条消息，模型返回一段文本，交互结束。没有工具调用，没有任务分解，没有跨会话记忆。
ChatBot的局限很明显：它只能”说”，不能”做”。用户问”我的订单到哪了”，ChatBot只能回复”请提供订单号”或编造一个答案——它没有能力去订单系统里查询。
1.2 Workflow：预定义DAG
Workflow（工作流）是开发者预定义的执行图。每个节点的输入输出、分支条件、执行顺序都在运行前确定。LLM在其中扮演的是”文本处理节点”的角色，而非”决策者”。
Workflow的优势是确定性和可控性——执行路径可预测、可测试、可审计。代价是无法处理未预见的情况：如果用户的需求不在预定义的路由表中，Workflow要么走兜底分支，要么直接失败。
1.3 Copilot：人主AI辅
Copilot的核心理念是人主导、AI辅助。GitHub Copilot是最典型的例子——开发者写代码，Copilot在旁边建议补全；人决定是否接受。决策权完全在人。
Microsoft Copilot Studio在2025年9月的官方文档中明确区分了两类Agent形态（ Microsoft Copilot Studio FAQ）：
・Declarative Agent：基于自然语言提示和预定义动作，不涉及自定义编排逻辑。本质是”配置驱动的Copilot”——开发者在Copilot Studio里用自然语言描述Agent的行为，平台自动编排。
・Custom Engine Agent：开发者使用代码（如AI SDK）编写自定义编排逻辑，控制流完全由开发者定义。这更接近Workflow + LLM的混合体。
