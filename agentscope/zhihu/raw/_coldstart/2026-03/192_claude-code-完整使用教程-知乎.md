---
title: Claude Code 完整使用教程 - 知乎
author: 硅基点火器
source_url: https://zhuanlan.zhihu.com/p/2018862186013946674?utm_medium=openapi_platform&utm_source=1a2112
publish_date: 2026-03-22 01:32
content_type: Article
vote_up_count: 31
comment_count: 5
collected_at: 2026-08-18 10:32:49
index: 192/314
---

# Claude Code 完整使用教程 - 知乎

> 硅基点火器 | 2026-03-22 01:32

来源: https://zhuanlan.zhihu.com/p/2018862186013946674?utm_medium=openapi_platform&utm_source=1a2112

---

扩展思考（Extended Thinking）
・默认启用，Claude 会进行深度推理
・Option+T / Alt+T — 切换开关
・/effort — 调整推理强度（low / medium / high / max）
后台任务
・Ctrl+B — 将当前任务放入后台运行
・Ctrl+T — 查看任务列表
・长时间运行的操作会在后台继续
对话回退（Checkpointing）
・Esc+Esc — 回退到之前的对话状态
・可恢复到任意之前的节点
・不会丢失数据
远程控制
可从 claude.ai 或移动端控制终端会话。
Web 会话
・在 claude.ai/code 上运行
・支持 1M token 上下文
・支持长时间运行任务
CI/CD 集成
支持 GitHub Actions、GitLab CI/CD 等非交互模式。
17. 环境变量参考
变量	说明
CLAUDE_CODE_EFFORT_LEVEL	推理努力等级：low/medium/high/max
CLAUDE_CODE_DISABLE_AUTO_MEMORY	设为 1 禁用自动记忆
CLAUDE_CODE_DISABLE_ADAPTIVE_THINKING	设为 1 禁用自适应思考
MAX_THINKING_TOKENS	最大思考 Token 数
CLAUDE_AUTOCOMPACT_PCT_OVERRIDE	自动压缩阈值百分比
CLAUDE_CODE_DISABLE_BACKGROUND_TASKS	禁用后台任务
CLAUDE_CODE_VOICE_LANGUAGE	语音输入语言（如 zh-CN）
CLAUDE_CODE_ENABLE_PROMPT_SUGGESTION	设为 false 禁用提示建议
CLAUDE_CODE_DEBUG	设为 1 启用调试日志
CLAUDE_DEBUG_HOOKS	设为 1 调试 Hooks
EDITOR	默认编辑器
18. 最佳实践
项目配置
1.创建 CLAUDE.md — 每个项目都应有，记录构建命令、代码规范和项目结构
2.配置权限 — 在 settings.json 中预授权常用命令，减少授权提示
3.设置 Hooks — 配置自动格式化、通知等自动化流程
工作流优化
1.善用 Plan 模式 — 复杂任务先规划再执行
2.使用子代理 — 为重复性任务创建专用代理
3.管理上下文 — 用 /compact 释放空间，用子代理处理冗长操作
4.用 /btw 旁问 — 快速问题不影响主对话
