---
title: 实战个人Windows本地部署大模型的PD分离架构 - 知乎
author: 大狗狗是狼
source_url: https://zhuanlan.zhihu.com/p/2070186258861762333?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-10 20:02
content_type: Article
vote_up_count: 4
comment_count: 0
collected_at: 2026-08-18 10:32:47
index: 33/314
---

# 实战个人Windows本地部署大模型的PD分离架构 - 知乎

> 大狗狗是狼 | 2026-08-10 20:02

来源: https://zhuanlan.zhihu.com/p/2070186258861762333?utm_medium=openapi_platform&utm_source=1a2112

---

摘要
大模型推理的 Prefill 与 Decode 有截然不同的硬件偏好。Prefill 同时处理大量输入位置，较容易形成高并行度矩阵运算；Decode 每轮只推进一个 token，需要反复读取权重和序列状态。微软研究院的  Splitwise据此把两个阶段分配到不同机器，在相同功耗和成本预算下得到最高 2.35 倍吞吐； DistServe进一步围绕首 token 时延与单 token 时延分别规划资源。
本文在一台 Windows 个人电脑上实现同样的阶段分工。NVIDIA RTX 5080 16G 负责图片编码和 Prefill，AMD MI50 32G 负责 Decode，两个 Vulkan context 之间通过主机内存迁移 Qwen3.6-27B 的完整混合 sequence state。加载模型时选择最大化上下文大小，加载参数ctx=262144，测试实际输入文本 10,000 token，图片组实际输入 10,236 token、10,020 个 M-RoPE 位置，输出统一为 2,000 token。
三次运行的阶段速率中位数显示：
・文本 PD 分离架构的 Prefill 和 Decode 分别为 49.15、13.16 token/s，请求总时间为 355.93 s，输出端到端吞吐为 5.62 token/s；请求总时间相对纯 MI50 缩短 41.91%，相对纯 5080 缩短 50.36%。
・图片 PD 分离架构的总时间为 366.59 s，请求总时间相对纯 MI50 和纯 5080 分别缩短 44.35% 和 49.69%，并正确读出报纸标题 “MEN WALK ON MOON”及 Apollo 11 事件。
Prefill、Decode 与请求时延的分项口径参考了  vLLM 的 PD 指标说明。
现有 PD 系统大多服务于 GPU 集群。
Splitwise、 Mooncake与  NVIDIA Dynamo依赖服务器资源池和高速互联；2026 年的  Moreh 跨厂商实测使用 8 张 H100、16 张 MI300X 和 200 Gbit/s 网络。
截至 2026 年 8 月 10 日，公开资料中尚未出现“原生 Windows、单机 llama.cpp/Vulkan、RTX 5080 预填、MI50 解码、多模态输入与 Qwen 混合状态迁移”这种个人PC异构PD分离方案。
