---
title: LLM后训练|从监督信号的视角理解 SFT、RL 到 OPD 与 OPSD - 知乎
author: 姚远
source_url: https://zhuanlan.zhihu.com/p/2065369932192338649?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-07-29 15:59
content_type: Article
vote_up_count: 16
comment_count: 2
collected_at: 2026-08-18 10:32:48
index: 93/314
---

# LLM后训练|从监督信号的视角理解 SFT、RL 到 OPD 与 OPSD - 知乎

> 姚远 | 2026-07-29 15:59

来源: https://zhuanlan.zhihu.com/p/2065369932192338649?utm_medium=openapi_platform&utm_source=1a2112

---

一. 前言
最近一直在学习和了解大语言模型（Large Language Model, LLM）的后训练技术。除了最常见的监督微调（Supervised Fine-Tuning，SFT）和强化学习（Reinforcement Learning，RL）之外，近年来又出现了在线策略蒸馏（On-Policy Distillation，OPD）和在线策略自蒸馏（On-Policy Self-Distillation，OPSD）等新的后训练范式。OPD 和 OPSD 可以理解为介于 SFT 与 RL 之间的一类训练方法，其中 OPSD 又在 OPD 的基础上进一步推进了这一思路。
尽管近年来出现了多种后训练技术，但万变不离其宗：这些方法本质上都是利用不同形式的监督信号指导模型学习，区别主要在于监督信号的来源与形式。基于这一认识，本文将从监督信号的视角，对 SFT、RL、OPD 和 OPSD 的核心思想进行简要梳理。
注：笔者水平有限，若有错误或理解不当之处，欢迎批评指正，共同学习与进步！
二. 背景
2.1 LLM 生成的最小单元：下一个词元预测（Next-Token Prediction）
要理解 LLM 后训练的基本原理，可以先从模型生成文本的最小单元出发。LLM 并不是一次性生成完整回答，而是根据当前输入和已经生成的内容，不断预测下一个词元（token），直至形成完整的输出序列。从这一层面看，每次 token 预测都可以视为一次在数万乃至数十万个词表类别上的大规模分类任务：模型先计算各 token 的概率分布，再通过解码策略选择或采样下一个 token。换句话说，LLM 的每一步生成，本质上是一次 token 分类任务！
2.2 SFT，RL，OPD与OPSD 的监督信号
既然 LLM 的生成过程由一系列 token 预测组成，那么训练的关键就在于：如何为每一步的 token 预测提供有效的监督信号？从这一视角看，SFT、RL、OPD 与 OPSD 的核心区别主要在于：监督信号的来源和形式不同。具体而言：
・SFT 直接给出标准回答，利用标准回答中的每个 token 作为监督信号，指导模型生成相应的 token；
・RL 先由模型生成完整回答，再根据奖励信号计算回答中各个 token 的优势值，并据此提高或降低相应 token 的生成概率；
・OPD 先由学生模型生成完整回答，再由外部教师根据模型已经生成的内容，逐步给出下一个 token 在整个词表上的概率分布，并利用该分布指导学生模型调整自身的预测分布；
・OPSD 先由模型根据问题生成完整回答，再让同一模型在额外获得标准答案等特权信息的条件下，针对学生生成的每个前缀构造下一 token 在整个词表上的概率分布，并利用该分布指导学生模型调整自身的预测分布。
