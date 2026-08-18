---
title: 下一代Agent架构——Pi Agent Core 设计逻辑深度解析 - 知乎
author: 王鹏LLM
source_url: https://zhuanlan.zhihu.com/p/2004665077618458930?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-02-10 21:30
content_type: Article
vote_up_count: 350
comment_count: 31
collected_at: 2026-08-18 10:32:50
index: 215/314
---

# 下一代Agent架构——Pi Agent Core 设计逻辑深度解析 - 知乎

> 王鹏LLM | 2026-02-10 21:30

来源: https://zhuanlan.zhihu.com/p/2004665077618458930?utm_medium=openapi_platform&utm_source=1a2112

---

项目地址： https://http://github.com/badlogic/pi-monohttps://http://github.com/badlogic/pi-mono
核心哲学: "An autonomous agent is just an LLM + tools + a loop."
— Mario Zechner,  What I learned building an opinionated and minimal coding agent
一、Pi 的反直觉立场
在当前 Agent 框架生态中，大多数项目在做加法：更多工具、更长提示词、更复杂的规划链、更多子 Agent。Pi 的创作者 Mario Zechner 认为这是一条弯路。他的核心论点是：
"前沿模型已经被 RL 训练得足够理解'编码 Agent'是什么。你不需要 10,000 token 的系统提示词。"
这不是空谈。Pi 在  Terminal-Bench 2.0 上使用 Claude Opus 4.5 进入了排行榜前列，与 Codex、Cursor、Windsurf 等拥有复杂工具链的 Agent 竞争——而 Pi 的系统提示词 + 工具定义加起来 不到 1000 token。
对比维度	Claude Code	Codex	Pi
系统提示词	约 10,000+ tokens	适中	< 1,000 tokens
内置工具数	数十个	适中	4 个 (read/write/edit/bash)
Plan Mode	有（黑盒子 Agent）	有	无（用文件代替）
MCP 支持	有	有	无（用 CLI 工具代替）
Sub-Agent	有（不可观测）	—	无（通过 bash 自我调用）
二、架构分层：5 个文件构成的运行时
pi-agent-core 的全部源码只有 5 个文件、约 1,500 行代码：
下面逐层剖析每个核心模块的设计决策。
三、类型系统：少即是多
源码： types.ts
3.1 AgentMessage — 应用状态与模型上下文的分离
这是整个设计最精妙的抽象：
为什么不直接用 LLM 的 Message 类型？ 因为真实应用中存在大量"非 LLM 消息"：
场景	消息类型	交给 LLM？
用户提问	UserMessage	✅
Agent 回复	AssistantMessage	✅
工具结果	ToolResultMessage	✅

