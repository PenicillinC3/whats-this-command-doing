# What’s This Command Doing?

[English](README.md) | [简体中文](README.zh-CN.md)

What’s This Command Doing? is a Codex and Claude Code skill that explains command-line approval requests in the user's language. It covers Bash, Zsh, sh, Fish, PowerShell, Windows Command Prompt, and other terminal environments. It describes the requested action, purpose, approval scope, and material consequences without replacing the host's permission system.

## Install

Copy the `skills/whats-this-command-doing` directory from this repository to one or both locations:

- Codex project skill: `.agents/skills/whats-this-command-doing/`
- Claude Code project skill: `.claude/skills/whats-this-command-doing/`

For user-wide installation, copy the folder to Codex's `~/.agents/skills/whats-this-command-doing/` or Claude Code's `~/.claude/skills/whats-this-command-doing/`. Keep the folder name `whats-this-command-doing` and the included `SKILL.md`. Restart or start a new session if the host does not discover the skill immediately.

## Use

- Let the host discover the skill automatically when relevant.
- Invoke it explicitly with `$whats-this-command-doing` in Codex or `/whats-this-command-doing` in Claude Code where slash skill invocation is supported.
- If a project needs a stronger default, add a short instruction to its `AGENTS.md` or `CLAUDE.md` asking the agent to apply this skill to command approval requests.

## Always Apply

To make the skill apply consistently across projects, add the following instruction to both global instruction files:

- Codex: `~/.codex/AGENTS.md` (`C:\Users\<you>\.codex\AGENTS.md` on Windows)
- Claude Code: `~/.claude/CLAUDE.md` (`C:\Users\<you>\.claude\CLAUDE.md` on Windows)

Create the file if it does not exist, then add:

```markdown
Before requesting approval for any shell or terminal command, always apply the `whats-this-command-doing` skill. In the user's current language, explain the command's action, target, purpose, and material effects in the host's native approval description or justification field. Accurately explain the active shell's semantics and state uncertainties. Never execute the command before approval or approve it on the user's behalf.
```

These global instructions improve consistency, but they do not guarantee that every approval request will include an explanation or change the host's approval UI. For deterministic enforcement, use and validate a host-specific hook or client integration.

## Remove

Delete the installed `whats-this-command-doing` skill directory. If you added a reference in `AGENTS.md` or `CLAUDE.md`, remove that reference too.

## Validation

The behavioral cases in [`evals/cases.md`](evals/cases.md) are writing and review scenarios. They must not execute destructive commands, send data, or run unknown scripts.
