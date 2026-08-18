---
title: Tool Calling 是如何工作的 - 知乎
author: sonald
source_url: https://zhuanlan.zhihu.com/p/2036849474916594808?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-05-10 16:50
content_type: Article
vote_up_count: 14
comment_count: 0
collected_at: 2026-08-18 10:32:49
index: 166/314
---

# Tool Calling 是如何工作的 - 知乎

> sonald | 2026-05-10 16:50

来源: https://zhuanlan.zhihu.com/p/2036849474916594808?utm_medium=openapi_platform&utm_source=1a2112

---

我们都知道模型能力很强，只要给 claude code 或者 codex cli 配好 mcp 服务它就能发现和使用它包含的工具。现在如果我们写一个带工具调用能力的 Agent，已经非常简单了。如果你是一个开发人员，在使用大语言模型（LLM）构建智能体应用时，Tool Calling（工具调用/函数调用）也是我们最常用的能力之一。
你只需要给 OpenAI SDK 传入两样东西：一组 messages，再加一组 tools。模型就好像突然拥有了“调用函数”的能力：它会判断什么时候该用工具，用哪个工具，应该传什么参数，然后返回一个结构化的 tool_calls。
但这里有一个很容易被 API 封装盖住的问题：
大模型只是一台文字接龙机器，它只能接收一段连续的字符串（Prompt），再吐出下一个字。它本质上不是一个真正会执行函数的程序。它不是 Python 解释器，也不是操作系统进程。它的核心能力仍然是：接收一段输入，然后继续生成 token。
那 tools 到底去了哪里？
我们在代码里传入的是 JSON 格式的工具定义。模型真正接收到的，难道也是 JSON 对象吗？还是说这些工具定义最终被转换成了一段文字，塞进了 Prompt 里？
更进一步，如果一个多轮对话里，每一轮传入的工具列表都不一样，那么底层 Prompt 会发生什么变化？这会不会影响 prompt cache 或 KV cache 的复用？
这篇文章就沿着这个问题，把 Tool Calling 的端到端链路拆开看一遍。
先说结论：Tool Calling 不是模型真的在执行函数，而是一套由 SDK、推理服务、chat template、模型、tool parser 和宿主程序共同完成的协议栈。
在很多开源模型里，tools 会通过模型自带的 chat_template 被渲染成模型能读懂的文本格式。模型生成符合约定的工具调用文本后，推理服务再把这段文本解析成 OpenAI SDK 里看到的 tool_calls 对象。真正执行工具的，仍然是你的程序。
但这并不意味着所有模型都一定把 tools 明文塞进 system prompt。
对于 OpenAI、Claude 这类闭源托管模型，我们只能看到 API 层接收了结构化 tools，不能直接断言它们内部一定是用某段可见文本实现的。
下面的分析，重点放在我们能观察、能验证的开源模型链路上。
