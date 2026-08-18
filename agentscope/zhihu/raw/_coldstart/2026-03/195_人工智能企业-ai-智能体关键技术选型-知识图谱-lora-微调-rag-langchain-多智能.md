---
title: 【人工智能】企业 AI 智能体关键技术选型  | 知识图谱| LoRA 微调| RAG | LangChain |多智能体框架| 规则引擎 | AI 护栏 - 知乎
author: 吴开春
source_url: https://zhuanlan.zhihu.com/p/2017631740068398417?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-03-18 16:20
content_type: Article
vote_up_count: 1
comment_count: 0
collected_at: 2026-08-18 10:32:49
index: 195/314
---

# 【人工智能】企业 AI 智能体关键技术选型  | 知识图谱| LoRA 微调| RAG | LangChain |多智能体框架| 规则引擎 | AI 护栏 - 知乎

> 吴开春 | 2026-03-18 16:20

来源: https://zhuanlan.zhihu.com/p/2017631740068398417?utm_medium=openapi_platform&utm_source=1a2112

---

Langchain早期有 SQLDatabaseChain/APIChain ，当前已经升级为更强大的「Agent + 工具调用」模式，优先使用 create_sql_agent（数据库）、@tool 装饰器 / OpenAPI 适配（API）。
需要强调的是, 直接用自然语言来操作数据库的风险很高，通常只限于指定范围内的只读查询，同时还要配合SQL语法白名单校验，保证数据库稳定和安全。
三、教AI「会合作」：与人、系统无缝衔接
3.1 目标及思路
教AI「会合作」，企业要建立AI智能体与企业现有系统、在岗人员的协作机制，优化交接流程，推动AI→人工、人工→AI、系统→系统之间的转接丝滑、自动、不丢信息。
3.2 关键技术诉求
3.2.1 智能体调度框架
在业务流程编排中，BPM建立起了企业完整的业务流程（比如：发起、流转、审批），在其中某个节点，当由人工完全转向全自动化时，通过调用智能体调度框架来完成具体的自动化工作，并将结果返回给BPM。简单点说，在此处，智能体替代一个人工的角色来完成工作。
智能体调度框架会分配具体的AI Agent角色，调用相关的RAG/知识图谱/工具/数据库等执行操作，完成任务并返回。
当前的智能体调度框架有支持LangGraph、crewAI、AutoGPT等, 其中：
・LangGraph：通用智能体流程编排工具，支持多智能体编排，可通过adapter集成AutoGPT/crewAI，负责全局流程编排
・CrewAI：聚焦角色化多智能体协作，专为多智能体分工设计，负责局部角色任务
・AutoGPT：偏向单智能体自主探索，适合无明确流程的开放性任务
实战中，在BPM的某个需要自动化的节点上，LangGraph负责全局流程编排（将上一个环节输入采购相关表单数据，翻译成自然语言任务–>调用crew完成采购→判断是否转人工→返回结果）；CrewAI负责局部多角色协作（采购员工Agent查库存、财务Agent审核预算、合规Agent确认符合采购规范）；LangGraph通过adapter与crewAI完成通信。
注意：1）crewAI 多角色协作时，其中某个角色也有可能是人类；2）只有在某个自动化节点涉及到多个角色合作时，并且相关角色都已经有了AI智能体后，才要用到crewAI。
3.2.2 上下文持久化与共享（Context Management）
上下文持久化与共享要达成全局统一存储对话历史、工单信息、用户画像、任务状态，转接时自动同步，不丢失信息。
