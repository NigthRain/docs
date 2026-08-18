---
title: VSCode + Claude Code + DeepSeek 安装使用指南(初学者版) - 知乎
author: 王御
source_url: https://zhuanlan.zhihu.com/p/2057136882446775607?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-08-01 12:06
content_type: Article
vote_up_count: 88
comment_count: 30
collected_at: 2026-08-18 10:32:48
index: 79/314
---

# VSCode + Claude Code + DeepSeek 安装使用指南(初学者版) - 知乎

> 王御 | 2026-08-01 12:06

来源: https://zhuanlan.zhihu.com/p/2057136882446775607?utm_medium=openapi_platform&utm_source=1a2112

---

5. 开始使用
1.重新打开 VSCode 后，点击左侧活动栏的 Claude Code 图标（Anthropic 的标志）。
2.Claude Code 面板将在侧边或底部打开。
3.在对话输入框中输入你的问题或编程任务，按回车发送。
4.Claude Code 会直接调用 DeepSeek API，为你生成代码、解答问题。
常见问题
Q:vscode看不到claude code的图标
・vscode打开文件夹默认为Restricted模式，需要关闭。方法为点击红框位置，在弹出的窗口选择trust。
Q: 发送消息后没有响应？
・确认 settings.json 中的 ANTHROPIC_AUTH_TOKEN 已替换为正确的 API Key。
・确认 ANTHROPIC_BASE_URL 地址可以正常访问（https://api.deepseek.com/anthropic）。
・尝试完全关闭 VSCode 后重新打开。
Q: API Key 忘记了怎么办？
・登录 DeepSeek 平台 → API Keys 页面 → 删除旧密钥 → 创建新密钥。
Q: 需要切换模型怎么办？
・无需修改配置文件。在对话框中直接输入 /model 命令即可切换：
 ・/model sonnet → 日常使用 flash（便宜快速）
 ・/model opus → 复杂任务切到 pro（强推理）
 ・切换立即生效，仅影响当前会话。
Q: 能在命令行终端中使用吗？
・可以。安装 Claude Code CLI（npm install -g @anthropic-ai/claude-code）后，相同的 settings.json 配置同样对 CLI 生效。
Q: 一直弹出claude.ai订阅登陆界面？
弹 claude.ai 登录界面 = 机器上 Claude Code 完全没读到 API 凭证，settings.json 的 env 块在机器上没被加载
① 文件是不是真的在正确位置、名字对不对（最常见）
・Win+R 输入 %USERPROFILE%\.claude 回车，确认里面有 settings.json
・注意 Windows 隐藏扩展名：很可能实际是 settings.json.txt（右键新建文本文档改名后最常见的坑）
・确认不是放进了项目文件夹的 .claude/、.vscode/settings.json 或 VSCode 用户设置里——只有 %USERPROFILE%\.claude\settings.json 才对所有目录生效
