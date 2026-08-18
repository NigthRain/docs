---
title: 模型量化三、below 8bit量化 - 知乎
author: Xavier.Hsu
source_url: https://zhuanlan.zhihu.com/p/1979951339946647659?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-12-09 16:27
content_type: Article
vote_up_count: 12
comment_count: 2
collected_at: 2026-08-18 10:32:50
index: 234/314
---

# 模型量化三、below 8bit量化 - 知乎

> Xavier.Hsu | 2025-12-09 16:27

来源: https://zhuanlan.zhihu.com/p/1979951339946647659?utm_medium=openapi_platform&utm_source=1a2112

---

4. 蒸馏辅助量化 Distillation‑Assisted Quantization
模型蒸馏（Knowledge Distillation）：用一个大而准的 teacher 模型（一般是 full‑precision）指导一个小而快的 student 模型 的训练。
训练 student 时，loss 不止包含 cross_entropy(y, y_true)，还包含与 teacher 输出的差异：
   L = \alpha H\bigl(y, \sigma(z_s)\bigr)     + \beta H\bigl(\sigma(z_s, T), \sigma(z_t, T)\bigr)    
各符号含义：
・zs：student 模型输出的 logits（未经过 softmax 的得分向量）
・zt：teacher 模型输出的 logits
・σ(⋅)：softmax 函数，把 logits 变成概率分布
 ・σ(zs) 就是普通 softmax（温度 T=1）
 ・σ(zs,T) 表示带温度 TT 的 softmax
・y：one‑hot 的真实标签（ground‑truth）
・H(⋅,⋅)：交叉熵（cross‑entropy）损失
・α,β：权重系数，用来平衡学生自身与真实标签的损失和蒸馏损失
・T：温度系数（temperature）。T>1 会让 softmax 输出更“平滑”。
配套的 softmax with temperature 为： 
 p_i = \frac{\exp(z_i / T)}{\sum_j \exp(z_j / T)} \tag{11} 
 基于以上定义的覆盖量化损失的公式，我们可以利用：
1.teacher：原始 full‑precision 模型
2.student：量化模型（比如 INT4、二值等）
3.训练 student 时加入蒸馏 loss，让 student 学 teacher 的“软标签”，从而减轻量化带来的损失。
5. 极端低bit量化 (Extreme Quantization)
“Extreme Quantization” 指的是比 INT8 更低比特的量化，典型是：
・1-bit：二值化（Binarization）
・2-bit：三值化 / 低比特量化（Ternarization / 2‑bit）
