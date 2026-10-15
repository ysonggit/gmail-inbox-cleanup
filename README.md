# Gmail Inbox Cleanup

A mail-cleanup skill for Gmail, with Outlook support when the host provides equivalent capabilities. It first checks the selected account, asks about your preferences, scans metadata, and presents a numbered report. Mail changes require approval of specific items in the current conversation.

## Install

Download or clone this repository. Copy its contents into a folder named `gmail-inbox-cleanup` in the skill directory used by your agent:

- Codex: `~/.codex/skills/gmail-inbox-cleanup/`
- Claude Code: `~/.claude/skills/gmail-inbox-cleanup/`

The skill contains instructions and templates. Your agent must separately provide a mail integration or browser access; installing the skill does not connect an account or start a scan. Provider-specific support varies and has not been verified for every host or Outlook integration.

## Connect Gmail and run for the first time

1. Connect your Gmail account using your agent's supported mail connection flow. Keep credentials in that connection flow, never in the skill or a chat message.
2. Invoke `$gmail-inbox-cleanup`, or say: "Use gmail-inbox-cleanup to assess my inbox. Do not change any mail."
3. If no `config.yaml` exists, the agent asks for your account, retention period, archive/Trash preference (default archive), unsubscribe preference, and categories to keep. It saves these settings locally. You can also copy and edit `config.example.yaml` yourself.
4. The agent checks account access and performs a read-only assessment using metadata. If access or metadata is unavailable, it explains what must be connected or which part cannot be assessed.
5. Review the report shown in the conversation and saved in `reports/YYYY-MM-DD.md`. Each item shows its query, counts, senders, sample subjects, and suggested action. Private message IDs freeze its scope.
6. Approve exact numbered items, for example `approve 1,3`. Broad statements such as "approve all" are not accepted. Without numbered approval, no mail changes are authorized.

Reports are conversation responses and local files; this skill does not implement a separate popup window.

## Browser assistance and unsubscribe

If the mail integration lacks an operation, an agent with Computer Use / browser access may use the mail provider's web interface under the same account, scope, and approval rules. Browser assistance does not bypass metadata-only assessment or permit clicking links in email bodies.

Unsubscribe has three modes, set in `config.yaml`: `off`, `list` (default; the report lists senders for you to unsubscribe by hand, for example from Gmail's **Manage subscriptions** page), and `provider`. In `provider` mode, after you approve specific senders, the agent uses the mail provider's own unsubscribe control, so the provider makes the safety checks. The agent never opens unsubscribe links itself. For senders that only offer email-based unsubscribe, the provider may send an unsubscribe email for you; the report says so before you approve. External preference pages, forms, and ambiguous outcomes are listed for manual handling. See [the unsubscribe guide](references/unsubscribe.md).

## Large mailboxes

Assessment reads paginated search results instead of opening messages one by one, and scans up to 5,000 results per query (a later run picks up the rest). Execution uses the fastest operation your mail integration supports: bulk by ID list, then per thread, then per message. It works in chunks of 500 with a progress line per chunk, so you can stop between chunks. Speed still depends on your integration; one that only supports single-message changes will be slow on thousands of messages.

The skill never permanently deletes mail, empties Trash, sends/replies/forwards mail, or creates suggested filters. Archive and Trash actions can be recovered using the cleanup label and provider recovery window. Moving mail to Trash does not itself prove storage was freed.

## Privacy and sharing

Share only `SKILL.md`, `README.md`, `LICENSE`, `config.example.yaml`, `.gitignore`, and the `references/` documents. Your account configuration, reports, message IDs, and unsubscribe URLs are private. Reports may expose senders and subjects even though bodies are not read. Financial identifiers and authentication codes should be masked in examples.

The included `.gitignore` excludes private configuration, reports, and common credential/backup files. It cannot remove information already committed to Git history. Do not upload your installed skill folder wholesale; prepare a separate public copy containing only the files listed above. Never attach real reports or private configuration to issues or screenshots.

These are instructions for an AI agent, not a permission sandbox. Safety also depends on the agent following them and on the permissions you grant its mail/browser integration. Use read-only access for assessment where available, review numbered proposals, and keep recovery options in mind before approving changes.

Technical references: [Gmail date filtering](https://developers.google.com/workspace/gmail/api/guides/filtering), [RFC 8058](https://www.rfc-editor.org/rfc/rfc8058.html), and [GitHub ignoring files](https://docs.github.com/en/get-started/git-basics/ignoring-files).

## License

[MIT](LICENSE)
