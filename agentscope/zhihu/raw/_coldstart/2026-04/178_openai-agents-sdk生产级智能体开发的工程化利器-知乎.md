---
title: OpenAI Agents SDK:生产级智能体开发的工程化利器 - 知乎
author: 奇舞团
source_url: https://zhuanlan.zhihu.com/p/2030367778314638232?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-04-22 19:30
content_type: Article
vote_up_count: 0
comment_count: 0
collected_at: 2026-08-18 10:32:49
index: 178/314
---

# OpenAI Agents SDK:生产级智能体开发的工程化利器 - 知乎

> 奇舞团 | 2026-04-22 19:30

来源: https://zhuanlan.zhihu.com/p/2030367778314638232?utm_medium=openapi_platform&utm_source=1a2112

---


fromagentsimportRunner

fromagents.sandboximportManifest, SandboxAgent, SandboxRunConfig

fromagents.sandbox.entriesimportLocalDir

fromagents.sandbox.sandboxesimportUnixLocalSandboxClient



asyncdefmain():

# 1. 创建受控工作区

withtempfile.TemporaryDirectory() astmp:

dataroom = Path(tmp) / "dataroom"

dataroom.mkdir()

# 写入业务数据

(dataroom / "metrics.md").write_text(...)



# 2. 定义沙箱智能体

agent = SandboxAgent(

name="Dataroom Analyst",

model="gpt-4o", # 使用 GPT-4o 模型

instructions="仅使用data/文件作答，标注文件名",

default_manifest=Manifest(entries={"data": LocalDir(src=dataroom)}),

)



# 3. 运行任务

result = awaitRunner.run(

agent,

"对比2025与2024财年营收、营业利润、现金流",

run_config=RunConfig(

sandbox=SandboxRunConfig(client=UnixLocalSandboxClient()),

),

)

print(result.final_output)




亮点：隔离沙箱执行，无权限溢出、无数据泄露、环境可复现。
五、工程收益对比
| 维度 | 传统开发 | Agents SDK |
|------|---------|-----------|
| 开发效率 | 手写循环、重试、鉴权、状态管理 | SDK 内置，开箱即用 |
| 安全能力 | 自行实现隔离，风险高 | 原生沙箱 + 权限隔离 |
| 模型效能 | 框架适配损耗 | 模型原生对齐 |
| 环境迁移 | 本地→生产配置混乱 | Manifest 跨云兼容 |
