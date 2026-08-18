---
title: A Systematic Survey of Prompt Engineering in Large Language Models: Techniques and Applications(待续) - 知乎
author: 马东什么
source_url: https://zhuanlan.zhihu.com/p/1973796194250662182?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-11-21 17:32
content_type: Article
vote_up_count: 2
comment_count: 0
collected_at: 2026-08-18 10:32:50
index: 239/314
---

# A Systematic Survey of Prompt Engineering in Large Language Models: Techniques and Applications(待续) - 知乎

> 马东什么 | 2025-11-21 17:32

来源: https://zhuanlan.zhihu.com/p/1973796194250662182?utm_medium=openapi_platform&utm_source=1a2112

---


在多个领域，优化是一个基础过程，通常涉及迭代技术。Yang 等人 （ 2023）提出了 PROmpting 优化（OPRO），这是一种利用大型语言模型作为优化器的创新方法。与传统方法不同，OPRO 利用自然语言提示，基于问题描述迭代生成解答，从而实现快速适应不同任务和优化过程的定制化。通过线性回归和旅行推销员问题等经典问题的案例研究，展示了大型语言模型在优化中的潜力。此外，研究还探讨了提示词的优化，以最大化自然语言处理任务的准确性，强调了大型语言模型的敏感性。实验表明，在小型训练集中优化提示以实现准确性，可以有效地转化为测试集上的高性能。OPRO 带来了显著的性能提升，OPRO 优化的最高提示在 GSM8K 数据集上比人类设计的提示高出最多 8%，在 Big-Bench 中高达 50%。
理解用户意图
Rephrase and Respond (RaR) Prompting


邓等人（ 2023）的研究关注了探索大型语言模型（LLM）时常被忽视的一个维度：人类思维框架与大型语言模型（LLMs）之间的差异，并引入了“重述与回应”（Rephrase and Respond，简称 RaR）。RaR 允许大型语言模型在单一提示中重新表述和扩展问题，展示了理解力和回答准确性的提升。两步 RaR 变体结合重述和响应 LLMs，在多个任务中实现了显著的性能提升。研究强调，与随意的人类提问不同，重新表述的问题有助于提升语义清晰度并解决固有的模糊性。这些发现为理解和提升大型语言模型在各种应用中的效能提供了宝贵见解。
Take a Step Back Prompting


针对复杂多步推理的持续挑战，Zheng 等人（ 2023）提出了针对高级语言模型如 PaLM-2L 专门设计的步退提示技术。这种创新方法使模型能够进行抽象，从具体实例中提取高层次概念和基本原则。步回提示法包含两步过程，整合抽象和推理。通过广泛实验，将步进提示应用于 PaLM-2L 在 STEM、知识质量保证和多跳推理等多种推理密集型任务中，结果显示推理能力显著提升。显著的性能提升显著，如 MMLU 物理和化学任务提升 7%，TimeQA 提升 27%，音乐类任务提升 7%。

总结
在人工智能领域，提示工程（prompt engineering） 已成为一股重要的变革力量，正在释放大语言模型（LLM）的巨大潜力。
本文旨在作为一篇基础性的综述性资源，从功能目标出发，对 41 种不同的提示工程技术 进行了系统化分类，以激发后续研究，并为提示工程不断发展的创新生态赋能。
