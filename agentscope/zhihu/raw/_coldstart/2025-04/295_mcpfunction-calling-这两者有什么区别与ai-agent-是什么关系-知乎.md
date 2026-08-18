---
title: MCP、function calling 这两者有什么区别?与AI Agent 是什么关系? - 知乎
author: 段小草
source_url: https://www.zhihu.com/question/13800647198/answer/1899244535629980162?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-04-25 23:33
content_type: Answer
vote_up_count: 24
comment_count: 2
collected_at: 2026-08-18 10:32:51
index: 295/314
---

# MCP、function calling 这两者有什么区别?与AI Agent 是什么关系? - 知乎

> 段小草 | 2025-04-25 23:33

来源: https://www.zhihu.com/question/13800647198/answer/1899244535629980162?utm_medium=openapi_platform&utm_source=1a2112

---

在 MCP 成为主流（或者像现在这样流行）之前，大多数 AI 工作流依赖于传统的函数调用 (Function Calling)。
现在，MCP（模型上下文协议，Model Context Protocol）正在为开发者如何为 Agent 构建工具访问和编排带来转变。
下图解释了函数调用与 MCP的对比说明：
让我们深入了解更多！
什么是函数调用 (Function Calling)？ 
函数调用是一种机制，允许 LLM 根据用户的输入识别其需要何种工具以及何时调用该工具。
其典型工作流程如下：
1.LLM 接收来自用户的提示词 (prompt)。
2.LLM 决定其所需的工具。
3.程序员实现相应流程，以接收来自 LLM 的工具调用请求，并准备函数调用。
4.函数调用（附带参数）被传递给负责处理实际执行的后端服务。
让我们快速了解一下实际操作！
首先，我们定义一个工具函数 get_stock_price。它使用 yfinance 库来获取指定股票代码 (stock ticker) 的最新收盘价：
接下来，我们向一个 LLM（通过 Ollama 提供服务）发出 prompt，并传递模型在需要时可以访问以获取外部信息的工具：
打印响应，我们得到：
注意，上述响应对象中的 message 键包含 tool_calls，其中含有相关详细信息，例如：
・tool.function.name：要调用的工具的名称。
・tool.function.arguments：该工具所需的参数。
因此，我们可以利用这些信息生成如下响应：
这会产生以下输出：
注意到整个过程发生在我们的应用程序上下文中。我们需要负责：
・托管和维护工具/API。
・实现用于确定应调用哪个（些）工具及其参数的逻辑。
・处理工具执行并在需要时进行扩展 (scaling)。
・管理身份验证和错误处理。
简而言之，函数调用是关于在您自己的技术栈内实现动态工具使用——但它仍然需要您手动连接所有环节。
什么是 MCP？
MCP，即模型上下文协议 (Model Context Protocol)，试图标准化这一过程。
函数调用关注的是模型想要做什么，而 MCP 则关注工具如何被发现 (discoverable) 和使用 (consumable)——特别是在跨多个 Agent、模型或平台的情况下。
