---
description: Suggest meeting times across your selected iCloud and Microsoft 365 calendars, without booking anything
argument-hint: [duration in minutes] [date range, up to 7 days] [IANA timezone]
disable-model-invocation: true
---

Use the `pear-find-time` skill.

- Duration: from the arguments, otherwise ask.
- Range: from the arguments (up to 7 days), otherwise the next 5 working days.
- Timezone: from the arguments; otherwise ask rather than guess.
- Calendars: use the ones the user names; if unclear, use `pear-account-selection` first.

Return up to three options with local start and end times, the timezone, which
calendars were checked, and anything that couldn't be checked. Do not create events,
hold slots or invite anyone.

ARGUMENTS: $ARGUMENTS
