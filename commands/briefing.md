---
description: Get a daily briefing of today's calendar events and pending reminders
argument-hint: [YYYY-MM-DD] [IANA timezone, e.g. America/New_York]
disable-model-invocation: true
---

Get a daily briefing using `pear_get_daily_briefing`.

If the user provided a date argument, use it. Otherwise default to today.
If the user provided a timezone argument, use it. Otherwise try to infer from context or omit.

Present the briefing in a clear, scannable format:
1. **Date and day of week** as a header
2. **Events** listed chronologically with times, titles, locations, and attendee names
3. **Reminders** listed by priority, showing due dates where set
4. A brief natural-language summary at the end (e.g., "You have 3 meetings and 5 pending tasks today")

ARGUMENTS: $ARGUMENTS
