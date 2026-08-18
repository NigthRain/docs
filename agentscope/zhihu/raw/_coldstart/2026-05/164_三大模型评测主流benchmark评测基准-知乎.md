---
title: 三、大模型评测:主流Benchmark评测基准 - 知乎
author: Alongsin
source_url: https://zhuanlan.zhihu.com/p/2036385326927721733?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-05-11 10:56
content_type: Article
vote_up_count: 2
comment_count: 0
collected_at: 2026-08-18 10:32:49
index: 164/314
---

# 三、大模型评测:主流Benchmark评测基准 - 知乎

> Alongsin | 2026-05-11 10:56

来源: https://zhuanlan.zhihu.com/p/2036385326927721733?utm_medium=openapi_platform&utm_source=1a2112

---

七、安全对齐类Benchmark
Benchmark	简介
HarmBench	320+ 有害行为类别，标准化越狱攻击测试集，2024年发布
TruthfulQA	817道"诱导模型说谎"的题目，测幻觉率
BBQ	偏见与刻板印象测试，覆盖9个社会维度
WildGuard	真实用户提交的边界案例，动态更新
八、多模态类Benchmark
Benchmark	内容	说明
MMMU	30学科，多模态高校考试题	2024年成为图文评测核心指标
MMBench	感知+认知双维度图像评测	上海AI实验室，2023
MathVista	数学视觉推理题	图形题是当前多模态难点
Video-MME	视频理解，1分钟至1小时	时序推理能力评测
Video-MME-v2	三层难度体系（2026-04，南京大学）	新增跨视频推理
九、Benchmark的核心问题：污染、刷榜与信任危机
9.1数据污染（Data Contamination）
问题根源：公开Benchmark一旦发布，题目就可能被爬取进入下一代模型的训练数据，导致"背题"而非"解题"。
已有研究证实的案例： 多项研究（含arXiv 2311.09783等）发现主流模型训练数据与测试集存在重叠
・Scale AI 2024年"GSM1K实验"：构造同风格新题后开源模型准确率大幅下降 -微软专门推出MMLU-CF（Contamination-Free）版本应对这一问题
检测方法（长期有效）：
・Perplexity比较法：污染数据的困惑度通常异常低
・Min-K% Prob：用最低概率词元检测记忆程度
・构造同风格新题（GSM1K式）：对比新旧得分差异
9.2排行榜刷分与公信力问题
Cohere 2025年4月论文《The Leaderboard Illusion》 提到（arXiv 2504.20879）OpenAI和Google在Chatbot Arena总测试数据中分别占约 19.2% 和 20.4%，而83个开源模型合计仅占约29.7% 。这表明大厂可在正式发布前大量私下测试：2025年1-3月，Meta在Chatbot Arena上提交了27个私有模型变体进行测试。这种资源不对等使得排行榜在一定程度上成为大厂营销工具而非纯粹技术评估。
大厂拥有更多测试资源和版本筛选机会，开源社区测试资源则严重不对等——这是任何依赖厂商自愿提交的公开榜单的内在缺陷，不仅限于Chatbot Arena。
