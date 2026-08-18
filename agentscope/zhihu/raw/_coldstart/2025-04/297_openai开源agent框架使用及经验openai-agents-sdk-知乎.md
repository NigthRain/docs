---
title: openai开源agent框架使用及经验(OpenAI Agents SDK) - 知乎
author: 牛肉好吃
source_url: https://zhuanlan.zhihu.com/p/29652548411?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-04-24 11:50
content_type: Article
vote_up_count: 35
comment_count: 4
collected_at: 2026-08-18 10:32:51
index: 297/314
---

# openai开源agent框架使用及经验(OpenAI Agents SDK) - 知乎

> 牛肉好吃 | 2025-04-24 11:50

来源: https://zhuanlan.zhihu.com/p/29652548411?utm_medium=openapi_platform&utm_source=1a2112

---

openai-agent的handoffs是父子代理的关系，父代理可以把任务转交给子代理，子代理可以只能转交给孙子代理，无法回转给父代理。体现在代码上时，也要先定义子代理，再定义父代理，不然就会报错。
这一点对于固定流程的任务效果很好，但是对于需要讨论回转的任务很不友好，想让子代理转交给父代理，只能通过手动代码实现，将子代理的输出作为父代理的输入传入（也可以引入循环），例如这样：
不过这样仍然很死板，用户可能需要完成不同的任务，子代理也不一定就需要转交给这个父代理，在情况多变的场景下，灵活度显然跟不上。这就让人想起了AutoGen的GroupChat机制，这种机制满足了灵活讨论和灵活结束流程的需求，但是仍然有很多不足之处，例如会出现讨论无休止的循环下去，甚至不循环，而是单个agent持续发言导致流程无法结束，在实际使用中，还会遇到莫名的中断问题，没有任何输出和报错，仅仅是GroupChat结束了。
4.Agent as tool
在openai-agent中可以将Agent注册为工具，交给另一个Agent使用，例如这样：
这种方式比直接调用tool效果更好，因为它让一些复杂的tool可以得到更好的调用。
不过实测下来，使用handoffs将发言权转交给time_agent进行工具的调用,比agent as tool的效果更好。
这是因为在handoffs中，time_agent接收对话历史，在agent as tool中，time_agent接收上一个代理生成的输入。
在Agent的构建中，应该尽量构造简单的Agent结构，越简单的Agent结构，效果越好，在时间开销和token开销上也更少。
三、框架特性
1.模型请求格式
框架支持Responses API和Chat Completions API格式响应。
