---
name: whats-this-command-doing
description: Explain command-line execution approval requests in the user's language. Use for shell commands in Bash, Zsh, sh, Fish, PowerShell, Windows Command Prompt, and other terminal environments, especially when a user is asked to approve execution or expanded permissions.
metadata:
  author: PenicillinC3
---

# What’s This Command Doing? / 这条命令要干啥？

**Author:** PenicillinC3

When a command-line action needs user approval, make the approval explanation understandable to someone who may not know the shell or its syntax. Explain the actual command request, its purpose in the current task, the authorization being requested, and material consequences.

For host-specific approval fields, read the matching reference: [Codex](references/codex.md) or [Claude Code](references/claude-code.md).

## Language

- Write in the language the user is currently using. Follow an explicit language request when given.
- Keep command text, paths, filenames, branch names, URLs, product names, and other exact identifiers unchanged. Explain them in the surrounding prose.
- Use plain, direct wording. Define shell terms only when they help the user decide.

## Explain the request

Use the command and available task context to explain:

1. What will happen, including the important target: files, folders, processes, services, hosts, accounts, or data.
2. Why it is being requested for this task, without inventing a reason that the context does not support.
3. What approval grants: this command, broader access, or future matching commands, but only as the host's actual approval control specifies.
4. Material consequences relevant to the decision, such as changing or deleting files, sending data, installing software, running downloaded code, changing system settings, affecting a remote service, or incurring a known cost.

Scale the explanation to the risk and complexity. A routine, narrowly scoped read can be brief. A destructive, privileged, networked, compound, or otherwise consequential command needs enough detail to identify its targets and likely effects. Do not mechanically add headings or repeat generic warnings.

## Accuracy and uncertainty

- Explain the command's actual semantics in its detected shell and operating system. Do not assume Bash syntax, Unix paths, or Unix command behavior for PowerShell or CMD, or assume Windows behavior on macOS/Linux.
- For chained, piped, redirected, substituted, or compound commands, describe the meaningful stages and how data or success flows between them.
- Treat invoked scripts, aliases, functions, package lifecycle hooks, downloaded programs, and remote endpoints as unknown unless their behavior is available in context or has been inspected.
- State uncertainty precisely. Do not claim a command is harmless, reversible, local-only, or limited to a particular target without evidence.
- Do not conflate similar commands or side effects. For example, `git reset --hard` affects tracked working-tree changes; do not claim it also removes all untracked files.
- If a command includes credentials or secrets, do not repeat their values in the explanation. Describe their role and where they are sent only when supported by context.
- Do not imply that declining approval will cause the command to run. Do not imply that approval is temporary or persistent beyond what the host's UI says.

## Use the host's approval surface

- Put the explanation in the approval request's intended description, reason, or justification field when the host provides one.
- Respect tool schemas, host instructions, and higher-priority permission policies. Never invent fields or add a message that conflicts with host instructions.
- Do not change the command, run it early, broaden its scope, or approve it on the user's behalf in order to produce an explanation.
- A skill guides model behavior; it does not guarantee that it will load for every approval, change the host's approval UI, or replace a hook or client integration where deterministic coverage is required.

## Concision examples

For a command such as `Remove-Item -Recurse -Force .\dist` in PowerShell, explain that it recursively deletes the `dist` folder under the current directory, that `-Force` can include hidden/read-only items where permitted, and that deleted files may not be recoverable from the Recycle Bin. Mention the task reason only if known.

For `curl https://example.com/install.sh | bash`, explain that it downloads a remote script and immediately runs it with Bash; unless the script has been inspected, its exact changes are unknown.

For `git push origin main`, explain that it sends local commits to the remote `origin` and updates `main`; mention CI, deployment, or collaborators only if repository context supports those effects.

These are guidance, not fixed scripts. Keep the explanation proportionate and grounded in the actual request.
