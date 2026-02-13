---
description: Set up Pear by verifying your API key and testing the iCloud connection
disable-model-invocation: true
---

Help the user verify their Pear setup by testing the connection:

1. Call `pear_list_calendars` to test the connection
   - **On success:** Show the list of calendars and confirm "Pear is connected to iCloud"
   - **On auth error (-32001):** The API key is missing or invalid. Tell the user:
     - Set the environment variable: `export PEAR_API_KEY=pear_sk_...`
     - Sign up at [pearmcp.com](https://pearmcp.com) to get an API key
     - They need an [Apple app-specific password](https://support.apple.com/en-us/102654) connected to their Pear account
   - **On connection error:** The MCP endpoint may be unreachable. Suggest checking `PEAR_MCP_URL` or network connectivity

2. On success, summarize what's available:
   - Number of calendars found (list their names)
   - Available commands: `/pear:briefing`, `/pear:schedule`
   - Mention they can ask things like "What's on my calendar today?" or "Remind me to..."
