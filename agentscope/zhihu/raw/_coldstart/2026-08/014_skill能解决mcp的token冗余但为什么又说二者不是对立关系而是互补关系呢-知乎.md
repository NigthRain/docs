---
title: SKILL能解决MCP的token冗余,但为什么又说二者不是对立关系而是互补关系呢? - 知乎
author: 数据与AI爱好者
source_url: https://www.zhihu.com/question/1986836032759562965/answer/2070960526897705071?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-12 19:51
content_type: Answer
vote_up_count: 20
comment_count: 0
collected_at: 2026-08-18 10:32:47
index: 14/314
---

# SKILL能解决MCP的token冗余,但为什么又说二者不是对立关系而是互补关系呢? - 知乎

> 数据与AI爱好者 | 2026-08-12 19:51

来源: https://www.zhihu.com/question/1986836032759562965/answer/2070960526897705071?utm_medium=openapi_platform&utm_source=1a2112

---

把我们所有的配置的的工具（有的工具是MCP）作为上下文塞到提示词中去，
比如，“我想查询一下上海的天气”，大模型会从上下文的工具列表中找到查询天气的MCP，这些MCP通常包含：1.名称 2.描述 ...
大模型根据 名称，描述，选择合适工具，比如查询天气的MCP工具，然后组装好参数，比如日期+地点，提交MCP执行。
需要注意的是，为了适应不同需求，每次需要把所有的工具组装到提示词中去，因为智能体无法预判什么时候需要调用工具，需要调用哪个工具。
如果有十几个工具、几十个工具、上百个工具呢，这会占用大量的提示词。
Skill可以做什么呢？
工具调用作为Skill的组成部分，完成特定任务的skill之需要配置相应的工具，比如研究报告的skill，需要搜索MCP工具、写文档的MCP工具、一些命令行工具等。
大模型完成任务时调用skill，直接是使用skill中的工具，可与无需加载所有的工具。
 这就是你说的“引入skill能够解决mcp带来的一次加载所有tool信息的上下文的臃肿的问题”
