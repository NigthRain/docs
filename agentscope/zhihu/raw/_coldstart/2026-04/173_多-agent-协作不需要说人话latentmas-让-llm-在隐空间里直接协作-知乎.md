---
title: 多 Agent 协作不需要说「人话」?LatentMAS 让 LLM 在隐空间里直接协作 - 知乎
author: marsggbo
source_url: https://zhuanlan.zhihu.com/p/2032219144121209209?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-04-27 22:14
content_type: Article
vote_up_count: 16
comment_count: 0
collected_at: 2026-08-18 10:32:49
index: 173/314
---

# 多 Agent 协作不需要说「人话」?LatentMAS 让 LLM 在隐空间里直接协作 - 知乎

> marsggbo | 2026-04-27 22:14

来源: https://zhuanlan.zhihu.com/p/2032219144121209209?utm_medium=openapi_platform&utm_source=1a2112

---

1.LatentMAS 的 hidden embeddings 和 TextMAS 的 token embeddings 覆盖了几乎相同的 embedding 区域——说明 latent thoughts 编码了和正确文本回答相同的语义
2.LatentMAS 的分布更广——说明 latent thoughts 比离散 token 具有更高的多样性和表达能力
4.3 对齐矩阵  的作用
如下图，不做对齐的 hidden state （橙色）和原始 input embedding （蓝色）分布差异很大。做完  对齐后的 （绿色）重新和  对齐了：
去掉  后，下游任务准确率下降 2.3%-5.3%。
4.4 最佳 Latent Step 深度
Latent step 并不是越多越好。论文在三个任务上做了 ablation，发现 40-80 步是最佳范围。超过这个范围，性能会平台期甚至下降——过多的 latent step 可能引入冗余信息。
5. 几点个人 Take
这篇工作最让我兴奋的地方不是具体的数字提升，而是它开辟了一个新的思路：多 Agent 之间的通信介质不必是人类可读的文本，可以是模型内部的连续表示。
几个值得关注的点：
1. 完全 training-free 这件事很 impressive。 的构造只用了现有的  和 ，KV cache 传递用的是 HuggingFace 原生接口。没有额外参数、没有训练数据，直接即插即用。这大大降低了实际落地的门槛。
2. 但同构 agent 的假设是个限制。LatentMAS 要求所有 agent 使用相同架构的模型（same transformer layer shape），因为 KV cache 的 dimension 要对齐才能拼接。现实中，强大的 MAS 往往需要不同规模甚至不同架构的模型分工协作。论文也提到了可以用 adapter 做异构对齐，但这就引入了训练，breaking 了 training-free 的优势。
3. 和 KV cache 通信的结合值得深挖。
这篇工作的 KV cache 传递策略非常朴素——全量拼接。
随着 agent 数量增加和 latent step 加深，KV cache 会持续膨胀。
能不能结合 KV cache 压缩（比如上一篇聊的 SemShareKV 的思路）做选择性传递？
这可能是一个有意思的后续方向。
