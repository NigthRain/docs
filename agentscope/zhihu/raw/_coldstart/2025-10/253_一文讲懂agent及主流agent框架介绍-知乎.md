---
title: 一文讲懂Agent及主流Agent框架介绍 - 知乎
author: 腾讯技术工程
source_url: https://zhuanlan.zhihu.com/p/1962475257895052209?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-10-20 18:02
content_type: Article
vote_up_count: 371
comment_count: 9
collected_at: 2026-08-18 10:32:50
index: 253/314
---

# 一文讲懂Agent及主流Agent框架介绍 - 知乎

> 腾讯技术工程 | 2025-10-20 18:02

来源: https://zhuanlan.zhihu.com/p/1962475257895052209?utm_medium=openapi_platform&utm_source=1a2112

---

1.工作流Workflow类型
2.Agent类型（Function Call）
4.4 CrewAI
简介：CrewAI 是一个多智能体（multi-agent）编排框架，其核心理念是让多个具备特定角色的 AI 代理协同合作（组成“crew”团队）来完成复杂任务。每个代理被赋予特定的角色、目标和背景知识，通过相互分工与配合，自动地进行任务委派和问询，最终以团队形式完成用户交给的工作。
主要特点：多工具及生态集成、支持Workflow和AI Agent两种模式
优势与不足：
优势	不足
工具和生态集成：CrewAI 起初借鉴并构建在 LangChain 生态之上，因而天然支持使用 LangChain 提供的大量工具集合（如搜索、数据库查询、API 接口等）。同时CrewAI 自身及社区提供了许多内置工具，目前已内置超过 40 种工具接口（包括常用的 LLM、云服务、数据库等）以供代理直接使用。	特定功能支持有限： 相较于某些专精的框架，CrewAI 在特定能力上可能不如对手完善。例如，在“AI编程助手”这一场景中，CrewAI 并没有内置像 AutoGen 那样成熟的代码执行与自我纠错循环。如需实现让代理编写并执行代码来完成任务，必须手动集成额外的工具（如运行Python代码的工具）。目前 CrewAI 并未直接提供沙箱执行代码的内置模块，这使它在代码自动生成与执行的任务上稍显不足。
灵活性与深度定制： 在CrewAI的高层模式下，CrewAI 依然保留了很大的灵活性。开发者可以深入定制每个代理的提示（prompt）、工具和内部行为，甚至可以自定义低层的提示模板和代理行为。CrewAI 支持同时结合自主代理（Crews）和精确流程（Flows）两种范式，允许在同一应用中既有自主探索的部分，也有确定顺序的流程，从而无缝融合自治与精确控制。	
使用示例：研究AI agent领域的最新进展
4.5 AutoGen
简介：AutoGen 是微软开源的一个面向 Agentic AI（代理式人工智能）的编程框架，用于构建 AI 智能体并促进多个智能体协作完成复杂任务。AutoGen 支持事件驱动的分布式架构，具有良好的可扩展性和弹性，可用于搭建可自主行动或在人类监督下运行的多代理 AI 系统。
主要特点：微软开源、原生多Agent支持、灵活对话控制
优势与不足：
优势	不足

