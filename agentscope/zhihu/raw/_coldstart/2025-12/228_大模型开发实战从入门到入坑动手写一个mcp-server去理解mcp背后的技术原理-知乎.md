---
title: 大模型开发实战从入门到入坑:动手写一个MCP Server去理解MCP背后的技术原理 - 知乎
author: 千问云
source_url: https://zhuanlan.zhihu.com/p/1986482781321205237?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-12-30 12:00
content_type: Article
vote_up_count: 19
comment_count: 0
collected_at: 2026-08-18 10:32:50
index: 228/314
---

# 大模型开发实战从入门到入坑:动手写一个MCP Server去理解MCP背后的技术原理 - 知乎

> 千问云 | 2025-12-30 12:00

来源: https://zhuanlan.zhihu.com/p/1986482781321205237?utm_medium=openapi_platform&utm_source=1a2112

---

前言
"会调接口"早已不是后端工程师的专利——在AI时代，这成了每个想用大模型创造业务价值的Agent开发者必备技能。通过MCP协议让Agent获取业务上下文，已成为行业标配，集团也提供了完善的工具链支持。但当你真正想弄懂MCP时，官网白皮书再精美，也逃不过"一看就懂，一写就懵"的困境。
通过这篇文章可以学习以下内容： 
・手把手带你从0到1实现MCP Server；
・全量剖析MCP协议及背后涉及的技术原理；
・让你彻底告别"只听说过MCP"的尴尬；
一、MCP介绍
什么是MCP？
Q：MCP 究竟是什么？
A：MCP（Model Context Protocol，模型上下文协议）是规范应用程序向大语言模型提供上下文的开放协议。当AI客户端（MCP Host）需要获取上下文时，会通过集成的MCP Client向MCP Server发送请求，由Server返回模型所需的上下文数据。该协议的核心价值在于标准化交互流程——反之，如果AI客户端都不集成MCP Client，那该协议就和AI没有任何关系了。
 一句话：MCP本质上是MCP Client和MCP Server之间的通信协议，实现了Agent开发与工具开发的解耦。
Q：协议具体如何运作
A：由三个核心组件协作：
1. MCP Client：负责发送请求/接收响应
2. MCP Server：处理请求并返回上下文数据
3. MCP Host：MCP协议的执行者。负责：
接收用户问题 → 选择工具 → 构建参数 → 通过Client调用Server → 解析结果 → 继续对话
 集成 MCP Client 的智能体执行平台（如 IDEA LAB）或模型厂商的 Agent/AI 客户端（如 Cherry Studio）均可承担 MCP Host 职能。
Q：MCP Host、MCP Server、MCP Client到底长什么样啊？
以阿里云百练平台为例，MCP Host可以简单理解为平台上的智能体应用
MCP Host长这样子：
MCP Client直接集成在MCP Host中了，所以我们是看不到的。但是我们可以看看自己写一个MCP Client的例子：
@Slf4j
publicclassMcpClient {
    private String baseUri;        // MCP 服务器基础地址
    private String sseEndpoint;    // SSE 连接端点

