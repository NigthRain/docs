---
title: GitHub Copilot 入门:老牌 AI 编程助手还值得用吗? - 知乎
author: 阿伟玩不懂
source_url: https://zhuanlan.zhihu.com/p/2061035811240423604?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-07-16 10:35
content_type: Article
vote_up_count: 0
comment_count: 0
collected_at: 2026-08-18 10:32:48
index: 118/314
---

# GitHub Copilot 入门:老牌 AI 编程助手还值得用吗? - 知乎

> 阿伟玩不懂 | 2026-07-16 10:35

来源: https://zhuanlan.zhihu.com/p/2061035811240423604?utm_medium=openapi_platform&utm_source=1a2112

---

写代码时，AI 实时给出灰色建议代码，按 Tab 接受。支持整行、整段函数补全，覆盖 20+ 编程语言。
Copilot 的补全特点是对开源代码学习得最透——毕竟背后是 GitHub 的代码库。写常见框架（React、Vue、Express、Django）的模板代码时，补全质量很高。
2. Copilot Chat
侧边栏聊天面板，可以问代码问题、解释报错、生成代码。支持 @workspace 引用整个项目上下文，@terminal 引用终端报错。
快捷键 Ctrl+I（Mac 用 Cmd+I）可以触发行内聊天——选中一段代码，直接在代码上方输入指令，比如"加 try-catch"“改成 async/await”。
3. PR 自动审查
这是 Copilot 独有的杀手功能。在 GitHub 的 PR 页面，Copilot 会自动 Review 代码，指出潜在 Bug、安全漏洞、代码风格问题。
也可以在 PR 评论里 @github-copilot 让它审查特定代码，或者让它帮忙写 PR 描述。
4. Copilot Workspace（新功能）
更高级的 Agent 模式，能从 GitHub Issue 出发，自动规划任务、写代码、创建 PR。目前还在预览阶段，但方向很明确——从"补全工具"进化为"自主 Agent"。
安装：4 步搞定
1.订阅： 去 GitHub Settings → Copilot 页面开通。$10/月，学生免费（GitHub Student Developer Pack）
2.装插件： VS Code 扩展商店搜 “GitHub Copilot”，点 Install
3.登录： 弹出浏览器授权页面，点 Authorize
4.开始用： 写代码自动补全，Ctrl+I 开 Chat
省钱技巧： 如果你是学生或开源维护者，可以免费使用。在 GitHub Education 页面认证学生身份即可。
Chat 指令速查
新手必记的斜杠命令：
命令	作用
/explain	解释选中的代码
/fix	修复选中的代码错误
/tests	为选中代码生成单元测试
/doc	给函数添加注释文档
/new	描述需求，AI 新建文件
@ 引用让回答更精准：
引用	作用
@workspace	让 AI 理解整个项目
@terminal	把终端报错喂给 AI
@git	引用 Git diff 或历史

