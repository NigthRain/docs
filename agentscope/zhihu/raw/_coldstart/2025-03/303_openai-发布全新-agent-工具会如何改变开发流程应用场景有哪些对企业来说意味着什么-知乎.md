---
title: OpenAI 发布全新 Agent 工具,会如何改变开发流程?应用场景有哪些?对企业来说意味着什么? - 知乎
author: 段小草
source_url: https://www.zhihu.com/question/14726988892/answer/122986513806?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-03-12 23:47
content_type: Answer
vote_up_count: 19
comment_count: 5
collected_at: 2026-08-18 10:32:51
index: 303/314
---

# OpenAI 发布全新 Agent 工具,会如何改变开发流程?应用场景有哪些?对企业来说意味着什么? - 知乎

> 段小草 | 2025-03-12 23:47

来源: https://www.zhihu.com/question/14726988892/answer/122986513806?utm_medium=openapi_platform&utm_source=1a2112

---

从理念上讲，MCP 的设计和愿景是超过了 Agent SDK 的；从产品上说，Manus 的体验也是最接近 Agent 形态的。所以我不觉得 OpenAI 这波发布狙击了 Manus，Manus 的问题在于没有真正推向市场对所有用户开放使用，而不在于本身能力。还是那句话，Manus 的表现虽然达不到成熟 Agent，但并不弱于 Deep Research。
我个人有时候会觉得 Agent 的路走歪了，现在大家都在研究用户端的 Agent 怎么模拟人类操作，而不去想如何从内容/产品的供给端上给 AI 提供更多便利。这就好比写爬虫的，遇到了反爬，只能用模拟浏览器的方式去采集数据，但是真正程序友好的方式是由对方提供数据接口，这个接口可以限流甚至收费，甚至达到双赢的效果。
我觉得，如果能够形成 AI Agent 是终将来到的共识，那也许有一些网站愿意给 AI 提供更友好的接口，而非浪费海量的算力，去适应当前的 GUI 图形界面，去用视觉方案点击页面元素。
现在的 Agent 有点像纯视觉方案的自动驾驶，由于当前广泛的互联网产品都是为人类用户设计，而不是为 AI Agent 设计，所以模拟人类操作的工程实现，场景泛化能力确实更强。但未来，我们应该会看到更多 LLM-Friendly 的内容格式，看到更多 Agent-Ready 的功能设计，到那时 Agent 才会真正成熟。当然，此处的想法还比较粗浅，等闲了我整理一下，再写完整点。
以下是对播客  ⚡️The new OpenAI Agents Platform - Latent.Space 的内容总结：
OpenAI发布了一批API功能和工具更新，这些更新聚焦于支持AI代理（Agent）的构建，包括Responses API（响应API）、Web Search Tool（网页搜索工具）、File Search Tool（文件搜索工具）、Computer Use Tool（计算机使用工具）以及Agents SDK（代理SDK）。本文将解析这些新功能及其对开发者的意义。
Responses API：为Agentic工作流设计的统一接口
OpenAI的Chat Completions API一直是开发者的核心工具，适用于单轮对话场景。
然而，随着AI应用的复杂性增加，尤其是需要多轮交互和状态管理的agentic工作流（Agentic Workflows），开发者对更灵活的API需求日益迫切。
