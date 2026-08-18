---
title: 被 LangChain 全家桶搞晕了?LangGraph、LangSmith、LangFlow 一文读懂 - 知乎
author: 顶级摸鱼大师
source_url: https://zhuanlan.zhihu.com/p/1977684118427956316?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-03-12 14:36
content_type: Article
vote_up_count: 49
comment_count: 4
collected_at: 2026-08-18 10:32:49
index: 200/314
---

# 被 LangChain 全家桶搞晕了?LangGraph、LangSmith、LangFlow 一文读懂 - 知乎

> 顶级摸鱼大师 | 2026-03-12 14:36

来源: https://zhuanlan.zhihu.com/p/1977684118427956316?utm_medium=openapi_platform&utm_source=1a2112

---

这种模式天然适合处理复杂的逻辑：
・分支：可以根据背包里的状态，决定走不同的箭头。
・循环：可以让箭头指回之前的站点，实现循环追问或重试。
・持久化：可以随时把背包里的状态存起来，下次接着用。
一个基础的 Graph
我们来看一个最基础的 LangGraph 应用，它只有一个调用模型的节点。
from typing import TypedDict, Annotated, List
from langgraph.graph import StateGraph, START, END
from langgraph.graph.message import add_messages
from langchain_openai import ChatOpenAI
from langchain_core.messages import HumanMessage

# 这就是那个“背包”，定义了应用的状态
class State(TypedDict):
    # messages 会自动累积聊天记录
    messages: Annotated[List, add_messages]

llm = ChatOpenAI(model="gpt-4o")

# 这是一个“站点”，接收当前状态，调用模型，并返回要更新的状态
def model_node(state: State):
    reply = llm.invoke(state["messages"])
    return {"messages": [reply]}

# 开始构建图
graph_builder = StateGraph(State)
graph_builder.add_node("model", model_node) # 添加一个名为 "model" 的节点
graph_builder.add_edge(START, "model")      # 从起点连接到 "model" 节点
graph_builder.add_edge("model", END)        # 从 "model" 节点连接到终点

# 编译图，得到一个可执行的应用
app = graph_builder.compile()

# 运行
initial_state = {"messages": [HumanMessage(content="Explain LangGraph in one sentence.")]}

