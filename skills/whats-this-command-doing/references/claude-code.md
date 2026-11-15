# Claude Code

When Claude Code requests permission to run a command, follow the shared rules in the parent `SKILL.md`. For Bash tool calls, use the tool's `description` field as the short human-readable summary shown in the permission prompt. Apply the same explanation rules to other command tools and shell environments, including the PowerShell tool when enabled; do not force Bash wording onto PowerShell, CMD, Zsh, Fish, or other shells.

- The description should identify the action and target, and call out the most relevant effect or uncertainty.
- Keep the description accurate and concise; the prompt also displays the command itself. Do not assume the description can contain every detail or that every host interface has identical rendering.
- Permission-prompt comments are supplied by the user when answering a prompt and then sent back to Claude; they are not a field for Claude to pre-fill.
- Hooks such as `PermissionRequest` or `PreToolUse` are separate integrations. Do not claim that this Skill makes permission decisions, intercepts every request, or rewrites the UI.
- Never use a hook or command wrapper to silently approve an action as a substitute for explaining it.

For local use, install this skill in `<project>/.claude/skills/whats-this-command-doing/` or `~/.claude/skills/whats-this-command-doing/`. Follow current Claude Code documentation for skill discovery and permission behavior.
