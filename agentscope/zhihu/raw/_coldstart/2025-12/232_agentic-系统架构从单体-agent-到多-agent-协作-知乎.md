---
title: Agentic 系统架构:从单体 Agent 到多 Agent 协作 - 知乎
author: 笨鸟先飞
source_url: https://zhuanlan.zhihu.com/p/1984217673383555123?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-12-16 12:16
content_type: Article
vote_up_count: 14
comment_count: 1
collected_at: 2026-08-18 10:32:50
index: 232/314
---

# Agentic 系统架构:从单体 Agent 到多 Agent 协作 - 知乎

> 笨鸟先飞 | 2025-12-16 12:16

来源: https://zhuanlan.zhihu.com/p/1984217673383555123?utm_medium=openapi_platform&utm_source=1a2112

---

在单体Agent架构下，感知-思考-行动循环通常由一个Agent独自反复执行。它适合单一领域或单用户场景，实现相对简单，易于调试。但当任务变得极其复杂或需要不同领域知识时，一个Agent可能力不从心。而这正是我们接下来要讨论的重点：多 Agent 协作如何通过分工让AI团队发挥更大威力。
二、多 Agent 协作：当 AI 组成团队
当一个Agent难以独自胜任某些复杂任务时，我们可以让多个 Agent 分工合作，组成一个AI团队（Multi-Agent System）。就像现实中不同专长的人组队完成项目一样，多Agent系统中的各Agent可以扮演不同角色、协同解决问题。
1、多Agent协作的核心理念
什么是多Agent协作？简单来说，就是让多个相对独立的智能体，通过适当方式互相通信、共享信息，一起完成某个目标。每个Agent可以有自己的技能、知识和LLM模型，就好比团队中不同成员各有所长。关键在于如何连接这些Agent，也就是设计它们之间的通信和工作流程，使得整个团队配合默契。 常见的多Agent协作模式包括：
・角色分工：为每个Agent设定明确的角色和职责。比如一个项目管理Agent负责规划和分配任务，若干执行Agent各自完成子任务；又如在内容创作场景中，一个Agent生成初稿，另一个Agent专门审核修改。这类似公司里的分部门协作，有人管策划，有人负责实施。
・信息共享：团队Agent可能共享一个公共的记事本或对话板(scratchpad)来记录当前进展。这样所有Agent都能看到彼此的工作产出，方便协同。但也有场景下信息按需传递，而不所有内容都公开，以减少干扰。
・通信方式：大多数多Agent系统让Agent通过自然语言对话沟通，这也是利用LLM特长的直观方式。例如Agent A用一段文字说明自己的结果或请求Agent B协助，然后Agent B读懂后给出回复。这样的对话可以多轮往复，直到得出最终答案。这种以对话为纽带的模式，被微软的AutoGen框架称为“对话式协作”。除了自然语言，也有用更结构化的消息传递或共享内存对象方式的，但核心都是让Agent彼此交换信息、协调行为。
・协调控制：可以是集中式的（一个主导Agent/调度器来管理其它Agent，例如“主管Agent”监督多个“员工Agent”的模式），也可以是分散式的（各Agent根据约定的协议自发交互，没有单一点控）。集中式易于控制和追踪，分散式更灵活且无单点故障，不同应用会选择不同策略。
