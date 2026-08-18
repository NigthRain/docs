---
title: 1.5万字速通LLM主流模型结构(Llama、Qwen、GLM、Deepseek...) - 知乎
author: 魔法学院的Chilia
source_url: https://zhuanlan.zhihu.com/p/2060741715095560795?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-04 09:07
content_type: Article
vote_up_count: 1487
comment_count: 44
collected_at: 2026-08-18 10:32:48
index: 74/314
---

# 1.5万字速通LLM主流模型结构(Llama、Qwen、GLM、Deepseek...) - 知乎

> 魔法学院的Chilia | 2026-08-04 09:07

来源: https://zhuanlan.zhihu.com/p/2060741715095560795?utm_medium=openapi_platform&utm_source=1a2112

---

名词解释——【温度缩放】
在 softmax 前除以温度 T，调整分布的陡峭度。T越小，分布越sharp，越确定。
2.6 Multi-Token Prediction(MTP)
传统的自回归语言模型在训练时，每个位置只预测下一个 token。MTP 则把预测范围扩展到未来多个 token。这样做的motivation主要有两个：
1.增加训练信号密度：每个 token 位置不再只产生一个监督信号，而是同时监督它后续  个 token 的预测。这让模型从同等量级的训练数据中提取更丰富的学习信号，从而提高数据效率。
2.促使模型学习更有前瞻性的表示：要求模型在当前位置就为未来的多个token做出预测，迫使它学习更具前瞻性的表示，而不是仅仅关注眼前的下一个 token。这种提前规划的能力可以增强模型对长程结构的把握。
MTP loss和主LM loss加在一起，同时计算梯度并更新。
MTP 策略的主要目的是提升主模型的训练效果，因此推理时可以直接丢弃所有 MTP 模块，主模型完全独立运行。训练阶段引入的额外监督信号已经内化到了主模型的参数中。当然了，也可以将 MTP 模块用于投机解码。因为MTP 模块本身就是用来预测未来多个 token 的，那么它们天然可以作为投机解码中的draft model，在一次前向传播中生成多个候选 token，再由主模型进行验证，从而加速生成。
名字解释——【投机解码】
投机解码是一种针对自回归LLM的无损推理加速技术。其核心思想是用一个轻量级的草稿模型 (Draft Model)快速生成多个候选 token，再由目标模型 (Target Model)一次性并行验证这些候选 token，通过接受-拒绝机制保证最终生成的文本分布与目标模型逐 token 生成完全一致，从而在保持输出质量不变的前提显著降低推理延迟。
每次小模型自回归地快速预测出γ个候选 token，大模型一次性把【原序列 + 这γ个候选 token】吃进去，算出这个γ位置的输出概率，从前往后逐个检查候选 token 是否在大模型自己的top-k 个选择里。如果相同，就接受，接着检查下一个。一旦出现第一个不被接受的候选 token，后面的全部丢弃。对于这个位置，大模型会修正出一个新 token 来替代。
0x03. Mixture of Expert (MoE)
3.1 MoE的整体结构
在稠密模型中，每个 token 都会经过同一个FFN；而 MoE 的做法是把 FFN 替换为多个并行的FFN，并引入一个路由器（Router），让每个 token 只激活其中的一小部分最合适FFN专家。
