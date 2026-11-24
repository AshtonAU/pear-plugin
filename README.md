<div align="center">

# 🍐 Pear — iCloud and Microsoft 365 for Claude Code

**Official Claude plugin, slash commands, and OpenClaw skill for Pear.**

Hosted MCP tools · iCloud and Microsoft 365 Calendar, Contacts, Mail and tasks · Cross-platform

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![MCP Tools](https://img.shields.io/badge/MCP_Tools-Reference-blue.svg)](https://pearmcp.com/mcp-tools)
[![Claude Code](https://img.shields.io/badge/Claude_Code-MCP_Compatible-purple.svg)](https://docs.anthropic.com/en/docs/claude-code)

[Get Started](https://pearmcp.com) · [Documentation](https://pearmcp.com/docs) · [Dashboard](https://pearmcp.com/dashboard)

</div>

---

## What is Pear?

Pear is a hosted MCP server that connects Claude Code and other MCP clients to Apple iCloud and Microsoft 365. With iCloud you get Calendar, Contacts, Mail and legacy CalDAV reminder data. With Microsoft 365 you get Outlook Calendar, Outlook Mail, Contacts and Microsoft To Do. Ask Claude to check your schedule, create events, look up contacts, read inbox context and find meeting times through natural language. Google Workspace is coming soon.

**Apple Reminders limitation:** On iCloud, Pear cannot access Apple's upgraded Reminders store. Reminder operations apply only to legacy data still exposed through CalDAV `VTODO`; a successful Calendar connection does not prove current reminders are available. Reconnecting iCloud or changing an app-specific password cannot remove this protocol limitation. See [Apple Reminders compatibility](https://pearmcp.com/chatgpt-reminders).

```
> "What's on my calendar today?"
> "Schedule a 45-minute meeting with Sarah this week"
> "What's John's phone number?"
> "Show me unread iCloud Mail from today"
> "Find me 3 free slots for a 2-hour workshop next week"
```

Works on **macOS, Linux, and Windows**. iCloud uses CalDAV/CardDAV for Calendar, legacy reminders and Contacts, plus IMAP/SMTP for Mail; Microsoft 365 uses Microsoft Graph. No Apple hardware or local server required.

## Cursor editor plugin

The repository also includes a separate [Pear MCP plugin for Cursor](plugins/pear-mcp/README.md)
with per-member OAuth for Apple iCloud and Microsoft 365. It does not require a
Pear API key. Follow that guide for installation, supported capabilities, and the
current native-client verification status. The Claude Code and OpenClaw setup
below continues to use the existing API-key configuration.

## Install for Claude Code or OpenClaw

### 1. Get a Pear API Key

Sign up at **[pearmcp.com](https://pearmcp.com)**, connect iCloud or Microsoft 365, and generate an API key in Settings. The key grants access to the services and permissions available to your Pear account.

> iCloud needs an [Apple app-specific password](https://support.apple.com/en-us/102654). Microsoft 365 connects through Microsoft sign-in.
> For iCloud Mail support, connect using the real `@icloud.com` address or iCloud Mail custom-domain address tied to that mailbox.

### 2. Set Your API Key

```bash
export PEAR_API_KEY=pear_sk_your_key_here
```

### 3. Choose an install path

**Option A — Claude Plugin:**
```
/plugin marketplace add AshtonAU/pear-plugin
/plugin install pear@pear-marketplace
```

**Option B — MCP Server (direct):**
```bash
claude mcp add --transport http pear https://pearmcp.com/api/mcp \
  --header "Authorization: Bearer $PEAR_API_KEY"
```

**Option C — OpenClaw Skill:**
```bash
clawhub install ashtonau/pear-apple
```

### 4. Verify

```
/pear:pear-setup
```

Already installed the marketplace? Refresh it with:

```bash
/plugin marketplace update pear-marketplace
```

## What You Get

- Hosted MCP tools across Calendar, Contacts, Mail, tasks (Microsoft To Do or legacy iCloud reminders), scheduling, and batch operations; the visible subset depends on connected providers, granted scopes, account readiness, plan, and enabled capabilities
- Claude slash commands for common flows like setup, briefing, scheduling, finding a time and mail triage
- Workflow skills for connection checks, account selection, morning briefs, finding a time, mail triage, reply drafts and reviewed changes
- A `pear-assistant` agent for multi-step calendar, mail and contact requests
- One OpenClaw skill for users who want the same Pear integration outside Claude Code
- A direct MCP config via [.mcp.json](.mcp.json) for manual setups

## Repo Layout

This repo is intentionally small. Each top-level path maps to a specific client surface:

| Path | Purpose |
|------|---------|
| [`.claude-plugin/`](.claude-plugin) | Claude plugin and marketplace metadata |
| [`.cursor-plugin/`](.cursor-plugin) | Cursor marketplace metadata |
| [`plugins/pear-mcp/`](plugins/pear-mcp) | Cursor editor plugin with per-member OAuth |
| [`commands/`](commands) | Claude slash commands such as `/pear:briefing` |
| [`agents/`](agents) | The `pear-assistant` agent |
| [`skills/pear-icloud/`](skills/pear-icloud) | Main Pear skill (also the OpenClaw skill definition) |
| [`skills/`](skills) | Workflow skills: connection check, account selection, morning brief, find time, mail triage, reply draft, reviewed changes |
| [`.mcp.json`](.mcp.json) | Direct MCP server config template |
| [`README.md`](README.md) | User-facing install and usage guide |

## MCP Capabilities

This is an overview, not a fixed tool count or a guarantee that every tool is available to every account. Use the [current tool reference](https://pearmcp.com/mcp-tools) and the connected client's `tools/list` result for available tools and their input schemas. Writes must follow the approval flow exposed by your connection.

| Domain | What You Can Do When Available |
|--------|-------------------------------|
| 📅 **Calendar** | Read and manage events, find free slots, and check availability |
| ✅ **Tasks** | Microsoft To Do lists and tasks; on iCloud, only the reminder data Apple still exposes through CalDAV `VTODO` (upgraded Apple Reminders are unavailable) |
| 👤 **Contacts** | Search and manage contacts and groups |
| 🧠 **Scheduling** | Find meeting times using preferences and conflicts |
| ⚡ **Batch** | Supported bulk operations within the limits in the tool schema |
| ✉️ **Mail** | iCloud Mail and Outlook Mail: read inbox context and use permitted mail-management and sending workflows |

### Slash Commands

| Command | Description |
|---------|-------------|
| `/pear:briefing` | Today's events and available legacy reminders at a glance |
| `/pear:schedule` | Find the best time for a meeting |
| `/pear:find-time` | Suggest meeting times across selected calendars, without booking |
| `/pear:triage` | Group recent mail in one folder into replies, follow-ups and information, without changing the mailbox |
| `/pear:pear-setup` | Verify your connection |

## Highlights

- **🎂 Virtual Birthdays** — Birthday events auto-generated from contact data
- **🧠 AI Scheduling** — Scores time slots by work hours, preferences, and conflicts
- **👥 Attendee Resolution** — Event attendees matched to your contacts automatically
- **✉️ iCloud and Outlook Mail** — Read inbox context, send replies, and manage email folders through the same hosted MCP endpoint
- **⚡ Batch Operations** — Use supported bulk tools within their published limits; reminder operations remain legacy-only
- **🌍 Timezone Support** — Full IANA timezone handling across all operations
- **🔒 Data Handling** — Reads fetch provider records live; Pear also stores encrypted connection credentials, operational metadata, and persisted approved-write records. See [data handling](https://pearmcp.com/data-handling).

## How It Works

```
Claude Code                    Pear API                 iCloud / Microsoft 365
    │                             │                            │
    │── PEAR_API_KEY (Bearer) ──▶ │                            │
    │                             │── CalDAV/CardDAV/IMAP/SMTP ▶│ iCloud
    │                             │── Microsoft Graph ────────▶│ Microsoft 365
    │                             │◀── Calendar, Contacts, Mail, tasks ─│
    │◀── MCP JSON-RPC ─────────── │                            │
```

## Privacy & Security

| Concern | How Pear Handles It |
|---------|-------------------|
| Provider credentials | iCloud app-specific passwords and Microsoft tokens are encrypted at rest and never shared with Claude |
| Ordinary provider reads | Fetched live and processed in memory; Pear does not maintain a synced content database |
| Connection and operational records | Encrypted credentials/tokens, connection metadata, usage counts, and activity/audit metadata are retained |
| Persisted approved writes | May retain the exact approved action, including relevant content, approval evidence, and provider receipt/result |
| API authentication | Bearer token (`PEAR_API_KEY`) — Claude never sees your Apple or Microsoft credentials |
| Data in transit | HTTPS/TLS everywhere |

Retention and deletion details are described in [data handling](https://pearmcp.com/data-handling) and the [privacy policy](https://pearmcp.com/privacy). Do not treat this plugin as a no-retention service.

## Requirements

- A free [Pear](https://pearmcp.com) account
- An Apple ID with an [app-specific password](https://support.apple.com/en-us/102654), or a Microsoft 365 / Outlook account
- Claude Code with MCP support (or any MCP-compatible client)

## Links

- 🌐 [pearmcp.com](https://pearmcp.com) — Sign up & dashboard
- 📖 [Documentation](https://pearmcp.com/docs)
- 🐛 [Report Issues](https://github.com/AshtonAU/pear-plugin/issues)

## License

MIT — see [LICENSE](LICENSE) for details.
