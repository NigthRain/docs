---
title: 告别工具焦虑!GitHub Copilot Harness工作流实测:一个工具搞定开发全流程 - 知乎
author: 程序员2026
source_url: https://zhuanlan.zhihu.com/p/2066090694335370378?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-07-30 09:20
content_type: Article
vote_up_count: 1
comment_count: 0
collected_at: 2026-08-18 10:32:48
index: 89/314
---

# 告别工具焦虑!GitHub Copilot Harness工作流实测:一个工具搞定开发全流程 - 知乎

> 程序员2026 | 2026-07-30 09:20

来源: https://zhuanlan.zhihu.com/p/2066090694335370378?utm_medium=openapi_platform&utm_source=1a2112

---

7月27日，GitHub官方博客发布了一套全新工作流，核心观点：别再追新AI工具了，掌握Harness就够。
每天早上打开电脑，你是不是也有这种焦虑？
昨天Cursor出了新功能，今天Windscale又融资了，明天Claude Code好像又升级了……工具越来越多，每个都说自己能改变开发方式，但你连每个工具的快捷键都没记全。
7月27日，GitHub工程师Burke Holland在官方博客发了一篇文章，标题很直接：《The harness is all you need (mostly)》。
翻译过来就是：别折腾了，掌握Harness就够了。
什么是Harness？一句话说清楚
Harness不是新工具，是GitHub Copilot的核心工作流。
你可以把它理解成"AI驾驶的驾驶舱"——不管你在VS Code、CLI还是新的Copilot App里用，底层都是同一套Harness。学会一次，到处通用。
"我每天都很AI打交道，但我发现less is way more。真正让我效率提升的，不是我装了啥工具、配了啥MCP、用了啥花哨prompt，而是我怎么用Harness。"
说白了：不是你用的工具不够多，是你没把现有工具用明白。
Harness工作流6步骤：从原型到上线
我专门去试了一下这套工作流，确实有点东西。
第一步：选一个工具，别贪多
GitHub Copilot家族现在有CLI、VS Code插件、Visual Studio、JetBrains插件，还有新出的独立App。
Burke建议新手从CLI开始——纯文本界面，没那么多UI要学，输入prompt，agent干活，简单直接。
第二步：开启YOLO模式
YOLO模式就是"Allow All"，让agent自己执行命令，不用每次都问你"可以吗？"。
但有个前提：必须在沙箱环境跑。比如GitHub Codespaces，或者开发容器。别在你本地机器上开YOLO，出了事哭都来不及。
第三步：先做原型，别急着写代码
这一步我觉得是最有价值的。
以前我们接到需求，第一反应是打开编辑器开始写。现在呢？先让AI给你出20个方案。
