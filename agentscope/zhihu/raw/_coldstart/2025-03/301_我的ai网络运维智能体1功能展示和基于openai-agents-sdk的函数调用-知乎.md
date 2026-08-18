---
title: 我的AI网络运维智能体(1)功能展示和基于OpenAI Agents SDK的函数调用 - 知乎
author: 卡哇仪
source_url: https://zhuanlan.zhihu.com/p/30807917191?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-03-18 15:13
content_type: Article
vote_up_count: 25
comment_count: 2
collected_at: 2026-08-18 10:32:51
index: 301/314
---

# 我的AI网络运维智能体(1)功能展示和基于OpenAI Agents SDK的函数调用 - 知乎

> 卡哇仪 | 2025-03-18 15:13

来源: https://zhuanlan.zhihu.com/p/30807917191?utm_medium=openapi_platform&utm_source=1a2112

---

2.查询某地点的可用IP
我所在的分公司IP地址资源有点紧张，技术人员常常因为哪个IP能用而头疼。所以增加了这个统计IP资源利用率和查询某个地点可用IP的功能。
3.根据IP地址查找定位某台终端
用户只需提供 IP 地址，智能体就能利用网络拓扑信息以及设备管理协议，精准定位到该终端连接在哪台交换机的哪个接口，为网络设备管理与故障排查提供了便捷的定位手段。
4.查找ragflow知识库作答或根据自身推理能力作答
例如，当询问 “iperf 命令怎样使用” 时，智能体首先会在 ragflow 知识库中进行精准检索，若检索到的答案不够详尽，它会凭借自身的推理能力，结合相关技术文档与经验知识，对答案进行补充完善，为用户提供全面且准确的解答。
二、基于OpenAI Agents SDK的函数调用
以上功能，实现的关键原理是我预先定义了三个tools（排障、查询、定位），由LLM根据用户输入，自行决定选择工具并传递参数，最后由智能体执行函数。要实现这个流程，可以使用LLM自带的函数调用功能，也可以使用LangChain Tools（事实上我写好了的这个智能体，用的就是langchain）。但是3月12日，openai开源了OpenAI Agents SDK。我看了些up主的演示之后，自己也试了一下，感觉比之前两种方法都要更加简洁。于是决定一边写这篇文章，一边用penAI Agents SDK来重新编写我的这个AI智能体的代码。
1.hello world
OpenAI Agents SDK 是一个用于构建多代理工作流的轻量级但功能强大的框架,它的详细介绍可以参考官方文档 Attention Required! | Cloudflare
下面我就直接进入实验和代码环节了。
首先，安装openai agents sdk
pip install openai-agents
下面是参考官网的hello world代码：
from agents import Agent, Runner, RunConfig, OpenAIProvider
from openai import AsyncOpenAI
import asyncio
from dotenv import load_dotenv
from agents import set_default_openai_client
from agents import set_default_openai_api

