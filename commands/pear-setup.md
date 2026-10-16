---
description: Set up Pear by verifying your API key and testing the iCloud connection
disable-model-invocation: true
---

Help the user verify their Pear setup by testing the connection:

First inspect the tools exposed by the connected client; do not assume a fixed count or that unavailable tools can be called.

1. If available, call `pear_list_calendars` to test Calendar access
   - **On success:** Show the list of calendars and confirm only "Pear can read your connected iCloud calendars". A Calendar check does not verify Contacts, Mail, or Reminders access. Explain that Apple Reminders support is limited to legacy CalDAV data; upgraded Reminders are not accessible
   - **On auth error (-32001):** The API key is missing or invalid. Tell the user:
     - Set the environment variable: `export PEAR_API_KEY=pear_sk_...`
     - Sign up at [pearmcp.com](https://pearmcp.com) to get an API key
     - They need an [Apple app-specific password](https://support.apple.com/en-us/102654) connected to their Pear account
   - **On connection error:** The MCP endpoint may be unreachable. Suggest checking `PEAR_MCP_URL` or network connectivity

2. If the user expects Mail support, call `pear_list_mail_folders`
   - **On success:** Confirm Mail is connected too
   - **On failure while calendars succeeded:** Explain that Calendar was verified, but Mail was not. Mail may require the mailbox's real `@icloud.com` address or iCloud Mail custom-domain address during Pear onboarding

3. On success, summarize what's available:
   - Number of calendars found (list their names)
   - Mail status if checked
   - Available commands: `/pear:briefing`, `/pear:schedule`
   - Mention they can ask things like "What's on my calendar today?" or, if Mail was verified, "Show me unread iCloud Mail from today"
