---
title: 大模型微调实战(七)-基于LoRA微调多模态大模型 - 知乎
author: 吃果冻不吐果冻皮
source_url: https://zhuanlan.zhihu.com/p/670048482?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-06-06 11:52
content_type: Article
vote_up_count: 72
comment_count: 8
collected_at: 2026-08-18 10:32:48
index: 146/314
---

# 大模型微调实战(七)-基于LoRA微调多模态大模型 - 知乎

> 吃果冻不吐果冻皮 | 2026-06-06 11:52

来源: https://zhuanlan.zhihu.com/p/670048482?utm_medium=openapi_platform&utm_source=1a2112

---

随着，ChatGPT 迅速爆火，引发了大模型的时代变革。然而对于普通大众来说，进行大模型的预训练或者全量微调遥不可及。由此，催生了各种参数高效微调技术，让科研人员或者普通开发者有机会尝试微调大模型。
因此，该技术值得我们进行深入分析其背后的机理，之前分享了大模型参数高效微调技术原理综述的文章。下面给大家分享大模型参数高效微调技术实战系列文章，相关代码均放置在GitHub： llm-action。
本文为大模型参数高效微调技术实战的第七篇。本文将结合使用 LoRA 来训练用于图生文的blip2-opt-2.7b模型。
数据集和模型准备
数据集使用6名足球运动员的虚拟数据集，带有可用于微调任何图像描述模型的文字说明。数据集下载地址： huggingface.co/datasets...
模型为利用 OPT-2.7B 训练的 BLIP-2 模型，其由三个模型组成，下面会详细介绍，模型下载地址： huggingface.co/Salesfor...
BLIP-2 简介
BLIP-2 通过利用预训练的视觉模型和语言模型来提升多模态效果和降低训练成本，预训练的视觉模型能够提供高质量的视觉表征，预训练的语言模型则提供了强大的语言生成能力。如下图所示，由一个预训练的 Image Encoder，一个预训练的 Large Language Model 和一个可学习的 Q-Former 组成。
・Image Encoder：负责从输入图片中提取视觉特征。
・Large Language Model：负责文本生成。
・Q-Former：负责弥合视觉和语言两种模态的差距，由Image Transformer和Text Transformer两个子模块构成，它们共享相同自注意力层，如下图所示。
 ・Image Transformer通过与图像编码器进行交互提取视觉特征，它的输入是可学习的 Query，这些Query通过自注意力层相互交互，并通过交叉注意力层与冻结的图像特征交互，还可以通过共享的自注意力层与文本进行交互。
 ・Text Transformer作为文本编码器和解码器，它的自注意力层与Image Transformer共享，根据预训练任务，应用不同的自注意力掩码来控制Query和文本的交互方式。
为了减少计算成本并避免灾难性遗忘的问题，BLIP-2 在预训练时冻结预训练图像模型和语言模型，但是，简单地冻结预训练模型参数会导致视觉特征和文本特征难以对齐，为此BLIP-2提出两阶段预训练 Q-Former 来弥补模态差距：表示学习阶段和生成学习阶段。
