---
title: Claude Code 源码深度解析:运行机制与 Memory 模块详解 - 知乎
author: 青稞AI
source_url: https://zhuanlan.zhihu.com/p/2024236369631879273?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-04-05 21:28
content_type: Article
vote_up_count: 28
comment_count: 4
collected_at: 2026-08-18 10:32:49
index: 187/314
---

# Claude Code 源码深度解析:运行机制与 Memory 模块详解 - 知乎

> 青稞AI | 2026-04-05 21:28

来源: https://zhuanlan.zhihu.com/p/2024236369631879273?utm_medium=openapi_platform&utm_source=1a2112

---

10.5 Hooks 与设置
文件	职责	重要度
src/utils/hooks/hooksConfigManager.ts	Hook 事件定义与分组	★★★★
src/utils/hooks/hooksSettings.ts	Hook 来源收集与优先级	★★★
src/utils/settings/settings.ts	设置加载管线	★★★
src/utils/claudemd.ts	CLAUDE.md 加载与 @include 处理	★★★★
src/schemas/hooks.ts	Hook Schema 定义	★★★
附录 A：Feature Flags（功能开关）
Claude Code 大量使用 GrowthBook 进行功能开关控制：
Flag 名称	控制内容
tengu_session_memory	Session Memory 功能总开关
tengu_sm_config	Session Memory 阈值配置
tengu_sm_compact_config	Session Memory Compaction 参数（minTokens, maxTokens 等）
tengu_passport_quail	Auto Memory 提取功能总开关
tengu_bramble_lintel	提取节流（每 N 轮执行一次，默认1）
tengu_moth_copse	跳过 MEMORY.md 索引更新
tengu_coral_fern	"搜索过去上下文" 功能
tengu_cobalt_raccoon	仅反应式压缩模式（Reactive-only）
tengu_onyx_plover	AutoDream 开关 + 阈值（minHours, minSessions）
tengu_herring_clock	Team Memory 功能开关（GrowthBook）
tengu_slate_heron	Time-based Microcompact 配置（gapThresholdMinutes, keepRecent）
EXTRACT_MEMORIES	编译时开关（tree-shake）
HISTORY_SNIP	Snip Compact 编译时开关（ANT-only）
CACHED_MICROCOMPACT	Cached Microcompact 编译时开关
CONTEXT_COLLAPSE	Context Collapse 编译时开关（ANT-only）

