---
title: 如何评价 OpenAI 新推出的 Agents SDK 和 Responses API? - 知乎
author: 小橘子
source_url: https://www.zhihu.com/question/14721967679/answer/122445159409?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-03-12 11:55
content_type: Answer
vote_up_count: 27
comment_count: 4
collected_at: 2026-08-18 10:32:51
index: 304/314
---

# 如何评价 OpenAI 新推出的 Agents SDK 和 Responses API? - 知乎

> 小橘子 | 2025-03-12 11:55

来源: https://www.zhihu.com/question/14721967679/answer/122445159409?utm_medium=openapi_platform&utm_source=1a2112

---

概述
3月12日凌晨，OpenAI发布核弹级的Agent框架。OpenAI Agents SDK 构建在一组精心设计的核心组件之上，这些组件协同工作以创建智能代理系统。本文档将分析这套架构的核心组件、它们之间的关系以及设计理念，揭示这一SDK模块化和可扩展的设计思想。
核心组件及其关系
openai-agents-python/
├── src/
│ └── agents/ # 核心SDK代码
│ ├── agent.py # Agent类定义
│ ├── run.py # 运行循环逻辑
│ ├── tool.py # 工具定义
│ ├── handoffs.py # Agent间切换机制
│ ├── guardrail.py # 安全防护机制
│ ├── models/ # 模型实现
│ │ ├── interface.py # 模型接口
│ │ └── openai_chatcompletions.py # OpenAI模型实现
│ └── tracing/ # 运行追踪功能
├── examples/ # 使用示例
│ ├── basic/ # 基础示例
│ ├── tools/ # 工具使用示例
│ ├── handoffs/ # Agent切换示例
│ └── agent_patterns/ # 高级模式示例
└── tests/ # 测试代码
Agent
Agent组件位于层次结构顶端，是SDK中的核心抽象概念，它封装了：
- LLM指令和模型配置：定义大语言模型的行为准则和基本设置
- 可用工具和转接能力：确定代理可以使用哪些工具和何时可以转交控制权
- 输入输出安全防护：设置与用户交互的界限
- 对话上下文管理：维护整个交互的状态和历史
Agent将实际执行委托给Runner组件，实现了配置与运行时行为的清晰分离。
Runner
Runner是SDK的执行引擎，负责：
- 管理用户、LLM和工具之间的对话流：确保信息在各组件间正确传递
- 编排Agent执行循环：控制Agent的生命周期和行为顺序
- 协调工具调用和参数验证：确保工具被正确调用并输入有效
- 处理Agent间转接：使多个专业代理能够无缝协作
- 实施安全防护策略：执行Guardrails定义的安全措施
这种关注点分离遵循单一职责原则，使Runner专注于执行流程管理。
Tool
工具通过允许代理与外部系统交互或执行计算，扩展了Agent的能力范围。
