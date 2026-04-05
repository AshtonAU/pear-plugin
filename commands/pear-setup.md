---
description: Set up Pear by verifying your API key and testing the iCloud connection
disable-model-invocation: true
---

Help the user verify their Pear setup by testing the connection:

1. Call `pear_list_calendars` to test the core connection
   - **On success:** Show the list of calendars and confirm "Pear is connected to iCloud Calendar, Reminders, and Contacts"
   - **On auth error (-32001):** The API key is missing or invalid. Tell the user:
     - Set the environment variable: `export PEAR_API_KEY=pear_sk_...`
     - Sign up at [pearmcp.com](https://pearmcp.com) to get an API key
     - They need an [Apple app-specific password](https://support.apple.com/en-us/102654) connected to their Pear account
   - **On connection error:** The MCP endpoint may be unreachable. Suggest checking `PEAR_MCP_URL` or network connectivity

2. If the user expects Mail support, call `pear_list_mail_folders`
   - **On success:** Confirm Mail is connected too
   - **On failure while calendars succeeded:** Explain that Calendar, Reminders, and Contacts are connected, but Mail may require the mailbox's real `@icloud.com` address or iCloud Mail custom-domain address during Pear onboarding

3. On success, summarize what's available:
   - Number of calendars found (list their names)
   - Mail status if checked
   - Available commands: `/pear:briefing`, `/pear:schedule`
   - Mention they can ask things like "What's on my calendar today?", "Remind me to...", or "Show me unread iCloud Mail from today"
