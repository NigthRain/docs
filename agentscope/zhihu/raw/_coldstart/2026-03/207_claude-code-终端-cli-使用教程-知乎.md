---
title: Claude Code 终端 (CLI) 使用教程 - 知乎
author: 崔庆才丨静觅
source_url: https://zhuanlan.zhihu.com/p/2011381968739267310?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-03-01 10:08
content_type: Article
vote_up_count: 26
comment_count: 1
collected_at: 2026-08-18 10:32:49
index: 207/314
---

# Claude Code 终端 (CLI) 使用教程 - 知乎

> 崔庆才丨静觅 | 2026-03-01 10:08

来源: https://zhuanlan.zhihu.com/p/2011381968739267310?utm_medium=openapi_platform&utm_source=1a2112

---

你会看到 Claude Code 的欢迎界面，直接输入自然语言即可开始交互。
常用命令
命令	说明	示例
claude	启动交互模式	claude
claude "任务"	执行一次性任务	claude "修复构建错误"
claude -p "查询"	执行查询后退出	claude -p "解释这个函数"
claude -c	继续当前目录最近的对话	claude -c
claude -r	恢复之前的对话	claude -r
claude commit	创建 Git 提交	claude commit
交互模式命令
在交互模式中，可以使用以下内置命令：
命令	功能
/help	显示帮助信息
/clear	清除对话历史
/config	打开设置面板
/model	切换模型
/mcp	管理 MCP 服务
/compact	压缩上下文
/memory	管理记忆
/login	切换账号
exit 或 Ctrl+C	退出
对话交互示例
高级用法
管道和脚本化
Claude Code 遵循 Unix 哲学，支持管道和脚本化操作：
环境变量参考
以下是 Claude Code 支持的常用环境变量：
变量	说明
ANTHROPIC_AUTH_TOKEN	自定义 Authorization 头的值（自动添加 Bearer 前缀）
ANTHROPIC_API_KEY	API 密钥（作为 X-Api-Key 头发送）
ANTHROPIC_BASE_URL	API 基础 URL
ANTHROPIC_MODEL	覆盖默认模型
ANTHROPIC_SMALL_FAST_MODEL	Haiku 级别模型（后台任务用）
MAX_THINKING_TOKENS	设置思考 Token 预算（设为 0 禁用思考模式）
DISABLE_COST_WARNINGS	设为 1 禁用费用提醒
CLAUDE.md 项目记忆
在项目根目录创建 CLAUDE.md 文件，可以为 Claude Code 提供项目特定的指令和上下文。Claude 会在启动时自动加载这个文件。
常见问题
连接失败怎么办？
1.检查 ~/.claude/config.json 文件是否正确创建，内容为 {"primaryApiKey": "self"}
2.确认环境变量已正确设置：  echo $ANTHROPIC_AUTH_TOKEN echo $ANTHROPIC_BASE_URL
3.确认 API 令牌有效（可在 控制台 查看）
4.尝试重新启动终端
