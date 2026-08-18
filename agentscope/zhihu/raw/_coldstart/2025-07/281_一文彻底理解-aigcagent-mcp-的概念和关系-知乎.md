---
title: 一文彻底理解 AIGC、Agent 、MCP 的概念和关系 - 知乎
author: 腾讯技术工程
source_url: https://zhuanlan.zhihu.com/p/1928117140751362037?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-07-14 17:45
content_type: Article
vote_up_count: 127
comment_count: 7
collected_at: 2026-08-18 10:32:51
index: 281/314
---

# 一文彻底理解 AIGC、Agent 、MCP 的概念和关系 - 知乎

> 腾讯技术工程 | 2025-07-14 17:45

来源: https://zhuanlan.zhihu.com/p/1928117140751362037?utm_medium=openapi_platform&utm_source=1a2112

---

除了使用智能体开发平台快速开发自己的 Agent 以外，还可以使用 sdk 的方式进行开发。2025 年 3 月 11 日，OpenAI 重磅发布  OpenAI Agent SDK！AI 开发范式彻底颠覆！使用 sdk 可以快速配置一个自定义的 Agent 后执行，相比智能体开发平台，sdk 具有更高的灵活性和自主可控性。
同时，在 OpenAI Agent SDK 中，首次引入了 Mulit Agent 的概念。在此之前，通过智能体开发平台，我们开发出来的 Agent 都只是单 Agent。一个单 Agent 的能力有限，只能解决特定领域的一个任务，而一个复杂任务往往需要执行多个领域的任务才能完成。而 OpenAI Agent SDK 可以让开发者定义多个领域的 Agent，并且给这些 Agent 配置一些转交关系，允许某个 Agent 把特定的任务交给另外一个合适领域的 Agent 来执行，多个 Agent 之间协同和互动来完成一个复杂任务。
在 OpenAI Agent SDK 发布以后，coze，和腾讯云智能体开发平台都相继支持了 Multi-Agent 模式。
2.3 Agent 的发展
Agent 目前的发展还处于一个较初期的阶段，但是发展速度很快。在一些垂直领域比如代码生成 Cursor、智能客服、广告营销等方向已经有了比较好的落地。而更通用的 Agent 目前除了看到 Manus 落地以外，还没看到其他比较好的应用模式落地。相信随着时间发展，会有越来越好用，越来越通用的 Agent 应用诞生。
三、MCP
3.1 什么是 MCP
MCP（ Model Context Protocol，模型上下文协议）是由人工智能公司 Anthropic 于 2024 年 11 月 24 日正式发布并开源的协议标准。Anthropic 公司是由前 OpenAI 核心人员成立的人工智能公司，其发布的 Claude 系列模型是为数较少的可以和 GPT 系列抗衡的模型。
3.2 为什么需要 MCP
MCP 协议旨在解决大型语言模型（LLM）与外部数据源、工具间的集成难题，被比喻为“AI应用的USB-C接口“。通过标准化通信协议，将传统的“M×N集成问题”（即多个模型与多个数据源的点对点连接）转化为“M+N模式”，大幅降低开发成本。
在 MCP 协议没有推出之前：
1.智能体开发平台需要单独的插件配置和插件执行模型，以屏蔽不通工具之间的协议差异，提供统一的接口给 Agent 使用；
2.开发者如果要增加自定义的工具，需要按照平台规定的 http 协议实现工具。并且不同的平台之间的协议可能不同；
3.“M×N 问题”：每新增一个工具或模型，需重新开发全套接口，导致开发成本激增、系统脆弱；
4.功能割裂：AI 模型无法跨工具协作（如同时操作 Excel 和数据库），用户需手动切换平台。
