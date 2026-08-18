---
title: 什么是 AI Agent(智能体)? - 知乎
author: 小林coding
source_url: https://www.zhihu.com/question/661759314/answer/2041107661014429807?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-05-22 10:46
content_type: Answer
vote_up_count: 15
comment_count: 3
collected_at: 2026-08-18 10:32:49
index: 157/314
---

# 什么是 AI Agent(智能体)? - 知乎

> 小林coding | 2026-05-22 10:46

来源: https://www.zhihu.com/question/661759314/answer/2041107661014429807?utm_medium=openapi_platform&utm_source=1a2112

---

为什么工具调用如此重要？因为它一下子突破了前面说的三个局限。知识被冻结？接上搜索引擎，模型就能获取实时信息。不能行动？接上邮件 API、代码执行器，模型就能真正做事。这就好比一个人原来只能用嘴说话，现在给他配了手、脚和各种工具，能力上限瞬间拔高了一个量级。
我来举个最具体的例子。假设你给 Agent 配了两个工具：查天气和发邮件，然后让它「帮我查一下北京天气，发邮件给老板」：
# 这里定义了两个工具，就像给 Agent 配了两个「技能说明书」
# 注意：这里没有一行真正执行的逻辑，只是告诉模型「我有哪些能力、需要哪些参数」
tools = [
    {
        "name": "get_weather",
        "description": "获取指定城市的当前天气",
        "parameters": {
            "type": "object",
            "properties": {
                "city": {"type": "string", "description": "城市名称"}
            },
            "required": ["city"]
        }
    },
    {
        "name": "send_email",
        "description": "发送邮件给指定收件人",
        "parameters": {
            "type": "object",
            "properties": {
                "to": {"type": "string"},
                "subject": {"type": "string"},
                "body": {"type": "string"}
            },
            "required": ["to", "subject", "body"]
        }
    }
]
​
# 你告诉 Agent："帮我查一下北京天气，然后发邮件给 boss@company.com"

