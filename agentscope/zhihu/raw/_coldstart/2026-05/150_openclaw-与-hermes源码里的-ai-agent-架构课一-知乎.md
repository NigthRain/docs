---
title: OpenClaw 与 Hermes:源码里的 AI Agent 架构课(一) - 知乎
author: 腾讯技术工程
source_url: https://zhuanlan.zhihu.com/p/2043727154320499415?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-05-29 18:18
content_type: Article
vote_up_count: 65
comment_count: 1
collected_at: 2026-08-18 10:32:48
index: 150/314
---

# OpenClaw 与 Hermes:源码里的 AI Agent 架构课(一) - 知乎

> 腾讯技术工程 | 2026-05-29 18:18

来源: https://zhuanlan.zhihu.com/p/2043727154320499415?utm_medium=openapi_platform&utm_source=1a2112

---

・Client 是 Gateway 外部的连接方——TUI 、Control UI、原生OpenClaw App 、Web 聊天页面），也可以是程序。所有 Client 都通过 WebSocket 连入 Gateway，走 Ed25519 认证。
・Channel 是 Gateway 内部加载的插件模块，负责对接一个具体的 IM 平台。它跟 Gateway 之间是函数调用（不需要 WS、不需要鉴权），但它自己会向外连接对应平台的接口——QQ Bot 通过 WebSocket 接收事件 + HTTP 调用 OpenAPI，飞书走 HTTP + Event 订阅，Telegram 走 long poll 或 webhook。
两者通过 SessionKey 交汇：同一个用户可以在手机 OpenClaw App（Client）上看到 QQ Channel 产生的对话，也能在 TUI（Client）里继续回复。SessionKey 把"谁在操作"和"哪条线路"绑在一起（格式 agent:{agentId}:{channelId}:...，详见 §4.1）。
安全约束：
・非 loopback 地址强制 TLS（拒绝明文 ws://，CWE-319）
・TLS SHA-256 证书指纹 Pinning
・控制平面写操作限流（consumeControlPlaneWriteBudget）
・RBAC Scope 最小权限校验
3.3 RPC 方法体系
上述职责在源码中通过 server-methods.ts（39 个直接注册）+ server-aux-handlers.ts（3 个懒加载）共计 42 个 RPC handler 模块落地，下图按功能域归纳为十余类：
3.4 方法授权流程
3.5 Gateway 的 5 大角色与"边界 vs 实现"哲学
把 Gateway 定位为"操作系统内核"——它不是一个普通的消息网关，而是 OpenClaw 区别于 Hermes, Claude Code 等单体 Agent 框架的根本架构选择。
Gateway 同时承担 5 大角色：
角色 1：唯一长驻进程（Single Source of Truth）
 "A single long-lived Gateway owns all messaging surfaces" "One Gateway per host; it is the only place that opens a WhatsApp session."
 
