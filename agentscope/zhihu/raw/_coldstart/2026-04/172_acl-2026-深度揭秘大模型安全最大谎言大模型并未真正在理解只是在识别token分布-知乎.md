---
title: ACL 2026 | 深度揭秘大模型安全最大谎言:大模型并未真正在理解,只是在识别token分布? - 知乎
author: 应用机器学习
source_url: https://zhuanlan.zhihu.com/p/2033259317416161370?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-04-30 19:04
content_type: Article
vote_up_count: 5
comment_count: 0
collected_at: 2026-08-18 10:32:49
index: 172/314
---

# ACL 2026 | 深度揭秘大模型安全最大谎言:大模型并未真正在理解,只是在识别token分布? - 知乎

> 应用机器学习 | 2026-04-30 19:04

来源: https://zhuanlan.zhihu.com/p/2033259317416161370?utm_medium=openapi_platform&utm_source=1a2112

---

今天为大家分享来自香港城市大学、中国科学技术大学、阿姆斯特丹大学等机构的最新工作 LogiBreak，这篇论文被 ACL 2026 Findings 接收。该工作关注当前大模型安全对齐中的一个核心漏洞：现有安全机制往往依赖对有害请求表层 token 分布的识别，而并未真正建立起稳定的语义级安全理解。也就是说，当一个有害请求以模型熟悉的自然语言形式出现时，模型通常能够拒绝；但当其被转换为语义等价、形式陌生的逻辑表达式时，安全机制可能失效。为此，作者提出了一种基于自然语言到一阶逻辑转换的黑盒越狱方法 LogiBreak，通过将有害请求改写为形式逻辑表达，在保持语义不变的同时改变 token 分布，从而系统性揭示了当前安全对齐中“token ≠ 语义”的关键问题。 
论文链接：  https://http://arxiv.org/pdf/2505.13527https://http://arxiv.org/pdf/2505.13527 
代码链接：  https://http://github.com/Applied-Machine-Learning-Lab/ACL2026_Logibreakhttps://http://github.com/Applied-Machine-Learning-Lab/ACL2026_Logibreak
📌 核心问题
当前大模型已经通过对齐训练具备一定的安全能力，能够对明显的有害请求进行拒绝。然而，大量实践表明，这种安全机制在面对输入改写时往往并不稳健。
已有工作通常将这一现象归因于 prompt engineering 或攻击技巧，但这篇论文给出了一个更为本质的解释：
 大模型的安全对齐主要作用在 token 分布层面，而非真正的语义理解层面。
这意味着，模型并不是在判断“请求的含义是否有害”，而是在判断“请求是否符合已知的有害表达模式”。
🧠 核心洞察：token ≠ 语义
论文指出，对齐训练数据覆盖的是一类有限的表达形式（token 序列），而不是所有语义等价的表达方式。当输入的 token 分布发生变化，即使语义完全一致，也可能脱离模型的安全对齐范围。
因此，安全机制的失效并非偶然，而是源于一个结构性问题：
语义保持不变，但 token 分布发生偏移时，模型的安全判断可能失效。
这一点也解释了为什么多语言、编码或特殊符号等方法能够绕过安全机制——它们本质上都在改变输入的分布形式。
