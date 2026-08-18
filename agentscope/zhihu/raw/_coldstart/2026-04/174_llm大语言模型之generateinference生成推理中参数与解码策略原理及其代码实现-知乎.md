---
title: LLM大语言模型之Generate/Inference(生成/推理)中参数与解码策略原理及其代码实现 - 知乎
author: Glan格蓝
source_url: https://zhuanlan.zhihu.com/p/653926703?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-04-26 16:39
content_type: Article
vote_up_count: 663
comment_count: 37
collected_at: 2026-08-18 10:32:49
index: 174/314
---

# LLM大语言模型之Generate/Inference(生成/推理)中参数与解码策略原理及其代码实现 - 知乎

> Glan格蓝 | 2026-04-26 16:39

来源: https://zhuanlan.zhihu.com/p/653926703?utm_medium=openapi_platform&utm_source=1a2112

---

更新：所有代码都放在了github上，更方便实现：
—————————
LLM大语言模型Generate/Inference生成或者说推理时，有很多的参数和解码策略，比如OpenAI在提供GPT系列的模型时，就提供了很多的参数[1]，那这些参数的原理以及代码上怎么实现的呢？本文将尽力进行一一的解释。全文阅读和实现可能需要40分钟，建议收藏~如果觉得对你有帮助，那就点个赞吧 。
原始生成
假如都没有使用这些参数和策略做后处理，模型是怎么生成的呢？以llama模型举例（其他生成式模型是一样）：
from transformers import AutoModelForCausalLM, AutoTokenizer
import torch

model_name = "llama-2-7b-hf" # 用你的模型的地址
model = AutoModelForCausalLM.from_pretrained(model_name, device_map="auto")
tokenizer = AutoTokenizer.from_pretrained(model_name)

text = "say"
inputs = tokenizer(text, return_tensors="pt")
print(f"inputs:{inputs}")

# 结果
inputs:{'input_ids': tensor([[   1, 1827]]), 'attention_mask': tensor([[1, 1]])}
我们输入的模型的就一个词：say（该词分词后就是1个token，在词表中的位置是1827），然后给到模型预测下一个token，如果我们不做任何参数控制，就是直接走模型的forward：
logits = model.forward(input_ids)
print("Logits Shape:", logits.logits.shape)
print(f"logits:{logits.logits}")

# 结果
Logits Shape: torch.Size([1, 2, 32000])
logits:tensor([[[-12.9696,  -7.4491,  -0.4354,  ...,  -6.8250,  -8.0804,  -7.5782],
         [-11.3775, -10.1338,  -2.3563,  ...,  -6.7709,  -6.5252,  -8.9753]]],

