---
title: AI Agent 工程实践(11):Workflow——Agent 如何完成复杂任务? - 知乎
author: DeepAgent
source_url: https://zhuanlan.zhihu.com/p/2062133791066527691?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-11 14:05
content_type: Article
vote_up_count: 4
comment_count: 0
collected_at: 2026-08-18 10:32:47
index: 30/314
---

# AI Agent 工程实践(11):Workflow——Agent 如何完成复杂任务? - 知乎

> DeepAgent | 2026-08-11 14:05

来源: https://zhuanlan.zhihu.com/p/2062133791066527691?utm_medium=openapi_platform&utm_source=1a2112

---

同样的链路，不同复杂度用不同实现方式：
范式	适合什么	本质	Agent 场景举例
Pipeline	固定步骤、无分支	线性串联	"翻译 → 润色 → 输出"
DAG	有分支/并行	有向无环图	"同时研究方案A和B → 合并 → 决策"
State Machine	需要回退/重试/异常	状态 + 事件驱动	Planner→Execute→Review（失败回 Execute）
LangGraph	以上三者的工程落地	Graph + State + 条件边	任意复杂 Workflow 的生产实现
选型原则：步骤固定且 >2 步 → Pipeline / 有分支并行 → DAG / 需要回退重试 → State Machine / 真正写代码落地 → 用 LangGraph 表达前三种的任一种。
四种不是互斥的——LangGraph 是前三种的工程实现载体，不是"第四种范式"。
实际收益
指标	超长 Prompt	手动接力	Workflow 编排
步骤完成率	~40%（常丢）	~80%（人漏传）	~95%
错误恢复	无	靠人	自动回退重试
人参与度	低（但质量低）	高（累）	低（自动化）
架构图 / 流程图
带有回退的完整 Workflow（State Machine 视角）
关键：fail · 需重新规划 这条回退边，是 Workflow 区别于 Pipeline 的核心——Pipeline 只能往前，Workflow 能回头。
代码或配置示例
Planner-Execute-Review Workflow（LangGraph 实现）
代码不长，但 Workflow 的全部核心都在里面：状态在节点间传递、条件边决定去向、同一 Agent 换了三个 Skill 跑 Planner/Execute/Review。 这就是第 05 篇 Router 和第 07 篇 Skills 在 Workflow 里的交汇点。
设计权衡
候选方案	优点	缺点	不选的原因
超长 Prompt 硬塞多步	零工程成本	丢步骤、无回退	prompt 不是流程引擎
手动接力	灵活	人不可靠、不可持续	等于没自动化
Pipeline（纯线性）	简单可靠	无分支、无回退	复杂任务必有分支和重试
State Machine Workflow	有回退、有分支、有状态	需工程化	选择理由：唯一能处理"出错后怎么办"的编排方式
Workflow 不是越复杂越好。
