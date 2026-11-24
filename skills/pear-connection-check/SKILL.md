---
name: pear-connection-check
description: Check whether Pear is authenticated and can read one selected calendar or mailbox. Use for Pear setup, missing tools, and failed brief workflows.
---

Inspect the host's Pear connection before reading provider data. An installed plugin,
completed OAuth sign-in, permitted tools, and successful provider read are different
states.
Microsoft calendar checks currently require both `mcp:calendar:read` and
`mcp:contacts:read` under Pear's policy. Explain and verify that grant first;
do not silently request additional permission after a failed call.

1. Confirm the user's selected provider account and the read to perform. Inspect the
   current Pear tool schemas; host prefixes may differ from the `pear_*` names below.
2. If tools are absent or auth is required, use the host's provider-owned sign-in
   flow. Never ask for credentials, complete authorization URLs, tokens, or a key in
   chat. Do not copy a Cursor editor token into another host.
3. Call `pear_provider_status` with the selected `provider` and `accountId`. It reports
   configuration and capability routing. It does not prove current provider health.
   When authorization is present, report its grantedScopes and scopeMode for this
   connection. A missing field means permission evidence is unavailable, not that
   the connection is read-only. A write-capable grant stays write-capable even when
   this skill uses only reads. Never echo credentials or grant identifiers.
4. Check the selected account's exact readable tools before performing a small read:
   match `accounts[].id` and `provider`; require connected status, `featureEnabled`
   and `routingEnabled`, then `health.capabilities[].readable` and the tool in `tools[]`.
   `pear_list_calendars` with limit 1, or `pear_list_emails` with the exact folder and
   limit 1. Skip the read if its exact tool is unavailable, even if a broad capability
   exists. Send-only mail accounts do not expose inbox reads. For generic IMAP use
   `provider: "mail"` for status and `provider: "auto"` with the same explicit
   `accountId` for the read. Apple uses `provider: "apple", accountId: "apple"`.
   Other sources use their returned account IDs. Do not open message bodies.
5. Report the failing stage or successful read, checked-at time, and next step. A
   successful empty result is different from a failed read. Do not echo private
   message content, tokens, raw logs, or authorization query strings into diagnostics.

Stop on a team policy block, missing consent, unsupported registration, or rejected
callback. Do not weaken host policy, use browser login automation, install another
connector, or enable a routine as recovery. One connection check has at most two tool
calls and no writes. Authentication recovery is a separate user action.

For Apple Reminders, explain that upgraded Reminders are unavailable through Pear's
hosted CalDAV connection. Reconnecting does not change that limit.

A read-only workflow is not a read-only grant. Before an unattended routine, have the
user verify server-enforced read scopes for this connection. If that cannot be proved,
keep the routine disabled. Tool annotations and these instructions do not enforce scopes.
