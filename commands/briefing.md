---
description: Get a daily briefing of today's calendar events, available legacy reminders, and optional inbox context
argument-hint: [YYYY-MM-DD] [IANA timezone, e.g. America/New_York]
disable-model-invocation: true
---

Build a daily briefing using tools exposed by the connected client. Do not call tools that are unavailable to this account.

If the user provided a date argument, use it. Otherwise default to today.
If the user provided a timezone argument, use it. Otherwise try to infer from context or omit.

1. Call `pear_list_events` for the chosen day
2. If legacy reminder access is relevant and the tool is available, call `pear_list_reminders` for incomplete legacy reminders. Explain that Pear cannot read Apple's upgraded Reminders store. If Apple returns migration placeholders or no legacy data, do not imply the user has no current tasks
3. If Mail is likely relevant, call `pear_list_emails` on `INBOX` with `unreadOnly: true` and a small limit

Present the briefing in a clear, scannable format:
1. **Date and day of week** as a header
2. **Events** listed chronologically with times, titles, locations, and attendee names
3. **Legacy reminders** listed by priority, showing due dates where set; state the compatibility limitation when current Apple reminders are unavailable
4. **Unread Mail** only if you checked it and found relevant messages
5. A brief natural-language summary at the end (e.g., "You have 3 meetings, 5 pending tasks, and 2 unread emails today")

ARGUMENTS: $ARGUMENTS
