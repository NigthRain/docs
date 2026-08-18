---
title: 大模型蒸馏(以tulu3和deepseek-R1为主) - 知乎
author: 沁沁
source_url: https://zhuanlan.zhihu.com/p/22011316630?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-02-07 17:13
content_type: Article
vote_up_count: 27
comment_count: 1
collected_at: 2026-08-18 10:32:51
index: 309/314
---

# 大模型蒸馏(以tulu3和deepseek-R1为主) - 知乎

> 沁沁 | 2025-02-07 17:13

来源: https://zhuanlan.zhihu.com/p/22011316630?utm_medium=openapi_platform&utm_source=1a2112

---

导读
・1.模型蒸馏方法主要分为哪些？
・2.为什么大模型主要用的是数据增强蒸馏？
・3.大模型一般是如何进行数据增强蒸馏的？（以tulu3为例）
・4.完整post-training思路梳理以及数据增强蒸馏参与了哪些阶段？（以deepseek-r1为例）
・5.前沿关于数据蒸馏有哪些方向？
・6.对蒸馏要点进行总结
1. 蒸馏方法种类
note：
・对抗蒸馏：
 ・生成对抗网络（GAN）：生成器（学生）欺骗判别器，使其无法区分教师和学生的输出。
 ・对抗损失：结合蒸馏损失和对抗损失联合优化。
由于现在的top模型如gpt、claude等均是闭源模型，导致无法获取各层的特征与输出概率，无法直接应用基于输出、中间特征、逐层、对抗蒸馏方法。因此，一般是通过调用api获取数据结果的方式来实现数据增强蒸馏。
2. 数据增强蒸馏方法
deepseek-R1技术报告中对于数据分布与数据合成没有深入进行探讨，这里以tulu3为例进行展开描述。
2.1. tulu3
2.1.1. 数据组成
2.1.2. 数据合成
2.1.2.1. Persona IF（通用）
通过角色（来自Persona Hub： huggingface.co/datasets...，包含从网络数据中自动整理的10亿个不同角色的集合）为条件，生成特定技能的prompt，然后用精确指令跟随获取对应的response。具体prompt见图28-29 
constraints 示例
2.1.2.2. 偏好数据
重写instruction（减少constraint生成答案作为原prompt的rejected answer）。具体prompt见图30
2.1.2.3. math 和 code
采用类似的人物驱动方法来综合生成各种数学和编程问题。然后用zero-shot让gpt-4o生成答案，具体prompt见图31-34 
突出生成比较难，仅部分天才可解决（具像化描述）的数学题，在生成答案时要求step-by-step以及答案时正确的
突出生成比较难，中级以上工程师（（具像化描述））才能解决的代码题，在生成答案时约定输出格式和使用的代码类型
给定batch（instrction、output）一起进行评估并打分
2.1.2.4. safety & Non-compliance
来源现有数据集、gpt合成，涵盖incomplete, unsupported, indeterminate, and humanizing requests (in addition to unsafe requests) 
