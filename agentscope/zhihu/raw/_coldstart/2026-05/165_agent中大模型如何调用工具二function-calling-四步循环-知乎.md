---
title: Agent中大模型如何调用工具(二):Function Calling 四步循环 - 知乎
author: 数据与AI爱好者
source_url: https://zhuanlan.zhihu.com/p/2036872796035343343?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-05-10 21:27
content_type: Article
vote_up_count: 38
comment_count: 5
collected_at: 2026-08-18 10:32:49
index: 165/314
---

# Agent中大模型如何调用工具(二):Function Calling 四步循环 - 知乎

> 数据与AI爱好者 | 2026-05-10 21:27

来源: https://zhuanlan.zhihu.com/p/2036872796035343343?utm_medium=openapi_platform&utm_source=1a2112

---

Kevin
第2章：基础模式 — Function Calling 四步循环
2.1 通用四步循环
所有平台的 Function Calling 都遵循同一模式：
2.2 最简 Agent 循环实现（Python）
2.3 解读
关键理解：
・工具定义是 JSON Schema：模型不"知道"工具的实现，只知道它的接口描述
・模型输出的是函数调用请求：tool_calls 包含函数名和 JSON 参数
・应用层负责执行：模型不会自己调 API，它只告诉你"该调什么、传什么参数"
・循环可能多次：一个请求可能需要调多个工具，每次调完都要回传结果让模型继续决策
