---
name: pear-account-selection
description: Choose exact connected Pear accounts, calendars and mail folders for a workflow. Use when a source is missing, several accounts could match, or a brief needs setup. Does not change account defaults.
---

Identify whether the request needs Calendar, Mail or both. Discover Pear's actual
tool names and schemas in this host; prefixes can differ. A skill installation does
not establish sign-in, permission or provider health.

## Select accounts

Use `pear_provider_status` for account discovery. Filter by a known provider/account
when it expresses the user's choice; otherwise one unfiltered call lists visible
accounts. Read the structured `accounts[]` result, not a guessed provider list.

Match the intended account's returned `id` and runtime `provider`. Require connected
status, `featureEnabled`, `routingEnabled`, and the specific inventory/read tool in
`health.capabilities[].tools[]` with `readable: true`. Redacted placeholder IDs cannot
be used as selectors. If several accounts still match, ask the user to choose.
Do not select a default, invent an ID, or substitute an account after a failure.

- Apple uses `provider: "apple", accountId: "apple"`.
- Microsoft uses its returned account ID.
- Generic IMAP uses `provider: "mail"` for status and `provider: "auto"` with the
  same mandatory `accountId` for folder and mail tools. Require `accountKind: "mail"`.
  A `send_only_email` account cannot supply a mailbox read.

Microsoft calendar inventory and reads currently require `mcp:contacts:read` as
well as `mcp:calendar:read` under Pear's policy. Explain that extra permission before
consent. Do not silently expand an existing grant. Mail folder inventory needs
`mcp:mail:metadata`; status needs `mcp:tools:read`.

## Select calendars or folders

For a chosen calendar account, call `pear_list_calendars` with its exact binding,
`limit: 8` and `offset: 0`. For a chosen mail account, use `pear_list_mail_folders`
with its binding, `limit: 25` and `offset: 0`. Select the returned names or IDs the
user intends, preserving exact values. Microsoft child folders require the returned
`parentFolder` ID when that argument is exposed. Do not guess a nested folder path.

Keep this first selection pass to one status call and at most one inventory page
per selected capability. Report pagination and let the user request another page
or child folder if needed. A failed inventory is not an empty account. If the tool
schema omits `provider` or `accountId`, report that explicit selection is unavailable;
do not remove the binding to force execution.

Return the selected providers, account IDs, calendar selectors or mail folder, the
user-confirmed IANA timezone where needed, and any unresolved choices. Do not infer
timezone from an address. This selection record belongs in the user's private
conversation or explicitly requested private storage, never shared skill files.

The next workflow must check its own tool and grant requirements. Selecting a
calendar does not authorize event creation; selecting a folder does not authorize
message bodies, native drafts or sending. This skill reads inventory only. It does
not change defaults, save credentials, create routines or resolve modern Apple
Reminders' CalDAV limitation.
