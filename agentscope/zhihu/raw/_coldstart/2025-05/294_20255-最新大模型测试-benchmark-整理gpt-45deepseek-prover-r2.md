---
title: 2025.5 最新大模型测试 benchmark 整理(GPT 4.5/DeepSeek Prover R2 等) - 知乎
author: 王几行XING
source_url: https://zhuanlan.zhihu.com/p/1902395399324545137?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-05-04 17:03
content_type: Article
vote_up_count: 98
comment_count: 4
collected_at: 2026-08-18 10:32:51
index: 294/314
---

# 2025.5 最新大模型测试 benchmark 整理(GPT 4.5/DeepSeek Prover R2 等) - 知乎

> 王几行XING | 2025-05-04 17:03

来源: https://zhuanlan.zhihu.com/p/1902395399324545137?utm_medium=openapi_platform&utm_source=1a2112

---

多模态与跨语言类
1.MMMU (Massive Multimodal Multitask Understanding)
・用途：测试模型对图文混合输入（如图片+问题）的理解与回答能力
・特点：强调视觉+语言联合推理
编程与软件开发类
 1. SWE-Bench Verified
・用途：衡量模型在修复真实代码问题（bug fix）方面的准确率。
 ・特点：需要模型具备代码阅读、理解和修改能力。
 2. SWE-Lancer Diamond
・用途：评估模型在解决真实世界代码任务（含复杂项目）中的实际表现。
・单位：得分以“$金额”表示，模拟“自由职业者”完成项目的绩效。
 创意与人类评估类（间接指标）
1.Human preference scores（人类偏好评估）
・用途：衡量 GPT‑4.5 在日常问题、专业问题和创意写作中的表现是否被人类偏好。
・说明：不属于标准学术 benchmark，但常用于产品性能评估。
DeepSeek Prover R2 （2025.4.30）
Benchmark 名称	作用（评估内容）
MiniF2F	主流评测集之一，测试 Lean 3 中模型的定理证明能力
ProofNet	测试模型在 Lean 4 中处理自然语言定理和形式化语言间转换的能力
MathProofBench	基于 GPT-4 构建的大规模形式化数学 benchmark，用于评估多步骤推理
LeanDojo	用于构建 Lean 形式化环境，支持与 Lean 交互，可用于数据生成与强化学习等任务
Baldur	面向欧几里得几何定理的基准集，专注几何推理
MetaMath	包含海量形式化证明（元数学框架），常用于数学证明训练
HolStep	提供 HOL Light 定理与证明对，评估定理选择和步骤推荐能力
TPTP	自动定理证明社区常用的 benchmark，侧重一阶逻辑问题
PISA benchmark	关注于交互式定理证明（ITP）的基准
Lean-Gym	形式化交互环境，用于模拟 Lean 用户操作场景，用于训练强化学习模型
DeepSeek R1
DeepSeek V3
DeepSeek-V3-0324 
Gemini 2.5 （2025.3.25）
Claude 3.7 （2025.2.24）
附：ChatGPT 的总结
