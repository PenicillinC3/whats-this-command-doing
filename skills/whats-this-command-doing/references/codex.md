# Codex

When Codex requests approval for a command, follow the shared rules in the parent `SKILL.md` and put the user-facing explanation in the approval request's `justification` field when that field is available.

- Write the justification as a short, specific question that names the action, target, and reason and states any consequence the user needs to decide. For example, “May I create an empty file named `notes.txt` in `E:\ZS10190`? That folder is outside the project Codex can normally edit.” Use this example only for a command that creates a new file without overwriting one.
- Explain what additional access the request enables only when the approval details or tool context establish it.
- Do not send a separate pre-approval message if the host's approval workflow instructs the model to use the `justification` field without an ordinary message.
- Do not infer approval from a prior approval or alter the approval policy.
- The field improves the explanation; a Skill cannot force itself to load for every approval or control how every Codex client renders the field.

For local use, install this skill in `<project>/.agents/skills/whats-this-command-doing/` or `~/.agents/skills/whats-this-command-doing/`. Follow the current Codex documentation for discovery and restart requirements.
