---
title: eval + builtins:比 tools 更好的 Agent 架构范式 - 知乎
author: 车雄生
source_url: https://zhuanlan.zhihu.com/p/2018257242286209022?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-03-20 12:22
content_type: Article
vote_up_count: 140
comment_count: 28
collected_at: 2026-08-18 10:32:49
index: 194/314
---

# eval + builtins:比 tools 更好的 Agent 架构范式 - 知乎

> 车雄生 | 2026-03-20 12:22

来源: https://zhuanlan.zhihu.com/p/2018257242286209022?utm_medium=openapi_platform&utm_source=1a2112

---

・游戏引擎：Unreal（Puerts）、Godot（GDScript）等
・桌面应用：Electron、VS Code 插件等
・服务端：通过嵌入 V8 / QuickJS 让 LLM 操控后端服务
・硬件 / IoT：嵌入式 JS 引擎 + LLM 生成控制脚本
关键在于：给 LLM 一个可执行的脚本沙盒，加上一组按需加载的辅助函数（builtins），让"写代码"成为 Agent 与环境交互的主要通道。
同时支持原生 Agent 与 MCP 两种接入方式
PuerTsAgent 不局限于单一接入方式。同一套 eval + builtins 核心引擎，同时支持两种使用模式：
・原生 Agent 模式——内置 AI SDK agent（基于 Vercel AI SDK），TypeScript 实现，自带对话管理、历史压缩、上下文图片压缩等能力，直接在 Unity Editor 窗口中对话使用
・MCP Server 模式——基于 @modelcontextprotocol/sdk 在 PuerTS Node.js 后端启动一个 HTTP + SSE 的 MCP Server，将 evalJsCode（及 builtins）暴露为标准 MCP tool。任何支持 MCP 的客户端（Claude Desktop、Cursor、Windsurf、自定义 Agent 等）都可以直接连接使用
两种模式共享同一个 eval-core 模块和同一套 builtins，只是上层协议不同。这意味着你写一套 builtins，就可以同时服务于内置聊天窗口和外部 AI 工具。
可扩展的 Agent 框架
PuerTsAgent 不仅仅是一个编辑器助手。它是一个可扩展的 Agent 框架，你可以用它快速构建任何领域的智能体。
一个 Agent 的全部定义由一个资源目录承载：
Resources/my-agent/
├── system-prompt.md.txt      # 角色定义（你是谁、你能做什么）
├── skills/                   # 领域知识文档（按需加载）
│   └── my-domain.md.txt
└── builtins/                 # 可执行辅助模块（按需加载）
    ├── my-helper.mjs
    └── screenshot.mjs
