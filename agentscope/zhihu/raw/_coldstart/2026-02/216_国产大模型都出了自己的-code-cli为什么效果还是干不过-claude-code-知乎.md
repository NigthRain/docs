---
title: 国产大模型都出了自己的 Code CLI,为什么效果还是干不过 Claude Code? - 知乎
author: 傅红雪
source_url: https://zhuanlan.zhihu.com/p/2004518128386852038?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-02-10 11:36
content_type: Article
vote_up_count: 433
comment_count: 52
collected_at: 2026-08-18 10:32:50
index: 216/314
---

# 国产大模型都出了自己的 Code CLI,为什么效果还是干不过 Claude Code? - 知乎

> 傅红雪 | 2026-02-10 11:36

来源: https://zhuanlan.zhihu.com/p/2004518128386852038?utm_medium=openapi_platform&utm_source=1a2112

---

但 Anthropic 不一样。Claude Code 是他们的战略级产品。他们用最顶尖的工程师来打磨这个工具，因为他们深知：模型的能力需要通过工具来释放。
原因二：迭代深度不够
Claude Code 从发布到现在，经历了无数次迭代。每一次更新都在优化上下文管理、循环控制、工具调用的细节。
这些优化不是一朝一夕能追上的。就像做汽车——发动机（模型）很重要，但变速箱（编排）、悬挂（上下文管理）、刹车（安全控制）同样决定了驾驶体验。
你不能只做一个发动机，然后随便套一个车壳子就上路。
原因三：缺少真实场景的打磨
Claude Code 的很多优化来自于海量用户的真实使用反馈。哪种编排策略在大型项目中更有效？哪种错误处理方式更合理？这些都需要在实战中摸索。
国产 CLI 工具的用户量和使用深度，目前还远远不够支撑这种级别的优化。
所以，同样的模型 + Claude Code = 更好的效果
这就解释了开头提到的现象。
GLM-4.7 在 GLM-CLI 里效果一般，但在 Claude Code 里表现明显更好。Kimi K2.5 也是同样的情况。
不是模型不行，是工具没有帮模型把能力释放出来。
打个比方：
模型是一个高水平的厨师。GLM-CLI 给了他一个简陋的厨房——灶台不稳、刀具不全、食材乱摆。Claude Code 给了他一个米其林级别的厨房——设备齐全、流程规范、后勤完善。
同一个厨师，出菜的水平能一样吗？
这对普通开发者意味着什么？
意味着你现在就有一个白嫖策略：
用国产模型的价格（甚至免费额度），享受 Claude Code 级别的工具体验。
比如 Kimi K2.5，性能接近 Claude 的水平，API 成本只有 Claude 的几分之一。把它接入 Claude Code CLI，就能获得远超自家 CLI 工具的效果。
这不是多花钱，反而是省钱——用更便宜的模型，配更好的工具，达到更好的效果。
但是，配置起来有点麻烦
Claude Code 的模型切换功能，虽然官方支持，但配置过程对普通开发者并不友好。
你需要：
1.设置环境变量 CLAUDE_CODE_USE_BEDROCK 或 ANTHROPIC_API_KEY
2.配置 model_provider 相关参数
3.修改 settings.json 里的模型映射
4.处理各种兼容性问题
一个配置项搞错，就跑不起来。
AgentTerm：图形化界面，一键切换模型
