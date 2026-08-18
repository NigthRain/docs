---
title: 3 个 Multi-Agent 系统,把 GPTBots 的多智能体协作玩明白了! - 知乎
author: PaperAgent
source_url: https://zhuanlan.zhihu.com/p/1967727537498089194?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-10-31 23:02
content_type: Article
vote_up_count: 0
comment_count: 0
collected_at: 2026-08-18 10:32:50
index: 248/314
---

# 3 个 Multi-Agent 系统,把 GPTBots 的多智能体协作玩明白了! - 知乎

> PaperAgent | 2025-10-31 23:02

来源: https://zhuanlan.zhihu.com/p/1967727537498089194?utm_medium=openapi_platform&utm_source=1a2112

---

大家好，我是PaperAgent，不是Agent！在往期的文章中我们分享了 如何从0到1动手用GPTBots的Flow-Agent搭建企业数字助理智能体
今天要和大家分享的是如何在GPTBots平台上玩转多智能体(Multi-Agent)系统。
多智能体协作不仅能提升任务处理效率，还能实现单智能体难以完成的复杂任务。

这些多智能体系统通常由专业化的智能体组成，每个智能体都配备了各自的工具集，并由一个监督者进行管理
在GPTBots中默认集成了专家智能体，比如客服、产品经理、测试、程序员等等，开箱即用！

在实践中，有几十种多智能体架构，其核心的一部分是：智能体协调——如何协调所有智能体？ 有三种协作模式：
1.Cooperation(合作): 智能体之间相互配合，共同完成一个目标
2.Competition(竞争): 智能体之间相互竞争，最终选择最优方案
3.Coopetition(竞合): 既有合作又有竞争，智能体在特定环节协作，在其他环节竞争
接下来，通过3个具体案例，玩转多智能体协作模式：
・旅游规划协作系统(Cooperation模式)
・辩论对抗系统(Competition模式)
・商业决策系统(Coopetition模式)
当然小伙伴们也可以照着案例，在GPTBots平台上自己动手玩： gptbots.ai/zh_CN/signup?...
一、旅游规划协作系统(Cooperation模式)
场景: 用户输入目的地和预算，系统自动生成完整的旅游计划
理论架构
[主控Agent] → [景点推荐Agent] → [预算规划Agent] → [行程优化Agent] → [输出Agent]

实践步骤
首先，选择Agent类型，如果预置的客户服务、企业搜索、AI Apps无法满足需求，可选择空白Agent
接着，选择“Multi-Agent”，它由多个专业 AI Agent 组成团队，适用于研究、任务类业务场景：
先看总体的架构图：由4个Agent组成
1.创建主控Agent
・角色: 旅游规划协调员
大模型层面可选较多，可根据实际情况选择：OpenAI、Anthropic、ZhiPu、Google。
1.创建景点推荐Agent
・角色: 旅游景点专家
・Prompt: "你专门负责推荐旅游景点。根据主控Agent提供的城市名称，列出该城市最值得去的5个景点，包括景点类型(自然/人文/娱乐等)、推荐理由和预计游览时间。"
