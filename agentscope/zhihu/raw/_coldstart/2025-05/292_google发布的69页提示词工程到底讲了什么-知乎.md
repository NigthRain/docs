---
title: Google发布的69页提示词工程到底讲了什么 - 知乎
author: Laowangzi244
source_url: https://zhuanlan.zhihu.com/p/1903975110794248237?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-05-09 00:56
content_type: Article
vote_up_count: 36
comment_count: 3
collected_at: 2026-08-18 10:32:51
index: 292/314
---

# Google发布的69页提示词工程到底讲了什么 - 知乎

> Laowangzi244 | 2025-05-09 00:56

来源: https://zhuanlan.zhihu.com/p/1903975110794248237?utm_medium=openapi_platform&utm_source=1a2112

---

我从事科技写作已有三年，但说实话，没有什么比摆弄AI更让我着迷的了。这些语言模型——你可以理解为"超级智能聊天机器人"——能生成故事、代码甚至数学答案。
但关键在于：你得学会正确提问。
这就是提示工程（Prompt Engineering）的意义所在。
它不是什么高深的黑科技，其实就是掌握与AI对话的技巧，避免它胡言乱语。
本文主要参考了李·布恩斯特拉（Lee Boonstra）的《提示工程白皮书》，我会用简单例子拆解其中精髓，让你也能轻松上手。
什么是提示工程
想象一下，你让狗狗去捡球。如果只说“去拿过来”，它可能叼回一只袜子；但如果你指着球说“把那个红色的捡回来”，那就稳了。
提示工程就是这个道理——给AI清晰的指令，避免它输出一堆废话。
谷歌的白皮书指出，这些模型（比如AI）会根据已学的内容预测下一个词。好的提示就像轻轻推它一把，让它猜得更准。重点不在于用多高级的词汇，而在于直截了当地说清楚。下面我们看看具体怎么操作。
为什么这很重要
有一次，我问AI关于“bears”的信息，本想了解野生动物，结果它给我整了一段芝加哥熊队（橄榄球队）的简介……大无语。
而一个好的提示能避免这种乌龙，无论是写诗还是列购物清单。
你完全不需要懂技术。这份白皮书的核心就是：人人都能学会。就像和朋友发消息时，把话说明白对方才能懂你。以下是几个实用技巧：
让AI秒懂你的花式提问法
这份白皮书里技巧多到爆炸，但我只挑了几种不烧脑的——每种都像给AI递小纸条的不同姿势。
1. Zero-Shot方法（直接问）
最省力提问法——直接给AI下指令，不加修饰。适合快速解决问题。
比如判断影评是好评还是差评，你可以这样问：
Hey AI, is this movie review POSITIVE, NEUTRAL, or NEGATIVE?
Review: "Loved every minute of it!"
Answer:
优点：快准狠。
但白皮书特别提醒——遇到"精彩但无聊"这类矛盾型影评时，这种直球提问可能会翻车。
2. Few-Shot方法（实例法）
这就是所谓的“照这个模板来”——给AI几个示例，它就能模仿出相同风格。当我需要规整的内容（比如数据整理）时，这招特别管用。
举个例子：让披萨订单以JSON格式输出得整整齐齐。
Turn this pizza order into JSON.
Example 1: "Small pizza with pepperoni"

