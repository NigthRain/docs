---
title: Agent 架构综述:从 Prompt 到上下文工程构建 AI Agent - 知乎
author: phodal
source_url: https://zhuanlan.zhihu.com/p/1961712181994299775?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-10-15 08:40
content_type: Article
vote_up_count: 85
comment_count: 2
collected_at: 2026-08-18 10:32:50
index: 256/314
---

# Agent 架构综述:从 Prompt 到上下文工程构建 AI Agent - 知乎

> phodal | 2025-10-15 08:40

来源: https://zhuanlan.zhihu.com/p/1961712181994299775?utm_medium=openapi_platform&utm_source=1a2112

---

・结构分层与模块化：用清晰的层次（角色/通信/工具/安全/任务）组织提示，避免“大一统”文本，便于维护与动态加载。
・工具优先级与并行化：优先专用工具且能并行就并行，显著降低延迟与成本（如并行调用 read_file 读取多文件，编辑用 search_replace 而非 sed）。
・安全边界与权限模型：默认沙箱最小权限，危险操作需显式授权（如 required_permissions: ["network"|"git_write"|"all"]），禁止对 main/master 强推等高风险动作。
・任务管理最小充分：多步骤复杂任务用 TODO 管理（创建后第一个标记为 in_progress，完成即刻 completed），简单直接任务立刻执行。
・上下文唯一性与安全修改：代码编辑要求唯一可定位的上下文（old_string 在文件中唯一，前后各 3–5 行），多处修改分次执行，避免误改。
・交流规范与用户体验：隐藏内部工具名，用自然语言“说-做-总结”，保持简洁可扫读；用 backticks 标注文件/函数名，必要时给最小可用示例
这种从单体提示词向模块化、层次化、动态化演进的设计，正如从单体应用向微服务架构的转变，为 Agent 的高级推理、系统可扩展性与可维护性提供了结构支撑。
从检索到规划：使用 prompt 让 Agent 拆解目标
仅仅告诉 Agent “制定一个计划”是远远不够的，我们必须通过一套明确的原则来指导其分解过程，就像为软件模块制定规约一样。 单体 Agent 的智能上限，往往取决于其“规划能力”——能否将模糊目标拆解为明确的、可执行的子任务。
这涉及两种核心策略：
・预先分解：这种策略也被称为静态规划，它在任务执行开始之前，就将整个复杂任务完整地分解成一个子任务序列或计划。
・交错分解：这种策略也被称为动态规划，它不在任务开始时制定完整计划，而是在执行过程中动态地决定下一个子任务。
例如，BabyAGI 的架构就体现了这种“任务驱动”型规划： 它包含三个核心 Agent —— task_creation_agent（任务生成）、execution_agent（任务执行）和 prioritization_agent（任务优先级排序），形成了一个不断循环的任务更新与执行系统。
