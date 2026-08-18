---
title: 从链式思想到图状涌现:万字深度解析 LangChain 与 LangGraph 的思想演变与实战精髓 - 知乎
author: 王果ai
source_url: https://zhuanlan.zhihu.com/p/1957395470147118600?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-11-23 14:07
content_type: Article
vote_up_count: 42
comment_count: 4
collected_at: 2026-08-18 10:32:50
index: 238/314
---

# 从链式思想到图状涌现:万字深度解析 LangChain 与 LangGraph 的思想演变与实战精髓 - 知乎

> 王果ai | 2025-11-23 14:07

来源: https://zhuanlan.zhihu.com/p/1957395470147118600?utm_medium=openapi_platform&utm_source=1a2112

---

Python

from langgraph.graph import StateGraph, END
from typing import TypedDict, List

# 1. 定义状态
class ResearchState(TypedDict):
    topic: str
    report: str
    searches: List[dict]
    critique: str
    # 用于控制循环次数，防止无限循环
    revision_number: int

# 2. 定义节点
def search_node(state: ResearchState):
    print("--- 节点: 正在搜索... ---")
    # ... (此处调用搜索工具，例如 TavilySearchResults)
    # 将搜索结果更新到 state
    # ...
    return {"searches": new_searches, "revision_number": state["revision_number"] + 1}

def generate_report_node(state: ResearchState):
    print("--- 节点: 正在生成报告... ---")
    # ... (此处调用 LLM，结合 topic 和 searches 生成报告)
    # ...
    return {"report": new_report}

def critique_report_node(state: ResearchState):
    print("--- 节点: 正在评估报告... ---")
    # ... (此处调用 LLM，对报告进行评估)
    # ...
    return {"critique": new_critique}

# 3. 定义条件边的路由逻辑
def should_continue_router(state: ResearchState):
    print("--- 路由: 判断是否需要修正... ---")
    if state["revision_number"] > 3: # 设置最大修正次数
        print("--- 达到最大修正次数，结束。 ---")

