# 这条命令要干啥？

[English](README.md) | [简体中文](README.zh-CN.md)

“这条命令要干啥？”是一个适用于 Codex 和 Claude Code 的 Skill，用通俗易懂的语言解释命令行批准请求。它覆盖 Bash、Zsh、sh、Fish、PowerShell、Windows 命令提示符（CMD）及其他终端环境，并根据用户当前使用的语言撰写说明。它帮助解释请求要执行什么、为什么执行、批准范围及重要后果，但不会取代宿主软件自身的权限控制。

## 安装

将本仓库中的 `skills/whats-this-command-doing` 文件夹复制到以下一个或两个位置：

- Codex 项目级 Skill：`.agents/skills/whats-this-command-doing/`
- Claude Code 项目级 Skill：`.claude/skills/whats-this-command-doing/`

如需对当前用户的所有项目生效，可复制到 Codex 的 `~/.agents/skills/whats-this-command-doing/` 或 Claude Code 的 `~/.claude/skills/whats-this-command-doing/`。请保留 `whats-this-command-doing` 文件夹名和其中的 `SKILL.md`。如果宿主软件没有立即发现该 Skill，请重新启动软件或开始新的会话。

## 使用

- 在相关任务中由软件自动发现并使用。
- 在 Codex 中用 `$whats-this-command-doing` 显式调用。在 Claude Code 支持斜杠命令的界面中用 `/whats-this-command-doing`。
- 如果只想在一个项目里使用这条规则，把下方整段复制到该项目的 `AGENTS.md`（Codex）或 `CLAUDE.md`（Claude Code）。

## 在所有项目中使用

复制下方整段规则，任选一种方式添加。如果以前加过命令批准规则，请替换旧规则，保留其他指令。

### 桌面版

- **Codex / ChatGPT 桌面版**。打开 **设置 → 个性化 → Codex 指令**，把规则粘贴到输入框。
- **Claude 桌面版**。打开 **Settings → General → Instructions for Claude**，把规则粘贴到输入框。

### 指令文件

把规则加到对应文件中。如果文件不存在，可以创建。

- Codex 读取 `~/.codex/AGENTS.md`（Windows：`C:\Users\<用户名>\.codex\AGENTS.md`）。
- Claude Code 读取 `~/.claude/CLAUDE.md`（Windows：`C:\Users\<用户名>\.claude\CLAUDE.md`）。

### 要复制的规则

```markdown
### 说明每次终端命令批准请求

提交任何可能弹出批准请求的终端命令之前，用用户当前使用的语言写一段说明。假设读者从没用过终端，也从没写过代码。能加载 whats-this-command-doing Skill 时就应用它。即使 Skill 未安装或未加载，也照这条规则写。

先说你想做什么、会动到哪个文件、文件夹、网站或账号，以及这对当前任务有什么帮助。说明可能影响用户决定的后果，例如会删掉、覆盖或发送什么，数据会发到哪里。如果需要额外权限，说清这次批准会允许什么。有影响但无法确认的事要说清楚。用日常用词，遮住命令也要能看懂。只写“允许执行下列命令吗？”或只贴命令都不够。

提交前把说明写进工具提供给用户看的批准说明字段，例如 Codex 的 justification 或 Claude Code 的 description（如果工具提供）。如果工具收到调用后才决定是否弹出批准框，要在调用前填好说明。每次都检查，重试也一样。如果工具没有合适字段，或已知界面会隐藏说明，在软件允许单独发消息时，紧接着在正式批准请求前把说明发给用户。遵守软件的权限规则并等待用户决定，不提前运行或自行批准。
```

保存规则后，开启新会话。如果已经安装过 Skill，也请用新版文件夹替换旧版。你可以让它模拟删除项目中 `dist` 文件夹的批准说明，并明确要求只写说明。遮住命令后，读者也应该能看懂。例如：

> 可以删除项目里的 `dist` 文件夹和里面的所有文件吗？这样可以清理上次生成的文件。删除的文件不会进回收站。我还没检查里面是否有你手动保存的文件。

这条规则约束助手怎么写。如果软件自行显示通用批准提示，批准窗口里实际能看到什么，取决于软件界面。

## 卸载

删除已安装的 `whats-this-command-doing` 文件夹。如果曾把规则加到桌面版设置、`AGENTS.md` 或 `CLAUDE.md`，也请把规则从相应位置删除。

## 验证

[`evals/cases.md`](evals/cases.md) 中的行为案例用于撰写和审阅说明，不应实际执行有破坏性的命令、发送数据或运行未知脚本。
