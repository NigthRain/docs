---
title: DeepSeek R1来了,追平o1!它现在不但比OpenAI开放,也比它有活力 - 知乎
author: 硅星人
source_url: https://zhuanlan.zhihu.com/p/19580288630?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-01-21 09:53
content_type: Article
vote_up_count: 10
comment_count: 0
collected_at: 2026-08-18 10:32:51
index: 311/314
---

# DeepSeek R1来了,追平o1!它现在不但比OpenAI开放,也比它有活力 - 知乎

> 硅星人 | 2025-01-21 09:53

来源: https://zhuanlan.zhihu.com/p/19580288630?utm_medium=openapi_platform&utm_source=1a2112

---

论文里另一个很有意思的地方，是R1 zero训练过程里，出现了涌现时刻，DeepSeek把它们称为“aha moment”。
技术报告里提到，DeepSeek-R1-Zero 在自我进化过程中展现了一个显著特点：随着测试阶段计算能力的提升，复杂行为会自发涌现。例如，模型会进行“反思”，即重新审视并评估之前的步骤，还会探索解决问题的替代方法。这些行为并非通过明确编程实现，而是模型与强化学习环境交互的自然产物，大大增强了其推理能力，使其能够更高效、更精准地解决复杂任务。
“它突显了强化学习的力量和美丽：与其明确地教模型如何解决问题，我们只需为其提供正确的激励，它就会自主地开发先进的问题解决策略。这一“顿悟时刻”有力地提醒了强化学习在解锁人工智能新水平方面的潜力，为未来更自主、更适应的模型铺平了道路。”
蒸馏，蒸馏，欢迎大家一起来蒸馏
在DeepSeek的官方推文里，所有介绍的重点并不在R1模型技巧或R1模型榜单成绩，而是在蒸馏。
“今天，我们正式发布 DeepSeek-R1，并同步开源模型权重。DeepSeek-R1 遵循 MIT License，允许用户通过蒸馏技术借助 R1 训练其他模型。DeepSeek-R1 上线API，对用户开放思维链输出，通过设置 `model='deepseek-reasoner'` 即可调用。DeepSeek 官网与 App 即日起同步更新上线。”
这是它官方发布的头几句话。
DeepSeek在R1基础上，用Qwen和Llama蒸馏了几个不同大小的模型，适配目前市面上对模型尺寸的最主流的几种需求。它没有自己搞，而是用了两个目前生态最强大，能力也最强大的开源模型架构。Qwen 和 Llama 的架构相对简洁，并提供了高效的权重参数管理机制，适合在大模型（如 DeepSeek-R1）上执行高效的推理能力蒸馏。蒸馏过程不需要对模型架构进行复杂修改，减少了开发成本。而且，直接在 Qwen 和 Llama 上进行蒸馏训练比从头训练一个同规模的模型要节省大量的计算资源，同时可以复用已有的高质量参数初始化。
这是DeepSeek打的一手好算盘。
而且，效果同样不错。
“我们在开源 DeepSeek-R1-Zero 和 DeepSeek-R1 两个 660B 模型的同时，通过 DeepSeek-R1 的输出，蒸馏了 6 个小模型开源给社区，其中 32B 和 70B 模型在多项能力上实现了对标 OpenAI o1-mini 的效果。
