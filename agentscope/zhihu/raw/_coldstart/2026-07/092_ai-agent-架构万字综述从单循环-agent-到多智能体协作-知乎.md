---
title: AI Agent 架构万字综述:从单循环 Agent 到多智能体协作 - 知乎
author: 锤同学LikeMath
source_url: https://zhuanlan.zhihu.com/p/2065835617074917857?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-07-29 16:32
content_type: Article
vote_up_count: 1
comment_count: 0
collected_at: 2026-08-18 10:32:48
index: 92/314
---

# AI Agent 架构万字综述:从单循环 Agent 到多智能体协作 - 知乎

> 锤同学LikeMath | 2026-07-29 16:32

来源: https://zhuanlan.zhihu.com/p/2065835617074917857?utm_medium=openapi_platform&utm_source=1a2112

---

AI Agent 架构万字综述：从单循环 Agent 到多智能体协作
如果你在 2025-2026 年间关注过 AI Agent，你大概看过几十种不同的架构——ReAct、Reflexion、Tree-of-Thought、Multi-Agent Debate、MCP 协议……它们之间到底是什么关系？什么样的场景该用哪种架构？
亚利桑那州立大学最新发布的这篇综述论文，把这些碎片拼成了一整张地图。
论文信息
・标题：AI Agent Systems: Architectures, Applications, and Evaluation
・作者：Bin Xu（亚利桑那州立大学）
・发表时间：2026 年 1 月
・arXiv ID：2601.01743
核心：一个三维分类体系
论文的核心贡献是提出了一个三维分类体系，从三个维度理解任何 Agent 架构：
维度一：组件
一个 Agent 系统由六大核心组件构成：
组件	职责	典型实现
LLM 核心	推理引擎	GPT-4o, Claude, DeepSeek
记忆	持久化上下文	MEMORY.md, RAG, SQLite
世界模型	预测环境变化	搜索、模拟器
规划器	拆解任务、制定步骤	ReAct, Plan-and-Solve
工具路由器	决定调用什么工具	MCP 协议, Function Calling
评判器	自检输出质量	Reflexion, Self-Consistency
维度二：编排模式
模式	描述	代表框架
单 Agent	一个 LLM 完成所有步骤	ReAct, AutoGPT
多 Agent 协作	多个专长 Agent 分工	CrewAI, AutoGen
集中式协调	Coordinator 分配任务	Hermes Agent, OpenClaw
去中心化	Agent 之间直接通信	Agent Protocol, SWE-Agent
维度三：部署场景
场景	关键约束	例子
交互式助手	低延迟 > 高准确率	Claude Code
安全关键系统	可靠验证 > 速度	金融交易、医疗诊断
离线批量分析	结果质量 > 推理成本	科学研究、数据处理
