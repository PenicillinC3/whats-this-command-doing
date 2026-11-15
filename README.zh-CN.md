# 这条命令要干啥？

[English](README.md) | [简体中文](README.zh-CN.md)

“这条命令要干啥？”是一个适用于 Codex 和 Claude Code 的 Skill，用通俗易懂的语言解释命令行批准请求。它覆盖 Bash、Zsh、sh、Fish、PowerShell、Windows 命令提示符（CMD）及其他终端环境，并根据用户当前使用的语言撰写说明。它帮助解释请求要执行什么、为什么执行、批准范围及重要后果，但不会取代宿主软件自身的权限控制。

## 安装

将本仓库中的 `skills/whats-this-command-doing` 文件夹复制到以下一个或两个位置：

- Codex 项目级 Skill：`.agents/skills/whats-this-command-doing/`
- Claude Code 项目级 Skill：`.claude/skills/whats-this-command-doing/`

如需对当前用户的所有项目生效，可复制到 Codex 的 `~/.agents/skills/whats-this-command-doing/` 或 Claude Code 的 `~/.claude/skills/whats-this-command-doing/`。请保留 `whats-this-command-doing` 文件夹名和其中的 `SKILL.md`。如果宿主软件没有立即发现该 Skill，请重新启动软件或开始新的会话。

## 使用

- 在相关任务中由宿主自动发现并使用。
- 在 Codex 中使用 `$whats-this-command-doing` 显式调用；在 Claude Code 支持斜杠命令的界面中使用 `/whats-this-command-doing`。
- 如需项目级的更明确提示，可在项目的 `AGENTS.md` 或 `CLAUDE.md` 中添加一条简短说明，要求代理在命令批准请求中应用此 Skill。

自动发现和项目说明可以影响模型行为，但不能保证每次批准请求都包含完整解释，也不能改变原生批准界面。若需要确定性拦截或自定义批准界面，应另行实现并验证 hook 或客户端集成。

## 卸载

删除已安装的 `whats-this-command-doing` 文件夹。如曾在 `AGENTS.md` 或 `CLAUDE.md` 中添加引用，也请一并删除该引用。

## 验证

[`evals/cases.md`](evals/cases.md) 中的行为案例用于撰写和审阅说明，不应实际执行有破坏性的命令、发送数据或运行未知脚本。
