---
title: Hooks才是Claude Code CLI 的革命性更新 - 知乎
author: misterz
source_url: https://zhuanlan.zhihu.com/p/1961858543805248206?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2025-10-17 13:47
content_type: Article
vote_up_count: 53
comment_count: 2
collected_at: 2026-08-18 10:32:50
index: 255/314
---

# Hooks才是Claude Code CLI 的革命性更新 - 知乎

> misterz | 2025-10-17 13:47

来源: https://zhuanlan.zhihu.com/p/1961858543805248206?utm_medium=openapi_platform&utm_source=1a2112

---

前言
前面对Claude Code CLI有了基本了解，今天继续深度探索Claude Code CLI Hooks的使用方式。对往期内容感兴趣的小伙伴也可以看往期内容：
・Claude Code CLI平台与中转站接入汇总及避坑
・使用Claude Code Router轻松切换各种高性价比模型
・Claude Code CLI MCP配置很难？三种方式轻松掌握
・深入了解Claude Code CLI自定义命令
・深入了解Claude Code CLI子代理Subagent
当前使用版本
1.0.128 (Claude Code)
配置文件
Claude Code CLI钩子配置在 settings.json文件，提供了 用户(全局)配置、项目配置、本地项目配置 3种配置方式：
・用户(全局)配置：作用于当前用户下单所有项目，路径：~/.claude/settings.json
・项目配置：作用于特定项目，路径：.claude/settings.json
・本地项目配置：作用于特定本地项目(git忽略)，路径：.claude/settings.local.json
Hooks格式
钩子由匹配器组织，每个匹配器可以有多个钩子， 格式如下：
{
  "hooks": {
    "EventName": [
      {
        "matcher": "ToolPattern",
        "hooks": [
          {
            "type": "command",
            "command": "your-command-here",
            "timeout": 100
          }
        ]
      }
    ]
  }
}
・matcher：匹配工具名称的模式，区分大小写（仅适用于 PreToolUse 和 PostToolUse）
 ・支持字符串匹配， 例如：Write匹配写入工具，Bash匹配Shell命令
 ・支持正则表达式，例如：Edit|Write 或者 Notebook.*
 ・使用 * 匹配所有工具，也可以不配置或者使用 ""
・hooks：模式匹配时要执行的命令数组
 ・type：目前仅支持command
 ・command：要执行的Shell命令（可以使用 $CLAUDE_PROJECT_DIR 等环境变量）
 ・timeout：（可选）在取消该特定命令之前，命令应运行多长时间（以秒为单位）
