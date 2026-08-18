---
title: Mixture-of-Transformers (MoT):统一多模态大模型为什么需要的是MoT,而不是MoE? - 知乎
author: AI解析新纪元
source_url: https://zhuanlan.zhihu.com/p/2003243161728861577?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-04-07 22:38
content_type: Article
vote_up_count: 111
comment_count: 12
collected_at: 2026-08-18 10:32:49
index: 186/314
---

# Mixture-of-Transformers (MoT):统一多模态大模型为什么需要的是MoT,而不是MoE? - 知乎

> AI解析新纪元 | 2026-04-07 22:38

来源: https://zhuanlan.zhihu.com/p/2003243161728861577?utm_medium=openapi_platform&utm_source=1a2112

---

写在前面
论文标题：Mixture-of-Transformers: A Sparse and Scalable Architecture for Multi-Modal Foundation Models 
核心标签：多模态稀疏架构、训练效率、模态解耦、MoE替代方案
一、 问题意识：当“统一 Token”遇到“模态隔离”
在多模态大模型（MM-LLM）的研究中，Chameleon 和 Transfusion 等工作确立了一个优雅的范式：将文本、图像、语音全部 Token 化，扔进同一个 Transformer 进行自回归或扩散训练。
这种“Early-fusion”策略虽然统一了架构，却掩盖了一个深层次的矛盾：
虽然我们在形式上统一了 Token，但模型在内部真的把它们当成一回事吗？
我们先看一张概念图，这构成了整篇论文的出发点。
・左侧（Dense）：传统方法试图用同一套参数（Dense Transformer）处理所有模态的输入，忽视了模态间的异质性。
・右侧（MoT）：本文提出的架构，承认模态差异，为文本、图像、语音分配不同的“专家”路径，但在高层语义上保持互通。
论文作者通过对 Dense 模型（如 Chameleon-7B）的特征空间进行 PCA 分析，进一步证实了这种直觉。
・即使没有给予任何先验，模型内部的特征表示依然会自发地按照模态（文本、图像、语音）聚类，占据完全不同的特征空间区域。
・这揭示了一个关键问题：既然不同模态的分布差异如此之大，甚至存在训练动态冲突（Conflicting training dynamics），为什么还要强行让所有模态共享同一套 FFN 和 Attention 投影参数？
传统的解决方案是 Mixture-of-Experts (MoE)，利用 Learned Router 来动态选择专家。但在多模态场景下，MoE 面临着路由负载不均衡、训练不稳定（特别是在异构模态下）以及推理时的因果性难题。
本文提出的 Mixture-of-Transformers (MoT) 给出了一个更本质的回答：与其让模型“学习”如何路由，不如顺应模态差异的本质，直接在架构层面实现“模态感知稀疏性”（Modality-aware sparsity）。
二、 核心方法：确定性解耦与全局交互
MoT 的设计哲学非常直观：解耦计算，统一交互。
1. 架构概览：不仅是分治
MoT 并不是简单地将模型拆分为三个独立的塔，而是保留了 Transformer 最核心的“全局自注意力”机制。
