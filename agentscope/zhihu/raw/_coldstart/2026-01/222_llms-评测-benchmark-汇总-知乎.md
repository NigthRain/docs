---
title: LLMs 评测 benchmark 汇总 - 知乎
author: 蒸馏的猫
source_url: https://zhuanlan.zhihu.com/p/638508365?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-01-11 10:30
content_type: Article
vote_up_count: 70
comment_count: 1
collected_at: 2026-08-18 10:32:50
index: 222/314
---

# LLMs 评测 benchmark 汇总 - 知乎

> 蒸馏的猫 | 2026-01-11 10:30

来源: https://zhuanlan.zhihu.com/p/638508365?utm_medium=openapi_platform&utm_source=1a2112

---

截止到2023.6.20，GPT-3在SuperGLUE上排25名。
3. CLUE 2020
中文版 GLUE。
动机： 中文是个很大的语料库，但目前现存的大模型评测任务数据集都是英文的，所以搞了一个中文的。
评测使用的数据集：这里也分了3个子类，分别是单句任务、相似性任务、阅读理解任务
1.单句任务
・TNEWS：选择题，对今日头条的新闻标题分类；
・IFLYTEK：选择题，根据APP的表述对APP的类型进行分类
・CLUEWSC2020：判断题，按照WSC的方法收集制作的中文代词测试数据，给定一段文章和【代词-名次】对，判断这个代词指代的是不是这个名词。
・AFQMC：判断题，判断两个句子意思是否相似，数据来源于蚂蚁金服。
・CSL：判断题，根据论文摘要判断关键词是否是真实的关键词。
・OCNLI：选择题，中文版MNLI，判断两个句子的关系是【蕴含 | 矛盾 | 中立】
・CMRC2018：包含段落、问题、答案（论文里没说是什么题型），语料来源于中文维基百科。
・ChID：选择题，给定一个段落，中间有些词被遮掉了，模型需要从候选答案中选择正确的词填入，类似于完形填空。
・C3：选择题，给定文本和相关问题，选择答案。
paper： aclanthology.org/2020.c...
github： github.com/CLUEbenchmar...
官网评测： cluebenchmarks.com/
CLUE上，除人类以外，GPT-4排第一，文心一言之类排在后面，它们的中文水平都不如GPT-4，说明GPT-4对中文的理解水平远远高于其他模型。
二、对模型知识理解和记忆能力的评测
1. MMLU
动机：由于目前 LLMs（Large Language Models）已涌现出了强大的理解能力，以往的自然语言处理评测数据集已经没有能力评估新模型的新能力了，于是研究人员又开发出了这个新的评测benchmark。
数据集类型：英文语料，覆盖率各个级别57个学科的知识，选择题题型，对模型来说比较难
paper： arxiv.org/pdf/2009.0330...
github： github.com/hendrycks/te...
同样，GPT-4遥遥领先。
2. C-Eval
中文版MMLU，上海交大 + 清华，2023.5发表。

评测库内容：中文评测库，全是单选题，4选1。包含13948个多项选择题，涵盖52个不同学科，难度从初一、大学、到职业则个考试共4个难度级别，
