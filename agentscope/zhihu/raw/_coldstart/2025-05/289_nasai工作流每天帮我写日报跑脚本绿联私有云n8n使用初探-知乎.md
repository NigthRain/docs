---
title: NAS+AI工作流,每天帮我写日报、跑脚本!绿联私有云N8N使用初探 - 知乎
author: 可爱的小Cherry
source_url: https://zhuanlan.zhihu.com/p/1904331901998708420?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-05-15 10:09
content_type: Article
vote_up_count: 7
comment_count: 0
collected_at: 2026-08-18 10:32:51
index: 289/314
---

# NAS+AI工作流,每天帮我写日报、跑脚本!绿联私有云N8N使用初探 - 知乎

> 可爱的小Cherry | 2025-05-15 10:09

来源: https://zhuanlan.zhihu.com/p/1904331901998708420?utm_medium=openapi_platform&utm_source=1a2112

---

前言
关于 NAS + AI 的玩法，我之前已经分享过好几篇，尤其是针对绿联NAS，其自带的AI Plugins应用充分调用了 GPU的加速，满足dxp 4800 plus以上设备 14b小模型的日常使用。
但是 AI ，说到底还只是一个工具而已，如何运用 AI 发挥出更大的工作成效，帮助我们增加工作、生活的便利，才是最重要的。
这段时间，我一直在研究 AI 工作流这个新玩具，从dify、openwebui，到扣子空间，最终以本地部署n8n作为了我的最终工作流工具，并且实现了日报、周报的自动生成！
所以这篇文章，我就把我关于在绿联NAS上部署 AI 工作流，以及日报、周报生成的模型做一个分享！
AI 工作流，顾名思义，就是将 AI 运作到一个固定模式的工作流程中。它其实是一种低代码拼搭 + 自动化的结合工具，为不懂代码，但是有想法的用户提供了很多自动化的实现路径。
n8n是一款很火的原生 AI 工作流自动化平台，在github上拥有87k star。它将可视化构建与自定义代码、自托管或云、400+ 集成相结合，支持目前很火的mcp服务。
一、部署n8n
 n8n的部署很简单，下列是项目的yaml文件，其中我们只需要根据自己的想法，修改ports左侧的地址就行了。
在environment环境变量中，我增加了2个Proxy的变量，主要是为了解决容器内链接各式各样国外服务。
services:
  n8n:
    container_name: n8n
    ports:
      # 根据自己的要求修改左侧端口
      - 35678:5678
    volumes:
      # 必须使用docker volume，否则有权限问题
      - n8n_data:/home/node/.n8n
    environment:
      # 该变量解决http访问，否则需要代理https地址
      - N8N_SECURE_COOKIE=false
      - GENERIC_TIMEZONE=Asia/Shanghai
      # 下面两个是你自己的代理地址
      - HTTP_PROXY=http://192.168.0.1:7890
      - HTTPS_PROXY=http://192.168.0.1:7890
    image: docker.n8n.io/n8nio/n8n

