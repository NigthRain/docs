---
title: 规划模块:Agent的大脑 — 决定"做什么"和"以什么顺序做" - 知乎
author: 修远客
source_url: https://zhuanlan.zhihu.com/p/2072599495087544197?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-17 08:26
content_type: Article
vote_up_count: 1
comment_count: 0
collected_at: 2026-08-18 10:32:47
index: 3/314
---

# 规划模块:Agent的大脑 — 决定"做什么"和"以什么顺序做" - 知乎

> 修远客 | 2026-08-17 08:26

来源: https://zhuanlan.zhihu.com/p/2072599495087544197?utm_medium=openapi_platform&utm_source=1a2112

---

先说结论
感知让 Agent 看见世界，记忆让 Agent 记住过去，规划让 Agent 决定下一步做什么。
没有规划的 Agent，就像没有大脑的机器人 — 感知到信息也不知道怎么用，记住了偏好也不知道什么时候该用。
在 self-media-agent 项目里，规划体现在三个层面：
规划层面	决定什么	对应代码	当前状态
选题规划	写什么主题	topic/generator.py	LLM 生成，但与热点脱节
流水线编排	以什么顺序执行	pipeline/runner.py	固定 7 步，静态
风格进化策略	用什么风格写	persona/style_learner.py	被动触发，用户修改后才学习
当前项目是静态规划 — 步骤固定、顺序固定、策略固定。 这够用但不够聪明。真正的 Agent 应该能动态规划：根据热点自动选题、根据质检分数决定是否重写、根据发布数据主动调整风格。
一句话：规划是 Agent 智能的核心体现，当前项目迈出了第一步（静态规划），离动态规划还有距离。
一、选题规划：从赛道到选题
当前实现：LLM 根据赛道生成选题
topic/generator.py 的 TopicGenerator — 给 LLM 赛道信息，让它生成结构化选题：
选题规划的输入输出：
选题池管理：规划结果的存储
生成的选题不直接用，先存入选题池（topic/pool.py），按状态管理：
选题状态流转：
选题池的作用：规划结果不一次性消费完，可以攒一批选题，按需取用。避免每次生成都要调 LLM。
踩坑：选题与热点脱节
项目在 api/schemas.py 里定义了 use_hotspot 参数：
但这个参数在选题生成的实现里并没有被使用。 热点抓取（hotspot/）和选题生成（topic/generator.py）是两个独立模块，没有自动串联。
当前流程（手动）：
理想流程（自动）：
差距就是规划模块的进化方向 — 从"人规划"到"Agent 规划"。
二、流水线编排：固定顺序的执行规划
第4篇详细讲过 pipeline/runner.py 的 7 步流水线。从规划的角度看，流水线就是一种静态规划 — 步骤和顺序在代码里写死：
静态规划的特点
特点	当前项目	动态规划的未来
步骤顺序	固定写死在代码里	根据内容类型动态调整
步骤数量	固定 7 步	某些步骤可跳过或重复
分支决策	只有 short_video vs text 一个分支	根据质检分数决定是否重写
错误处理	失败跳过，不重试	失败后根据原因决定重试策略
