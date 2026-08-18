---
title: Claude Code 命令体系解析:三种类型、七大分类、50+ 命令 - 知乎
author: deephub
source_url: https://zhuanlan.zhihu.com/p/2018440051848136003?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-03-20 21:34
content_type: Article
vote_up_count: 68
comment_count: 0
collected_at: 2026-08-18 10:32:49
index: 193/314
---

# Claude Code 命令体系解析:三种类型、七大分类、50+ 命令 - 知乎

> deephub | 2026-03-20 21:34

来源: https://zhuanlan.zhihu.com/p/2018440051848136003?utm_medium=openapi_platform&utm_source=1a2112

---

Claude Code 内置了超过 50 个命令，但是大多数开发者只用了其中 3 到 5 个，剩下的基本没人翻过。
这篇文章覆盖每一个斜杠命令、每一个 CLI 标志、每一个键盘快捷键，以及开发团队从未正式宣布就悄悄上线的隐藏功能。看完本文后Claude Code命令都不再是盲区。
三种命令类型
进入具体命令之前，有必要区分 Claude Code 的三种命令形态。
CLI 命令在终端启动 Claude Code 时执行：
 claude                    # Start in current directory  
 claude -c                 # Continue most recent session  
 claude --print "question" # One-shot query, then exit
斜杠命令在交互式会话内部输入 / 触发：
 /init      # Initialize CLAUDE.md  
 /compact   # Compress context  
 /model     # Switch models
输入 / 即可查看所有可用命令，边输入边筛选。
键盘快捷键在会话期间直接生效：
 Ctrl+C     # Cancel current generation  
 Ctrl+R     # Search command history  
 Shift+Tab  # Toggle modes (normal → auto-accept → plan)
第一部分：日常核心命令（核心 10 个）
每天都会用到的命令，优先掌握。
1./init — 项目初始化
在项目根目录创建 CLAUDE.md——Claude 每次会话都会读取的持久记忆文件。
 /init
Claude 生成的初始 CLAUDE.md 包含项目描述、技术栈、代码风格偏好和常见模式。
根据开发者工作流反馈，每个项目从 /init 开始可以消除 80% 的重复上下文设置。比如说与其每次会话都解释"用 async/await 别用 promises"，不如一次写进 CLAUDE.md 永久生效。
/init 执行完毕后，立即追加具体规则：
 # CLAUDE.md  
 Authentication  
 - Use JWT tokens, not sessions  

