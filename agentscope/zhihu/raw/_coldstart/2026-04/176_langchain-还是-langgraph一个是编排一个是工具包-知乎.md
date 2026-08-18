---
title: LangChain 还是 LangGraph?一个是编排一个是工具包 - 知乎
author: deephub
source_url: https://zhuanlan.zhihu.com/p/2031114112642578193?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-04-24 20:57
content_type: Article
vote_up_count: 5
comment_count: 0
collected_at: 2026-08-18 10:32:49
index: 176/314
---

# LangChain 还是 LangGraph?一个是编排一个是工具包 - 知乎

> deephub | 2026-04-24 20:57

来源: https://zhuanlan.zhihu.com/p/2031114112642578193?utm_medium=openapi_platform&utm_source=1a2112

---

现在介绍LangGraph 和 LangChain 的文章。每一篇的结论都差不多：简单流程用 LangChain，复杂的用 LangGraph。
但是简单和复杂都是相对的，如果是具体问题呢，比如说一个做代码分析、三个 Agent 串起来的流水线，到底该拿哪一个上线？
所以本文用同一个需求分别用两个框架实现，Agent、逻辑、Gemini 2.5 Flash 调用全部一致，一遍 LangChain，一遍 LangGraph。
两个框架到底在做什么
LangChain 是一个模块化工具包，提供 prompt 模板、文档加载器、retriever、输出解析器、memory 抽象这些零件，再把它们按线性顺序 A → B → C 串起来。像一条传送带：定义步骤，数据往前流，结束。
LangGraph 是一层编排。它把工作流建模成状态机 —— 节点是函数，边是转换 —— 而边可以是条件的。流水线可以循环、分支、重试，也能暂停等待人工输入。就是一张流程图。
不过从 LangChain v1.0（2025）开始，LangChain 自己的 Agent 抽象就是建在 LangGraph 之上的。所以这两个不是两个互相竞争的框架，而是同一个系统不同的抽象层级。
实验：同一条流水线，两个框架
测试用例是一条三阶段的代码审查流水线：
1.Context agent —— 抓 PR diff 和仓库历史
2.Analysis agent —— 在改动代码中定位问题
3.Review agent —— 输出带严重程度评分的结构化反馈
BugLens 线上的 analysis agent 有时需要回头再去拉一轮 context 才能给出有把握的判断。正是这个条件回跳把我逼到了决策点。
LangChain 版本
 from langchain_core.prompts import ChatPromptTemplate  
from langchain_google_genai import ChatGoogleGenerativeAI  
from langchain_core.output_parsers import StrOutputParser  

llm = ChatGoogleGenerativeAI(model="gemini-2.5-flash")  
context_chain = (  
    ChatPromptTemplate.from_template("Analyze this PR diff: {diff}")  

