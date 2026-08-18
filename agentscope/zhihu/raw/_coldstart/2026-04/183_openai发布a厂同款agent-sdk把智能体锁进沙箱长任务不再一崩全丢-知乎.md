---
title: OpenAI发布A厂同款Agent SDK:把智能体锁进沙箱,长任务不再一崩全丢 - 知乎
author: 智东西
source_url: https://zhuanlan.zhihu.com/p/2028228941698081388?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-04-16 21:54
content_type: Article
vote_up_count: 0
comment_count: 0
collected_at: 2026-08-18 10:32:49
index: 183/314
---

# OpenAI发布A厂同款Agent SDK:把智能体锁进沙箱,长任务不再一崩全丢 - 知乎

> 智东西 | 2026-04-16 21:54

来源: https://zhuanlan.zhihu.com/p/2028228941698081388?utm_medium=openapi_platform&utm_source=1a2112

---

智东西
编译 | 刘煜
编辑 | 陈骏达
智东西4月16日报道，今天，OpenAI更新其Agents SDK（智能体软件开发工具包），更新内容包括新增原生沙箱执行环境，让智能体在受控的计算机环境中安全运行；升级分布内管控框架，支持智能体在指定工作空间内处理文件并使用经授权的工具；实现管控框架与计算资源的分离，兼顾智能体运行的安全性、稳定性与可扩展性。
Agents SDK的全新功能已通过API向所有客户全面开放，延用OpenAI标准API定价模式，计费依据为token使用量与工具调用次数。全新的管控框架与沙箱功能将率先在Python中上线，后续OpenAI计划推出支持TypeScript的版本。
OpenAI产品团队成员卡兰・夏尔马（Karan Sharma）向TechCrunch透露：“本次更新的核心，是对现有Agents SDK进行优化升级，使其能够兼容各类沙箱服务提供商。”他称，希望通过此次更新，让用户能够借助该管控框架，结合自身已有的技术体系，开发出可处理长周期任务的智能体。
博文链接：
 openai.com/index/the-ne...
一、沙箱功能能给企业在生产环境中安全部署智能体
智能体有时会表现出不可预测性，在完全无监督的状态下运行存在风险。
OpenAI此次新增沙箱功能，旨在通过集成该功能，使智能体可在特定工作空间内独立运行，安全地读写文件、安装运行所需工具包、执行代码与调用工具。仅在执行特定操作时访问文件与代码，同时保障系统整体完整性。
Agents SDK所提供的原生沙箱，可直接为开发者提供上述执行环境能力，无需开发者自行搭建与集成。
使用沙箱功能时，开发者可选用自有沙箱环境，也可直接使用工具包内置支持的第三方沙箱服务，包括Blaxel、Cloudflare、Daytona、E2B、Modal、Runloop以及Vercel。
同时，为实现不同服务商环境间的迁移适配，Agents SDK还引入清单抽象层，用于定义智能体工作空间。开发者可挂载本地文件、设定输出目录，并接入各类存储服务提供商的数据资源，包括AWS S3、谷歌云存储、Azure Blob存储以及Cloudflare R2。
如此一来，Agents SDK便为开发者提供了从本地原型开发到生产部署的统一环境配置方式，同时为模型构建了稳定可预测的工作空间，明确模型的输入读取路径、输出写入路径，以及长周期任务的作业管理方式。
