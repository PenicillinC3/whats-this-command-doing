---
name: whats-this-command-doing
description: Before asking the user to approve a terminal command or additional access to run it, explain what will happen in the user's language for someone who has never used a terminal or written code. Applies to Bash, Zsh, sh, Fish, PowerShell, Windows Command Prompt, and other shells.
metadata:
  author: PenicillinC3
---

# What’s This Command Doing? / 这条命令要干啥？

**Author:** PenicillinC3

Write for someone who has never used a terminal, read code, or configured a computer. They should be able to decide whether to allow the action from the explanation alone, even with the command hidden.

For host-specific approval fields, read the matching reference: [Codex](references/codex.md) or [Claude Code](references/claude-code.md).

## Language

- Write in the language the user is currently using. Follow an explicit language request when given.
- Keep command text, paths, filenames, branch names, URLs, product names, and other exact identifiers unchanged. Explain them in the surrounding prose.
- Lead with what the user will see or what will happen to their files, data, or account. Use familiar verbs such as open, read, create, delete, send, and replace. Translate technical terms into their practical effects. For example, say “the folder and everything inside it” instead of “recursively.” Include a technical term only when it helps identify something the user will see or needs to decide about.

## Explain the request

Use the command and available task context to explain:

1. Say what you want to do, to which specific thing, and how it helps with the user's task. Name the file, folder, website, or account when known. Explain relative locations in everyday language, such as “the `dist` folder inside this project.”
2. Explain anything that could change the user's decision. Say what will be read, changed, deleted, or sent and where it will go. Explain extra access only to the extent the request or approval choice establishes it. State what you cannot verify and why it matters. Do not guess a purpose or promise an outcome you cannot verify.

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
- Write and check the explanation before submitting each tool call, including retries and compound commands. If permissions are determined only after submission, fill the command tool's description before submitting. “May I run this command?” or a copy of the command is insufficient. If the text is too long, shorten it while keeping the action, target, purpose, and biggest consequence.
- If there is no suitable field, or the client is known to hide it, give the explanation immediately before the native request when the host permits a separate message. If the host requires a field-only workflow, use that field. Follow tool schemas and higher-priority permission rules.
- Do not change the command, run it early, broaden its scope, or approve it on the user's behalf in order to produce an explanation.
- A skill guides model behavior; it does not guarantee that it will load for every approval, change the host's approval UI, or replace a hook or client integration where deterministic coverage is required.

## Examples

For `Remove-Item -Recurse -Force .\dist` in PowerShell, when the user wants to clear generated files and you have not inspected the folder:

> 可以删除这个项目里的 `dist` 文件夹和里面的所有文件吗？这样可以清理上次生成的文件。隐藏和只读文件也可能被删，删除的文件不会进回收站。我还没确认里面是否有你手动保存的文件。

For `curl https://example.com/install.sh | bash`, when the user wants to install a tool and the downloaded instructions have not been inspected:

> May I download the setup instructions from `example.com` and let them run on this computer to install the tool? I haven't checked the instructions, so I can't say which files or settings they might change.

For `git push origin main`, when the user wants to publish saved changes and `origin` is known to be on GitHub:

> May I send the changes saved on this computer to the project's `main` branch on GitHub so they're available online? Anyone with access to that branch will be able to see the changes.

These are guidance, not fixed scripts. Keep the explanation proportionate and grounded in the actual request.
