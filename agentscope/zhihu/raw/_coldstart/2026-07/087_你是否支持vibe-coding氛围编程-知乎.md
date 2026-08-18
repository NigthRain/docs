---
title: 你是否支持Vibe Coding(氛围编程)? - 知乎
author: JavaGuide
source_url: https://www.zhihu.com/question/1898399718406617016/answer/2066477484997079880?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-07-31 10:57
content_type: Answer
vote_up_count: 3
comment_count: 0
collected_at: 2026-08-18 10:32:48
index: 87/314
---

# 你是否支持Vibe Coding(氛围编程)? - 知乎

> JavaGuide | 2026-07-31 10:57

来源: https://www.zhihu.com/question/1898399718406617016/answer/2066477484997079880?utm_medium=openapi_platform&utm_source=1a2112

---

一个 Agent 一个目录、一个分支、一个任务。这样它们即使乱改，也只会乱在自己的工作区里。
开工前先把范围写窄
你需要让 AI 做什么，尽量说得具体一些，不要让它自己猜。
以订单场景为例，你说一句：帮我实现导出订单功能。
这句话太宽泛了，AI 不知道每次导出几条，导出什么格式，导出哪些字段，字段顺序是怎样的。
信息没给够，它就会自己猜。猜出来的结果能跑，但未必是你想要的。
不如在开工前花几分钟写轻量 Spec，通常比后面返工便宜得多：
## 目标

实现订单导出接口，支持按时间范围导出 CSV。

## 约束

- 单次最多导出 5000 条
- 时间范围不能超过 31 天
- 只能导出当前租户的数据
- 查询必须走 order_tenant_time_idx
- 导出失败要记录失败原因，不能只返回 unknown error

## 验收

- 正常导出 CSV，字段顺序为 order_no、amount、status、created_at
- 超过 5000 条返回明确错误
- 越权租户数据不能被导出
- 单元测试覆盖无数据、越权、超过条数、超过时间范围 4 种情况
这份东西不用写得像方案评审文档。
小任务写清楚目标、约束和验收就够了；中等任务再补接口格式、错误码、表结构；大一点的需求，再拆成 requirements.md、design.md、tasks.md。没必要一上来就把流程拉满，不然你会先被文档劝退。
关于 Spec Coding 的详细介绍，可以参考： Spec Coding 规范驱动编程实战：从 Vibe Coding 到 AI 代码规范。
还有一招，比抽象规范更管用：给 AI 看项目里写得好的代码。
先阅读 UserController、UserService、UserRepository 和对应测试。参考它们的分层方式、异常处理、返回体包装、日志风格和测试写法。然后实现 OrderExportController。

不要引入新的响应格式。
不要新增全局异常处理器。
不要绕过现有权限校验逻辑。
“代码要优雅、可维护、符合最佳实践”这种话，放在 Prompt 里看着很认真，实际约束力很弱。
模型更擅长模仿具体样板。你让它看一段项目里真正合格的代码，它反而更容易写出同一套风格。
把项目坑点写进规则文件
长期项目可以把这些规则放到 AI 工具能稳定读取的位置。比如：
・Claude Code：CLAUDE.md
・Codex：AGENTS.md
・Cursor：Project Rules、.cursor/rules/*.mdc，也可以配合 AGENTS.md
・GitHub Copilot / VS Code：仓库级 .github/copilot-instructions.md、路径级 .github/instructions/*.instructions.md，也支持 AGENTS.md
