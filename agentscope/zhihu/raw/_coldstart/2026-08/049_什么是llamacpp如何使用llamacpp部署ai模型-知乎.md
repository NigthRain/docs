---
title: 什么是Llama.cpp?如何使用llama.cpp部署AI模型? - 知乎
author: 黑虾
source_url: https://zhuanlan.zhihu.com/p/2069068006727086229?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-07 22:33
content_type: Article
vote_up_count: 3
comment_count: 5
collected_at: 2026-08-18 10:32:47
index: 49/314
---

# 什么是Llama.cpp?如何使用llama.cpp部署AI模型? - 知乎

> 黑虾 | 2026-08-07 22:33

来源: https://zhuanlan.zhihu.com/p/2069068006727086229?utm_medium=openapi_platform&utm_source=1a2112

---

第三步：让Llama.cpp启动运行模型
只有这一步，才需要命令行，不过也相对简单。就是1、打开系统自带的命令行工具Power Shell，2、用命令进入到Llama.cpp文件夹，然后再用命令启动模型。
1、先打开Windows PowerShell
2、进入Llama.cpp文件夹，在PowerShell中，输入命令，按键盘Enter键。
，这个命令的含义是，让电脑进入到Llama.cpp文件夹。
这里说一下，我的电脑名称是45469，每个人的电脑名不一样，所以这里，每个人的命令也不一样。总之就是cd后面加Llama.cpp文件夹所在位置。
如何查看你电脑Llama.cpp文件位置路径？
点击文件夹最上面，就能显示文件具体路径位置。
3、在PowerShell中继续输入，模型启动命令，按键盘Enter键。
命令具体内容是：
命令执行后的效果：
出现这样的内容，就成功了，然后在浏览器中打开地址：
就可以看到网页聊天界面了。
命令行中的字母参数都是啥意思？主要就 3 个
.\llama-server.exe -m models\Qwen3.5-2B-Uncensored-HauhauCS-Aggressive-Q4_K_M.gguf -ngl 35 -c 4096
参数	作用	建议
-m	指定本地GGUF模型路径	路径有空格时加英文双引号
-ngl	卸载到GPU的层数	有独显先用-ngl 99测试
-c	上下文长度	日常从4096或8192开始
命令整体的意思是：启动llama服务器程序（.\llama-server.exe），运行具体模型（-m models\Qwen3.5-2B-Uncensored-HauhauCS-Aggressive-Q4_K_M.gguf），卸载35层到显卡GPU（-ngl 35），上下文长度是4096（-c 4096）
最常见的几个坑
第一，文件格式不对。 下载前先看清是不是GGUF。必须是.gguf后缀的模型才行。
第二，模型能下载，不等于电脑能跑。 硬盘只负责存模型；真正运行看内存和显存。模型文件 8GB，不代表 8GB 内存就稳，系统、上下文和运行时本身都要占空间。
第三，显卡没加速。 确认下载的是CUDA/ Vulkan等对应后端的版本，再看是否加了 -ngl 99。很多人装完直接运行 CPU 版，然后发现显卡没干活。
最后
Llama.cpp算是本地部署的进阶工具，参数设置的自由度高了很多，且因为是C语音写的，对硬件性能的使用更加极致，缺点就是需要用命令行，不过并不是真的写代码，就是简单启动命令，也不算难，另外现在有了AI，不懂就问AI，或者让智能体（Agent）直接操作。
