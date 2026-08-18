---
title: 【LLM从入门到优化实战】02-LLM推理的内核与部署:从Token生成机制到vLLM实战 - 知乎
author: Leon
source_url: https://zhuanlan.zhihu.com/p/2062494058837288168?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-04 19:26
content_type: Article
vote_up_count: 9
comment_count: 0
collected_at: 2026-08-18 10:32:47
index: 67/314
---

# 【LLM从入门到优化实战】02-LLM推理的内核与部署:从Token生成机制到vLLM实战 - 知乎

> Leon | 2026-08-04 19:26

来源: https://zhuanlan.zhihu.com/p/2062494058837288168?utm_medium=openapi_platform&utm_source=1a2112

---

「LLLM服务和优化：从入门到优化实战」系列共 10 篇文章，基于《Hands-On LLM Serving and Optimization》(O’Reilly 2026, Chi Wang & Peiheng Hu)：
・【LLM从入门到优化实战】01-模型服务基础认知：从训练完的模型到可用的服务
・【LLM从入门到优化实战】02-LLM推理的内核与部署：从Token生成机制到vLLM实战
・【LLM从入门到优化实战】03-从零搭建LLM服务：Batching、Streaming与多模型架构
・【LLM从入门到优化实战】04-Agent时代的LLM服务架构：RAG、企业部署与Build-or-Buy
・【LLM从入门到优化实战】05-LLM推理瓶颈：GPU内存墙、算术强度与模型加载拆解
・【第 6 篇】06-推理效率三件套：Continuous Batching、注意力内核优化与Prefix Caching
・【第 7 篇】07-模型压缩实战：量化、蒸馏与剪枝
・【第 8 篇】08-进阶优化：Speculative Decoding、多GPU并行与Prefill-Decode分离
・【第 9 篇】09-四大框架深度对比：vLLM、TensorRT-LLM、SGLang、Llama.cpp
・【第 10 篇】10-收官：一次完整的优化实战，以及下一站
本文是「LLM服务和优化：从入门到优化实战」系列的第二篇。
上一篇建立了模型服务的基础认知，本篇钻进LLM推理内部：从自回归生成机制到KV Cache的显存换时间，从Prefill/Decode两个计算阶段到vLLM相比HF 17倍的实测差距。读完你会理解后续所有优化技术在攻什么瓶颈。
要回答这个问题，得先钻进LLM的内部，看清每一次推理到底发生了什么。
一、从RNN到Transformer：为什么今天的LLM都”长这样”
2017年之前，处理文本的主流方案是RNN和它的变体LSTM、GRU。它们的工作方式很符合直觉：从左到右逐词阅读，每读一个词更新一次”记忆状态”，用累积记忆理解后续内容。
但RNN有一个致命缺陷：无法并行化。每个时间步依赖前一步的隐藏状态，你只能一个词接一个词处理，GPU里几千个计算核心大半时间闲着。而且随着文本变长，读到末尾时模型已经”忘记”了开头：长距离依赖的捕捉能力严重退化。
Google在2017年发表的”Attention Is All You Need”论文用Self-Attention机制替代了循环连接。
