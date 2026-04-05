---
description: Get a daily briefing of today's calendar events, reminders, and optional inbox context
argument-hint: [YYYY-MM-DD] [IANA timezone, e.g. America/New_York]
disable-model-invocation: true
---

Build a daily briefing using Pear's base tools.

If the user provided a date argument, use it. Otherwise default to today.
If the user provided a timezone argument, use it. Otherwise try to infer from context or omit.

1. Call `pear_list_events` for the chosen day
2. Call `pear_list_reminders` for incomplete reminders
3. If Mail is likely relevant, call `pear_list_emails` on `INBOX` with `unreadOnly: true` and a small limit

Present the briefing in a clear, scannable format:
1. **Date and day of week** as a header
2. **Events** listed chronologically with times, titles, locations, and attendee names
3. **Reminders** listed by priority, showing due dates where set
4. **Unread Mail** only if you checked it and found relevant messages
5. A brief natural-language summary at the end (e.g., "You have 3 meetings, 5 pending tasks, and 2 unread emails today")

ARGUMENTS: $ARGUMENTS
