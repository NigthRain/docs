---
title: 多智能体协同论文分享Reflective Multi-Agent Collaboration based on Large Language Models - 知乎
author: 李龙
source_url: https://zhuanlan.zhihu.com/p/2001057539928920889?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-02-01 21:35
content_type: Article
vote_up_count: 7
comment_count: 0
collected_at: 2026-08-18 10:32:50
index: 217/314
---

# 多智能体协同论文分享Reflective Multi-Agent Collaboration based on Large Language Models - 知乎

> 李龙 | 2026-02-01 21:35

来源: https://zhuanlan.zhihu.com/p/2001057539928920889?utm_medium=openapi_platform&utm_source=1a2112

---

・Reflexion 不修改模型参数。当模型做错时，它把“错误的解题过程”和“环境的评分”转化成一段文字形式的反思
・Retroformer 不满足于模型自带的反思能力。它使用强化学习（RLHF）去微调（Fine-tune）一个专门的“反思模型”如果生成的反思让 Agent 在下一次做对了，就给这个反思模型奖励；反之就惩罚。
预备知识 (Preliminary)
在本文中，我们使用元组 (N, S, A, P_{\xi_o}, R) 来表示基于 LLM 的多智能体协作系统。
其中 N 代表智能体的数量，S = S_1 \times S_2 \times \cdots \times S_N 是环境状态的联合空间，A = A_1 \times A_2 \times \cdots \times A_N 是联合动作空间，P_{\xi_o}: S \times A \rightarrow S 是状态转移函数。
根据 [38]，我们使用 \xi_o 来表示与状态转移相关的随机性。
在协作设置中，所有智能体共享一个一致的目标，奖励函数 R: (S, A) \rightarrow \mathbb{R} 通常被设计成促进协作的。
协作设置中的一个主要挑战是信用分配（Credit Assignment），这意味着我们需要将 R 分解为 R_1 \times R_2 \times \dots \times R_N，并以标量值的形式评估每个智能体对目标的贡献。
多智能体系统通过与环境的交互来完成目标任务。
这里我们使用轨迹 \tau = \{s_0, a_0, s_1, a_1, \dots, s_T, a_T\} 来表示这一过程，并使用 R(\tau) 描述累积奖励，其中 R(\tau) = \sum_{t=0}^{T} R(s_t, a_t)，T 是轨迹的长度。
在大多数情况下，来自环境的奖励是稀疏的，这意味着 R(s_t, a_t) 大多为零，除了极少数状态，例如指示任务成功或失败的终止状态。
具体而言，对于每个智能体 i，我们将其行动者模型（Actor Model）视为一个函数 M^i_{\xi_l}: X_i \rightarrow A_i，其中 X_i 是提示词（Prompts）的空间，\xi_l 表示采样过程中涉及的随机变量。
为了保持智能体的通用能力，本文选择参数冻结的 LLM（如 ChatGPT 和 GPT-4）作为行动者模型。
