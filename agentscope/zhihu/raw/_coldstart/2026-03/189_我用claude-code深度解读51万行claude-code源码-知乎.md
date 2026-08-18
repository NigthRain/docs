---
title: 我用Claude Code深度解读51万行Claude Code源码 - 知乎
author: 潜龙勿用
source_url: https://zhuanlan.zhihu.com/p/2022433246449780672?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-03-31 22:23
content_type: Article
vote_up_count: 157
comment_count: 10
collected_at: 2026-08-18 10:32:49
index: 189/314
---

# 我用Claude Code深度解读51万行Claude Code源码 - 知乎

> 潜龙勿用 | 2026-03-31 22:23

来源: https://zhuanlan.zhihu.com/p/2022433246449780672?utm_medium=openapi_platform&utm_source=1a2112

---

2026 年 3 月 31 日，Anthropic 通过一次源码快照泄漏了 Claude Code 的完整代码。本文基于这份源码，从工程角度深入剖析这个 AI 编程助手的核心设计——它有多大、用了什么技术、以及最关键的"智能体循环"究竟是怎么运转的。
目录
1.项目概览
2.技术栈全景
3.目录结构详解
4.启动流程
5.核心：Agent Loop
6.工具调用系统
7.流式执行引擎
8.Thinking 推理模式
9.Task 系统
10.Compact 对话压缩
11.Skill 系统
12.Hooks 生命周期扩展
13.高级特性与 Feature Flag
14.关键文件速查表
15.总结：架构亮点与设计哲学
一、项目概览：规模、背景、定位
Claude Code 是 Anthropic 官方出品的 AI 编程 CLI 工具，支持终端、IDE（VS Code / JetBrains）、Web 多端运行。用户通过对话指令让 Claude 直接操作本地文件、执行命令、搜索代码、调用外部工具，完成编程任务。
代码规模
指标	数值
TypeScript/TSX 文件数	1,884 个
总行数	~512,685 行
源码目录大小	35 MB
主入口文件 src/main.tsx	786 KB / 4,683 行
超过 50 万行代码，这不是一个玩具项目——它是生产级工程的体量。
二、技术栈全景
核心技术选型
类别	技术	说明
运行时	Bun	替代 Node.js，启动更快，内置 bundler 和测试框架
语言	TypeScript（strict 模式）	全库严格类型，Zod 作为运行时 schema 校验
终端 UI	React + Ink	在终端中运行 React 组件树
CLI 解析	Commander.js	附带 extra-typings 的类型安全 CLI
Schema 校验	Zod v4	工具输入校验、配置校验
LLM 接入	@anthropic-ai/sdk	Anthropic 官方 SDK，支持流式输出
外部协议	MCP SDK + LSP	工具扩展协议 + 语言服务器协议
遥测	OpenTelemetry + gRPC	懒加载，不阻塞启动
Feature Flag	GrowthBook + bun:bundle	运行时灰度 + 构建时死代码消除
认证	OAuth 2.0 + JWT + macOS Keychain	多层安全存储
代码搜索	ripgrep	GrepTool 内部调用
