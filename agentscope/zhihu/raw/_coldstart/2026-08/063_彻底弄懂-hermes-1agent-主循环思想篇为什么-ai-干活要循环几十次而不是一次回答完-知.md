---
title: 彻底弄懂 Hermes 1:Agent 主循环(思想篇)——为什么 AI 干活要循环几十次,而不是一次回答完 - 知乎
author: 锤同学LikeMath
source_url: https://zhuanlan.zhihu.com/p/2068285933011653727?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-05 10:44
content_type: Article
vote_up_count: 3
comment_count: 1
collected_at: 2026-08-18 10:32:47
index: 63/314
---

# 彻底弄懂 Hermes 1:Agent 主循环(思想篇)——为什么 AI 干活要循环几十次,而不是一次回答完 - 知乎

> 锤同学LikeMath | 2026-08-05 10:44

来源: https://zhuanlan.zhihu.com/p/2068285933011653727?utm_medium=openapi_platform&utm_source=1a2112

---

2022 年，普林斯顿和 Google 的研究者提出 ReAct（Reason + Act，推理 + 行动），2023 年发表在 ICLR。它的核心思想是三个动作交替循环：
・Thought：模型思考当前情况，决定下一步
・Act：采取一个行动（调用工具、查资料）
・Observe：观察行动的结果
把 ReAct 和 function calling 合在一起，就得到一个真正的 Agent 循环。以"帮我查最近的 AI 论文并写个摘要"为例：
这就是"循环"的含义：模型每轮决定要不要调用工具，调用完，结果回到模型手里，模型再看、再想、再决定。直到它觉得信息够了，不再调用工具，输出纯文本——循环结束。
注意关键点：工具结果回填。模型不是凭空幻想搜索结果，它看到的是程序真正执行工具后返回的真实数据。这个"真实世界的反馈"就是 Observe 环节——它让模型从"闭卷考试"变成了"开卷考试"，而且试卷可以反复查。
从 Chatbot 到 Agent，两次跃迁，一张图总结：
回到 Hermes：主循环到底长什么样
把上面的思想翻译成工程实现，就是 agent/conversation_loop.py（7040 行）里的主循环。用伪代码还原它的骨架（细节留到后续几篇）：
几个细节值得注意（后面几篇会逐一展开）：
・消息列表是整个循环的"黑板"：对话历史、工具结果，全都在同一个消息列表里。模型每轮看到的，是完整的历史加最新的工具结果。这就是 ReAct 里 Observe 的载体。
・工具调用由程序执行，不由模型执行：模型只负责"说"要调什么，真正执行的是 Hermes 的代码（调用 handle_function_call 分发到具体工具）。模型永远碰不到你的系统，它只发指令——这是 Agent 安全性的根基。
・循环必须有限制：如果模型一直调用工具停不下来怎么办？Hermes 有迭代预算（默认 90 次）、有宽限机制，防止无限消耗。这是下一篇的内容。
本质之问：循环，是 Agent 与 Chatbot 的分水岭
我的理解是：Chatbot 是一次问答，Agent 是一个循环。
Chatbot 模式下，模型收到你的话，凭记忆生成回复。它不查资料（或只查一次）、不执行代码、不反复试错。它的能力上限 = 训练数据 + 推理能力。
Agent 模式下，模型可以反复行动、观察、调整。
它的能力上限 = 训练数据 + 推理能力 + 工具的世界（搜索、代码、文件、API……）。
