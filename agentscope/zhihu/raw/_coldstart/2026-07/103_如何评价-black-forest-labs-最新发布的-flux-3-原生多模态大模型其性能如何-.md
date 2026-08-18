---
title: 如何评价 Black Forest Labs 最新发布的 FLUX 3 原生多模态大模型?其性能如何? - 知乎
author: VoidOc
source_url: https://www.zhihu.com/question/2063922512287813817/answer/2065046458995418233?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-07-27 12:10
content_type: Answer
vote_up_count: 27
comment_count: 0
collected_at: 2026-08-18 10:32:48
index: 103/314
---

# 如何评价 Black Forest Labs 最新发布的 FLUX 3 原生多模态大模型?其性能如何? - 知乎

> VoidOc | 2026-07-27 12:10

来源: https://www.zhihu.com/question/2063922512287813817/answer/2065046458995418233?utm_medium=openapi_platform&utm_source=1a2112

---

FLUX.1 / FLUX.2

Text + Image
      ↓
Flow Transformer
      ↓
Image
转向：
FLUX.3

Text    Image    Video    Audio    Action
 │        │        │        │        │
 ↓        ↓        ↓        ↓        ↓
Encoder / Token Representation
          │
          ↓
 ┌────────────────────────┐
 │ Multimodal Transformer │
 └────────────────────────┘
          │
          ↓
   Shared World Representation
          │
    ┌─────┼─────┬─────┐
    ↓     ↓     ↓     ↓
  Image Video  Audio Action
图 1 建议直接使用 BFL 官方这张 FLUX.3 架构图：图中 Text、Image、Video、Audio 分别进入对应编码器，中间共享一个 Multimodal Transformer，底部再通过各自 Decoder 输出；Action 则被画成一个可扩展模态。这张图其实是理解 FLUX.3 最关键的一张图。
从这里也能看出来，FLUX.3 虽然继承了 FLUX 系列 Transformer + Flow Matching 的技术路线，但目前官方还没有公布完整 block-level architecture：参数量多少、Image/Video/Audio Tokenizer 怎么设计、Transformer 深度多少、各模态训练比例是多少，目前都没有完整披露。因此现阶段把它称为“XXB MMDiT”其实是不严谨的。可以确认的是，所有能力都来自同一个 underlying multimodal flow model，而且 FLUX.3 是从训练开始就联合学习 Image、Video 和 Audio，而不是先训图片模型、后面再外挂一个 Video Module。
如果简单和上一代做个对比：
	FLUX.2	FLUX.3
核心定位	Visual Intelligence	Real World Model

