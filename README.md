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

Automatic discovery and project instructions influence model behavior; neither guarantees that every approval request will include a complete explanation or changes the native approval UI. For deterministic interception or a custom approval surface, build and validate a separate hook or client integration.

## Remove

Delete the installed `whats-this-command-doing` skill directory. If you added a reference in `AGENTS.md` or `CLAUDE.md`, remove that reference too.

## Validation

The behavioral cases in [`evals/cases.md`](evals/cases.md) are writing and review scenarios. They must not execute destructive commands, send data, or run unknown scripts.
