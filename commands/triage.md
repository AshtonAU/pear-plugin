---
description: Review recent mail in one folder and group it into replies, follow-ups and information, without changing the mailbox
argument-hint: [days back, max 7] [folder, default INBOX]
disable-model-invocation: true
---

Use the `pear-mail-triage` skill.

- Window: the number of days in the arguments (maximum 7), otherwise the last 2 days.
- Folder: the folder in the arguments, otherwise `INBOX`.
- If more than one mail account is connected and the user hasn't said which, ask before reading.

Return a short table of likely replies, follow-ups, information and items that need the
user's judgement, with the evidence for each. State the checked interval and anything
not covered. Suggest next steps as text only; do not mark, move, flag, delete or send.

ARGUMENTS: $ARGUMENTS
