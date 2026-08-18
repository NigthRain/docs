---
title: Orchestrator:把决策权还给人类的技能编排器 - 知乎
author: ldxs
source_url: https://zhuanlan.zhihu.com/p/2058940728017942047?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-07 20:24
content_type: Article
vote_up_count: 0
comment_count: 0
collected_at: 2026-08-18 10:32:47
index: 50/314
---

# Orchestrator:把决策权还给人类的技能编排器 - 知乎

> ldxs | 2026-08-07 20:24

来源: https://zhuanlan.zhihu.com/p/2058940728017942047?utm_medium=openapi_platform&utm_source=1a2112

---

・批处理/JSONL 模式依赖 LLM 可用，不可用时降级为步骤规划，不执行实际脚本。
・文件上传大小限制 50MB，超大文件需手动放入 input/ 目录。
・数据访问工具（db_query / read_table / image_info）仅读取，不修改数据。
・图片元数据读取仅支持常见格式（PNG/JPEG/GIF），其他格式返回基本信息。
・技能编排依赖 ~/.workbuddy/skills 目录存在且包含可执行技能入口脚本。
・llms.txt 和 README 基于 v2.8.1 代码编写，旧版本部分功能可能不适用。
原文：
 不想再跟 LLM 的随机性较劲，所以写了这个编排器——链你定，它只管执行。
一、为什么写这个
用过 ReAct 循环的人都有同感：LLM 一旦开始“自主决策”，你就得花大量精力去审查它在干什么、规避它乱调用工具、修正它跑偏的路径、规范它的输出格式。成本远远超过收益。
与其跟 LLM 的随机性死磕，不如把“决策”这一步暂时拿回人类手里。Orchestrator 就是这么个东西——你事先在画布上排好技能的执行顺序（串行、并行、循环），然后让它按部就班地执行每一步，每一步只调用 LLM 完成当前技能，不做任何路径选择。就这么简单。
它基于我们之前做的 skill-sub 技能（那个用来做黏连检查和里程碑标记的），把 skill-sub 做成了编排器的一个可选功能，你可以在执行前决定是否开启优化。整个系统的核心逻辑就是：链由人编排，LLM 只管执行。
二、系统功能
・链式执行：从已保存的 Pipeline 中选择一条，下达任务后系统自动进入“需求分析 →（可选优化）→ 逐步执行”三段式流程，每轮结果独立展示。
・可视化 Pipeline 编辑器：三栏布局（技能列表 / 编排画布 / 已保存 Pipeline），双击添加技能，支持 seq（串行）、par（并行）、loop（循环）三种模式，双击编辑参数，右键切换模式。
・三种真执行模式：seq = 前一步输出传入下一步，单次 llm.chat()；par = ThreadPoolExecutor 真并行；loop = for 循环真重复。
・skill-sub 可选优化：算法主导的链分析——读 SKILL.md 提取标签，检查步骤间黏连兼容性，插入转换步骤或标记里程碑。LLM 仅在算法无法判定时做一次模糊回退。你可以选择开或关。
・双入口：Web UI（主模式，三 Tab：对话 / 配置 / Pipeline） + CLI 批处理（--batch 和 --jsonl 管道模式）。
・LLM 后端兼容：支持 LM Studio、Ollama 及任意 OpenAI 兼容后端，超时和 max_tokens 通过配置页调节。
・全部配置界面化：LLM 后端、联网搜索、提示词、技能路径均在 Web 配置 Tab 中调整，无需编辑配置文件。
