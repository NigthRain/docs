---
title: ECCV 2026| 多模态大模型新范式:视觉 token 和计算量如何“自适应瘦身”? - 知乎
author: 多模态机器学习
source_url: https://zhuanlan.zhihu.com/p/2064019409853748499?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-07-24 16:10
content_type: Article
vote_up_count: 12
comment_count: 0
collected_at: 2026-08-18 10:32:48
index: 106/314
---

# ECCV 2026| 多模态大模型新范式:视觉 token 和计算量如何“自适应瘦身”? - 知乎

> 多模态机器学习 | 2026-07-24 16:10

来源: https://zhuanlan.zhihu.com/p/2064019409853748499?utm_medium=openapi_platform&utm_source=1a2112

---

论文标题：Look Less, Think Faster: Joint Token-Compute Adaptation for Multimodal LLMs
 
 作者单位：Purdue University、University of Wisconsin–Madison、NVIDIA
 
📌 论文链接：
 arxiv.org/pdf/2607.2035...
📌 项目主页：
 schaterji.io/publicatio....
一句话总结：作者提出 SmartVL，第一次把"要保留多少视觉 token"和"LLM 要跑多深多宽"这两件事联合训练、联合决策，在同一个计算预算下取得了比单独优化更优的精度-效率曲线。
 
图1：VQAv2上的帕累托前沿。SmartVL相比token剪枝方法（FastV和LLaVA-PruMerge+）、仅计算量控制方法（AdaLLaVA）以及token+计算量组合基线（AdaLLaVA-PruMerge），实现了更强的准确率-效率权衡，凸显了跨维度适配的优势。
引言
多模态大模型（MLLM）现在几乎是视觉-语言任务的标配，但推理成本一直是部署的老大难问题。原因主要有两个：
第一个是 视觉 token 太多：一张图经过 ViT 编码器后往往产生几百个 patch token，这些 token 要和文本 token 一起走完 LLM 的每一层；其次，LLM 本身太重：几十层 Transformer，每层还有多头注意力和 FFN，计算量惊人。
更麻烦的是，这个开销跟输入内容的难易程度没什么关系——一张背景干净的物体图和一张背景杂乱的同款物体图，模型花的计算量是一样的。而现实部署场景里，延迟预算还会随系统负载动态变化。
已有的加速方法，比如 token 剪枝（FastV、LLaVA-PruMerge）或者层/头跳过（AdaLLaVA），基本都是只优化一个维度：要么砍 token，要么砍层。问题是——这两件事其实是耦合的。
token 和 compute "绑在一起"
论文的核心观点很直白：
视觉序列里的 token 冗余度，和 LLM 需要的推理深度，是根本上耦合在一起的。
 
如果视觉端已经把冗余 token 剪得很干净，只留下高信息密度的内容，那 LLM 端其实不需要那么深的推理能力就能处理好；反过来，如果 token 剪得比较保守，LLM 端就该分配更多层数去消化这些信息。
