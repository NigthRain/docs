---
title: Vibe Coding:一个综述 - 知乎
author: xnliu
source_url: https://zhuanlan.zhihu.com/p/1992006025319035038?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-01-06 22:59
content_type: Article
vote_up_count: 160
comment_count: 5
collected_at: 2026-08-18 10:32:50
index: 225/314
---

# Vibe Coding:一个综述 - 知乎

> xnliu | 2026-01-06 22:59

来源: https://zhuanlan.zhihu.com/p/1992006025319035038?utm_medium=openapi_platform&utm_source=1a2112

---

本节内容主要来自《A Survey of Vibe Coding with Large Language Models》。
该论文是首个对“Vibe Coding”这一新兴软件开发范式进行全面系统的综述性研究。随着大型语言模型（LLM）从代码辅助工具进化为自主编码代理（Coding Agent），开发者们的工作模式正经历一场根本性变革——不再逐行审查代码，而是通过观察程序运行结果来验证AI生成的功能实现，这种模式被作者称为“Vibe Coding”。
这篇论文的核心目标，就是为Vibe Coding这一新兴但略显混乱的领域“立法”，将其从一种非正式的、依赖直觉的“艺术”，转变为一门有理论、有框架、有模型的严谨“工程学科”。它试图回答： 我们该如何系统、高效且安全地管理和利用自主编码代理来构建软件？
论文的核心贡献在于，成功地将“Vibe Coding”这一略带调侃的俚语，升华为一门严谨的、可分析、可管理的工程学科。通过形式化定义、理论建模、生态系统梳理和开发模型提炼，论文不仅为学术研究开辟了一片新的沃土，也为工业界如何系统、安全、高效地拥抱AI编程新时代提供了宝贵的“导航图”和“方法论手册”。它标志着我们对AI时代软件工程的理解，从最初的惊叹和零散的尝试，迈向了系统化、科学化管理的新阶段。
一、概览

Vibe Coding： 是一种以大型语言模型为基础的软件开发工程方法论，其核心是人类开发者、软件项目和编码代理三者之间动态的、三方协作的关系。
• 人类层	• cinstr：系统指令与任务需求。
• 项目层	• ccode：代码库（源代码、API接口、架构设计），• cdata：数据库（持久化数据、数据模式），• cknow：领域知识（文档、规范、最佳实践）。
• 智能体层	• ctool：可调用工具的定义与签名（编译器、测试框架、版本控制），• cmem：历史交互记忆（多轮对话上下文、既往决策记录），• ctasks：当前任务（待执行动作、任务队列、执行状态）。
二、形式化定义
本论文为 Vibe Coding 构建一个严谨的形式化定义,这个定义的核心是将 Vibe Coding 建模为一个由人类开发者、编码智能体和软件项目三者交互的闭环系统。
论文中采用 约束马尔可夫决策过程（Constrained Markov Decision Process, CMDP） 作为其理论基础，因为它能很好地刻画在满足特定约束（如代码规范、功能正确性）下寻求最优解（如开发效率）的过程。
