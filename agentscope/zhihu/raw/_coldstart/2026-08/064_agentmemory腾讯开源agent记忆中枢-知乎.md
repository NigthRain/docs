---
title: AgentMemory:腾讯开源Agent记忆中枢 - 知乎
author: AI时代逻辑与流
source_url: https://zhuanlan.zhihu.com/p/2068252841991574160?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-05 08:49
content_type: Article
vote_up_count: 1
comment_count: 2
collected_at: 2026-08-18 10:32:47
index: 64/314
---

# AgentMemory:腾讯开源Agent记忆中枢 - 知乎

> AI时代逻辑与流 | 2026-08-05 08:49

来源: https://zhuanlan.zhihu.com/p/2068252841991574160?utm_medium=openapi_platform&utm_source=1a2112

---

4. CodeGraph（代码图谱）。索引代码符号、文件、调用关系和影响路径。改代码前能做影响分析——不只告诉你「代码在这里」，还告诉你「改这个可能影响哪些地方」。
基准测试：成功率涨了，Token 还省了
跟 OpenClaw 集成后的实测数据很能说明问题。PersonaMem（长程记忆）从 48% 拉到 76%，提升 59%；WideSearch 成功率从 33% 到 50%，涨了一半；SWE-bench 从 58.4% 到 64.2%。更关键的是 Token 消耗——WideSearch 省了 61%，SWE-bench 省 33%，AA-LCR 省 31%。
记忆不是「塞更多上下文」，反而是「用更少 Token 做更好决策」。分层架构让 Agent 先拿高层画像做方向判断，再按需下钻拿事实，不会把上下文窗口撑爆。
它跟标准 RAG 有什么不一样
RAG 检索的是文本 Chunk，没有所有权、版本、状态的概念。Agent Memory 把对话、技能、文档、代码统一注册为「记忆资产」，每个资产有 Owner、可见性（Private/Team/Restricted/Agent）、版本号。团队管理员可以审核后把个人技能分享给全团队，再绑定到其他 Agent 上当装备用。
检索策略也不是纯向量：BM25 + 向量 + RRF 混合检索，支持中英文分词（jieba / 英文），结果受条目数、字符预算和超时三重限制，防止记忆撑爆上下文。
方案	记忆类型	团队共享	权限治理	Token 优化	代表项目
Agent   Memory	4   类资产 + L0-L3 分层	原生支持	Private/Team/ACL	最高省 61%	TencentDB-Agent-Memory
标准 RAG	文本 Chunk 检索	需自建	无	无优化	LangChain   RAG
Chat   History	原始对话记录	不支持	无	反而更费	框架内置
Mem0	对话记忆	有限	基础	有优化	mem0ai/mem0
安装：三种方式，推荐一键部署
一键部署适合想完整体验的团队，启动后自动打印可直接粘贴到 Claude 的命令。
OpenClaw 用户装个插件就行，默认 SQLite 后端零配置。
Hermes 用户走 Docker，默认接腾讯云 DeepSeek-V3.2，换个 API Key 就能用 GPT-4o。
