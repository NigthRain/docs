---
title: 基于 MCP 的 AI Agent 应用开发实践 - 知乎
author: 信鑫
source_url: https://zhuanlan.zhihu.com/p/32750183539?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-07-28 10:47
content_type: Article
vote_up_count: 221
comment_count: 18
collected_at: 2026-08-18 10:32:50
index: 275/314
---

# 基于 MCP 的 AI Agent 应用开发实践 - 知乎

> 信鑫 | 2025-07-28 10:47

来源: https://zhuanlan.zhihu.com/p/32750183539?utm_medium=openapi_platform&utm_source=1a2112

---

MCP 生态不断发展壮大，越来越多的应用支持 MCP，同时开放平台也提供 MCP Server。同时也有像  Cloudflare、 Composio、 Zapier 使用 SSE / Streamable HTTP 方式将 MCP 进行托管（即接入一个 MCP Endpoint 即接入一批 MCP Servers），通过 Stdio 方式最理想场景是 MCP Servers 和 Agent 系统跑在同一 Docker 容器中（类似 Sidecar 模式）。
・举个例子：接入地图厂商的 MCP Server 后，Agent 具备生活服务工具能力，远远优于单纯依赖搜索的方式。
未来
・目前的 MCP 开发非常初级，在工程化上缺少一套完善的框架来约束和规范。
・根据 MCP Roadmap，未来主要三件事：
 ・Remote MCP Support：鉴权、服务发现、无状态服务，很明显奔着 K8S 架构去的，这样才能构建一个生产级、可扩展的 MCP 服务。根据最近的 RFC Replace HTTP+SSE with new "Streamable HTTP" transport，支持 Streamable HTTP，可以低延迟、双向传输。
 ・Agent Support：提升不同领域复杂的 Agent 工作流，并可以处理更好的人机交互。
 ・Developer Ecosystem：更多的开发者和大厂商参与进来，才能扩展 AI Agent 的能力边界。
・实践下来，MCP Server SSE 并不是理想的方案，因为需要保持连接和 session 状态，而云服务（如 FaaS）更倾向于无状态架构（issue#273），所以最近提出了更适配云场景的 Streamable HTTP Transport。
・MCP 模型调用与 RL 强化学习：如果 MCP 成为未来的规范，那么 Agent 应用能否准确调用各个 MCP，将成为模型 RL 未来需要支持的关键功能。与 Function Call 模型不同，MCP 是一个动态的工具库，模型需要具备对新增 MCP 的泛化理解能力。
・Agent K8S：虽然目前 LLM 和上下文之间建立了标准化的通信协议，但 Agent 之间的交互协议尚未形成统一标准，Agent 服务发现、恢复、监控等一系列生产级问题等解决。目前 Microsoft 的 NLWeb（Natural Language Web）、Google 的 A2A（Agent2Agent） 和社区的 ANP（Agent Network Protocol）在做这方面的探索与尝试。
