---
title: #9、如何使用SpringAI实现自主规划智能体? - 知乎
author: 钱六两
source_url: https://zhuanlan.zhihu.com/p/2069921123995858816?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-09 23:05
content_type: Article
vote_up_count: 0
comment_count: 0
collected_at: 2026-08-18 10:32:47
index: 40/314
---

# #9、如何使用SpringAI实现自主规划智能体? - 知乎

> 钱六两 | 2026-08-09 23:05

来源: https://zhuanlan.zhihu.com/p/2069921123995858816?utm_medium=openapi_platform&utm_source=1a2112

---

执行完后，智能体的 messageList 已经包含了这一轮的"思考 + 工具结果"。下一轮循环的 think() 会带着这些新信息重新问模型——观察（Observe）环节就这样完成了。
5.3.4 终止循环的关键：识别 doTerminate
自主规划必须让模型自己决定什么时候收手。本次提交在 act() 末尾检查工具响应里是否包含 doTerminate 工具，一旦命中就把智能体状态置为 FINISHED，下一轮 while 判断就会退出循环：
为什么用"工具"而不是"特殊输出标记"来结束？ 因为工具调用是模型最擅长的结构化表达方式。让"结束任务"成为一个可被模型自主选择调用的工具，比让模型在自由文本里输出某个暗号可靠得多。
5.4 LoveManus —— 最终可用的超级智能体
有了前三层的骨架，最后一步就是装配。LoveManus 继承 ToolCallAgent，只需要配置：工具、模型、提示词、最大步数。
这里藏着几条关键实现思路：
配置	作用	实现思路
SYSTEM_PROMPT	定义智能体的身份与总目标	一句话让模型知道"你是全能助手，可以用工具解决任何任务"
NEXT_STEP_PROMPT	定义每一步的决策策略	引导模型"主动选工具、复杂任务拆步做、每步后解释结果、需要时调用 terminate"
setMaxSteps(50)	最大循环步数	防止模型陷入无限循环，是自主规划的安全阀
@Qualifier("openAiChatModel")	指定注入的模型 Bean	通过 Spring 的 Qualifier 明确选择 OpenAI 兼容模型端点
defaultAdvisors(new MyLoggerAdvisor())	打印每次 LLM 调用的详细日志	便于开发期观察每一步的思考过程
super(toolCallbacks, toolCallbackProvider)	同时传入两路工具来源	静态工具数组 + 动态工具 Provider 双保险
关键洞察：自主规划智能体的"人格"，其实全写在 Prompt 里。 代码骨架负责"循环和工具"，而"怎么拆任务、怎么选工具、什么时候收手"这些智能行为，全靠 SYSTEM_PROMPT + NEXT_STEP_PROMPT 引导出来。Prompt 设计在自主规划智能体中的地位，不亚于代码本身。
6. 终止工具与循环安全
6.1 终止工具：自主规划的安全阀
