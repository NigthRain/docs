---
title: LEEHPC 集群中部署 Open-WebUI + Ollama 大模型推理服务的完整记录 - 知乎
author: LEEHPC一粒海
source_url: https://zhuanlan.zhihu.com/p/2070604161243164968?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-11 20:15
content_type: Article
vote_up_count: 0
comment_count: 0
collected_at: 2026-08-18 10:32:47
index: 22/314
---

# LEEHPC 集群中部署 Open-WebUI + Ollama 大模型推理服务的完整记录 - 知乎

> LEEHPC一粒海 | 2026-08-11 20:15

来源: https://zhuanlan.zhihu.com/p/2070604161243164968?utm_medium=openapi_platform&utm_source=1a2112

---

报错现象	原因分析	解决方案
bind() to 0.0.0.0:80 failed (98: Address already in use)	管理节点已有服务占用 80 端口，Nginx 默认配置尝试监听 80	ss -lntp \| grep ':80' 查占用，禁用或修改默认 80 监听后重启 Nginx
Open-WebUI 启动后立即退出，日志显示 HuggingFace 下载失败	没有开启离线模式，启动时尝试连接 HuggingFace Hub 拉模型文件	确保设置了 HF_DATASETS_OFFLINE=1、TRANSFORMERS_OFFLINE=1、HF_HUB_OFFLINE=1
用户访问 mgmt01:8088 无响应	可能是 Nginx 没跑、防火墙没开、或 Open-WebUI 服务挂了	分别在 mgmt01 和 gpu02 检查监听端口和防火墙，在管理节点 curl 测试到 gpu02 的连通性
Open-WebUI 连接不上 Ollama	OLLAMA_BASE_URL 配置错误或 Ollama 没监听正确地址	检查 Ollama 是否绑定 0.0.0.0:11434，确认 OLLAMA_BASE_URL 地址正确
多个用户同时推理时显存溢出	OLLAMA_NUM_PARALLEL 设太大，单张卡同时加载模型太多	建议默认设为 2，显存充裕再尝试调到 4
FAQ
Q：Ollama 默认把模型下载到系统盘，怎么改到数据盘上？
A：在 Ollama 的 systemd 服务文件里加一行 Environment="OLLAMA_MODELS=/LLM/models"，然后 systemctl daemon-reload && systemctl restart ollama。模型目录需要提前创建好，Ollama 不会自己建。配完之后 ollama list 能看到路径变化。
Q：Nginx 反代时为什么要关 buffering？
A：因为大模型的输出是逐 token 流式返回的，如果 Nginx 开了缓冲，会把数据攒到一定量才发给客户端，用户看到的就是页面卡住、然后突然刷出一大段，体验很差。proxy_buffering off 之后每个 token 都能实时推到浏览器。这个在长回答场景下区别特别明显。
Q：Open-WebUI 启动就退出，日志里全是 HuggingFace 相关的下载报错，怎么解决？
