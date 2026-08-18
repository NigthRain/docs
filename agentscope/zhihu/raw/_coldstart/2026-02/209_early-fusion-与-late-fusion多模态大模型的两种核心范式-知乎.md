---
title: Early Fusion 与 Late Fusion:多模态大模型的两种核心范式 - 知乎
author: 简枫
source_url: https://zhuanlan.zhihu.com/p/2008312941645149174?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-02-26 10:15
content_type: Article
vote_up_count: 50
comment_count: 0
collected_at: 2026-08-18 10:32:50
index: 209/314
---

# Early Fusion 与 Late Fusion:多模态大模型的两种核心范式 - 知乎

> 简枫 | 2026-02-26 10:15

来源: https://zhuanlan.zhihu.com/p/2008312941645149174?utm_medium=openapi_platform&utm_source=1a2112

---

多模态大模型在处理视觉、语音与文本的跨模态交互时，Early Fusion 与 Late Fusion 是两种核心的架构范式。
一、 Early Fusion
在 MLLM 语境下，早期融合通常指原生多模态架构。模型没有深层、独立的不同模态编码器，而是在输入层将所有模态转换为统一格式（如 Token 或连续向量），随后输入到同一个 Transformer 骨干网络中进行联合计算。
1. 架构特点
・统一的输入空间：图像、音频等非文本模态被直接切块（Patch）或通过离散化分词器（如 VQ-VAE）转化为 Token 序列，与文本 Token 拼接在一起。
・深层跨模态交互：不同模态的信息从 Transformer 的第一层就开始进行 Self-Attention 计算，模态间的特征融合贯穿整个网络的深度。
・代表模型：Meta Chameleon、Adept Fuyu、Google Gemini（部分原生特性）。
2. 工程实现与挑战
・数据预处理：需要构建高度复杂的 Interleaved 多模态数据集。工程上需要精细处理不同模态 Token 的位置编码，例如为图像块分配二维位置编码，为文本分配一维位置编码。
・Tokenizer 设计：如果是离散化早期融合，需要训练高质量的视觉/音频 Tokenizer，使得非文本模态的离散 Token 具备良好的信息压缩率和语义表达能力。
・计算复杂度：序列长度极长。图像转化为 Token 后会大幅增加 Context Window 的压力，对 KV Cache 的显存占用极高。工程上常需要引入 Ring Attention 或长序列优化技术。
・训练成本：通常需要从头开始预训练，对算力和数据规模的要求极高，很难直接复用现有的单模态预训练权重。
二、 Late Fusion
在现阶段的开源 MLLM 中，最主流的范式实际上是这种基于特征对齐的晚期融合（有时也被细分为中期融合）。它依赖于预训练好的独立单模态编码器，在深层特征空间进行模态拼接或交叉注意力映射。
1. 架构特点
・模块化解耦：包含独立的模态编码器（如处理图像的 CLIP-ViT）、对齐连接器（Connector/Adapter）和 LLM 骨干网络。
・浅层跨模态交互：视觉或音频先在自身的编码器中提取出高维抽象特征，然后通过连接器映射到 LLM 的文本词 Embedding 空间中，LLM 本质上还是在处理被伪装成文本的视觉特征。
・代表模型：LLaVA 系列、Qwen-VL、Flamingo。
