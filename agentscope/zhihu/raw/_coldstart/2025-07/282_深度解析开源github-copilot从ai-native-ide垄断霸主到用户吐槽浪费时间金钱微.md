---
title: 深度解析开源Github copilot:从AI native IDE垄断霸主到用户吐槽浪费时间金钱,微软做错了什么? - 知乎
author: 小橘子
source_url: https://zhuanlan.zhihu.com/p/1923317104905544488?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-07-01 09:57
content_type: Article
vote_up_count: 4
comment_count: 0
collected_at: 2026-08-18 10:32:51
index: 282/314
---

# 深度解析开源Github copilot:从AI native IDE垄断霸主到用户吐槽浪费时间金钱,微软做错了什么? - 知乎

> 小橘子 | 2025-07-01 09:57

来源: https://zhuanlan.zhihu.com/p/1923317104905544488?utm_medium=openapi_platform&utm_source=1a2112

---

github copilot 终于开源了
第一代AI用户，应该知道ChatGPT的强大，知道Github copilot的传奇，2023年到2024年，AI辅助代码生成只有一款绝对霸主地位的AI产品应用:github copilot。
第一款世界级的代码补全产品，第一款业务AI native IDE应用。
Github copilot的商业模式，在2024年看上去完美无瑕，令人神往：
最好的模型支持：微软深度投资OpenAI,模型使用OpenAI gpt3.5全世界最好的模型:
庞大的用户基础： 截至 2024 年初，GitHub Copilot 拥有超过 130 万付费用户和 5 万企业客户，并且这个数字还在持续增长。使用vscode的用户，只有一款AI编程工具。
企业级采纳： 超过 60% 的财富 500 强公司在 2024 年初采用了 GitHub Copilot，渗透能力毋庸置疑。
集成优势： 作为 GitHub 和 Microsoft 生态系统的一部分，Copilot 与 VS Code、Visual Studio 等主流 IDE 的深度集成，提供了无缝的用户体验。
早期市场领导者： 在 AI 编程助手领域，Copilot 凭借其率先推出的功能和 OpenAI 模型最强大的ChatGPT支持，迅速成为市场领导者。

您好，我是阿里巴巴AI专家，专注于LLM大模型&Agent 能力开发，10年互联网经验，今天开始免费给大家分享
【vibe coding解决100个问题】AI编程完全手册2025版，欢迎参与从0到1的提升之路。
Github copilot 开源特性

微软把 GitHub Copilot 给开源了！准确的说是 在VSCode 中的 Chat 部分。 这个类似于 cursor 的 chat 面板，通过聊天的方式来编辑代码，它还可以根据代码提交者 、 变量和斜线命令等提供的信息，给出与您的代码库相关的回答。
功能	描述	代码仓位置
聊天界面	支持斜杠命令的对话式人工智能	src/extension/conversation/
inline chat	可在编辑器中直接进行 AI 辅助编辑（按 Ctrl+I 触发）	src/extension/inlineChat/
inline edit	具备高级流式编辑功能	src/extension/inlineEdits/

