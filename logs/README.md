# logs/ — AI Coding 日志目录

存放你在开发中与 AI 工具的对话日志，和作品代码一并提交。日志必须由官方采集器从真实会话导出。

> 本目录现在是**示例**，请替换成你自己导出的真实日志（删掉示例的 `your-github-login/` 目录）。

当前仓库不保留组委会模板会话。完成官方采集器安装并导出真实会话后，按下面的目录结构添加日志；不要手写或复制示例 JSONL 充数。

## 目录结构

```text
logs/
└── <github_login>/              # 你的 GitHub 用户名，一人一目录
    ├── manifest.json            # 会话清单
    └── <date>/                  # 日期 YYYY-MM-DD
        └── <tool>__<sid>.jsonl  # 一个会话一个文件（工具名与 session id 用 __ 连接）
```

- `<tool>`：`claude-code` / `opencode` / `codex` / `kiro`
- 每个 `.jsonl` 每行一个事件，由组委会提供的日志归集工具导出，**只提交 JSONL 本身**。

导出与提交的完整步骤、字段定义见[《AI Coding 日志归集与提交手册》](https://github.com/open-vela/docs/blob/dev-ai-contest-2026/zh-cn/contest_2026/ai_coding_log_guide.md)。
