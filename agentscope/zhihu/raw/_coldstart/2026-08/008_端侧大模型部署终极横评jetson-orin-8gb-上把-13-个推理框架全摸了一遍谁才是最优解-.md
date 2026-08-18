---
title: 端侧大模型部署终极横评:Jetson Orin 8GB 上把 13 个推理框架全摸了一遍,谁才是最优解? - 知乎
author: 无敌兔
source_url: https://zhuanlan.zhihu.com/p/2071522829615502619?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-14 09:06
content_type: Article
vote_up_count: 0
comment_count: 0
collected_at: 2026-08-18 10:32:47
index: 8/314
---

# 端侧大模型部署终极横评:Jetson Orin 8GB 上把 13 个推理框架全摸了一遍,谁才是最优解? - 知乎

> 无敌兔 | 2026-08-14 09:06

来源: https://zhuanlan.zhihu.com/p/2071522829615502619?utm_medium=openapi_platform&utm_source=1a2112

---

从 TensorRT-Edge-LLM 五次 OOM 血泪史，到 13 个方案逐个体检，这份踩坑报告帮你少走三个月弯路
适用场景：Jetson Orin 8GB / 边缘设备部署 Qwen2.5 系列 LLM
写在前面
大家好，最近我在 Jetson Orin 8GB 上折腾大模型部署，目标很朴素：把 Qwen2.5 系列跑起来，而且要跑得快、跑得稳，最后还要接 ROS2 做机器人推理。
过程有多惨烈呢？光一个 TensorRT-Edge-LLM 的 1.5B 模型构建，我就 连续 OOM 了五次——容器、宿主机、无桌面环境、最干净的窗口，五个环境全死在同一处 445MB 的 embedding 表分配上。期间还误装过版本（装了面向 Thor 的 v0.9.x，跟我的 JetPack 6.2 完全不兼容），一度怀疑人生。
冷静下来之后，我把市面上能跑 LLM 的推理框架全部调研了一遍：从 NVIDIA 官方的 TensorRT-Edge-LLM，到编译路线的 MLC-LLM，再到解释型的 llama.cpp、服务器级的 vLLM、移动端的 MNN、学术界的 PowerInfer……一共 13 个方案，逐个分析原理、优缺点、开源协议和 Jetson 适配度。
这篇文章就是调研的完整沉淀。结论先放这儿：
Jetson Orin 8GB 上部署 1.5B/3B，MLC-LLM 是综合最优解；0.5B 用已跑通的 TRT-Edge-LLM 守阵地；其余工具按"服务器向 / 移动端向 / 学术向"分类各有定位，不适合作为主引擎。
下面展开讲，全文无废话，所有数据都标了来源。
一、先分清两类：编译型 vs 解释型
13 个工具看着眼花，其实按一条轴就能分清楚：
类别	原理	代表	特点
编译型	把模型编译成目标硬件专属代码（.so / engine），运行时直接执行	MLC-LLM、TRT-Edge-LLM、LMDeploy、ExLlamaV2	性能上限高，但需编译步骤、构建期吃内存
解释型	运行时逐算子解释执行（读 ONNX / GGUF 图）	llama.cpp、ONNX Runtime、MNN	免编译即跑，性能取决于算子优化深度
再补一条轴：服务器级 vs 边缘级。
・服务器级（vLLM、SGLang、ExLlamaV2）：为数据中心 GPU 设计，高并发、大模型、多卡。内存开销大，8GB 边缘设备基本劝退。
・边缘级（MLC-LLM、TRT-Edge-LLM、llama.cpp、MNN、mllm）：单机低功耗、内存受限，拼的就是 tok/s 和峰值内存。
