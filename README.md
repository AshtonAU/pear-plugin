<div align="center">

# 🍐 Pear — iCloud for Claude Code

**Official Claude plugin, slash commands, and OpenClaw skill for Pear.**

Hosted MCP tools · iCloud Calendar, Contacts, Mail, and legacy CalDAV reminders · Cross-platform

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![MCP Tools](https://img.shields.io/badge/MCP_Tools-Reference-blue.svg)](https://pearmcp.com/mcp-tools)
[![Claude Code](https://img.shields.io/badge/Claude_Code-MCP_Compatible-purple.svg)](https://docs.anthropic.com/en/docs/claude-code)

[Get Started](https://pearmcp.com) · [Documentation](https://pearmcp.com/docs) · [Dashboard](https://pearmcp.com/dashboard)

</div>

---

## What is Pear?

Pear is a hosted MCP server that connects Claude Code to your iCloud Calendar, Contacts, Mail, and legacy CalDAV reminder data. Ask Claude to check your schedule, create events, look up contacts, read inbox context, and find meeting times through natural language.

**Apple Reminders limitation:** Pear cannot access Apple's upgraded Reminders store. Reminder operations apply only to legacy data still exposed through CalDAV `VTODO`; a successful Calendar connection does not prove current reminders are available. Reconnecting iCloud or changing an app-specific password cannot remove this protocol limitation. See [Apple Reminders compatibility](https://pearmcp.com/chatgpt-reminders).

```
> "What's on my calendar today?"
> "Schedule a 45-minute meeting with Sarah this week"
> "What's John's phone number?"
> "Show me unread iCloud Mail from today"
> "Find me 3 free slots for a 2-hour workshop next week"
```

Works on **macOS, Linux, and Windows** via CalDAV/CardDAV for Calendar, legacy reminders, and Contacts, plus IMAP/SMTP for iCloud Mail. No Apple hardware required.

## Install

### 1. Get a Pear API Key

Sign up at **[pearmcp.com](https://pearmcp.com)**, connect your iCloud account, and generate an API key.

> You'll need an [Apple app-specific password](https://support.apple.com/en-us/102654) to connect your iCloud account.
> If you want Mail support, connect using the real `@icloud.com` address or iCloud Mail custom-domain address tied to that mailbox.

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

- Hosted MCP tools across Calendar, legacy reminders, Contacts, Mail, scheduling, and batch operations; the visible subset depends on connected providers, granted scopes, account readiness, plan, and enabled capabilities
- Claude slash commands for common flows like setup, briefing, and scheduling
- One OpenClaw skill for users who want the same Pear integration outside Claude Code
- A direct MCP config via [.mcp.json](.mcp.json) for manual setups

## Repo Layout

This repo is intentionally small. Each top-level path maps to a specific client surface:

| Path | Purpose |
|------|---------|
| [`.claude-plugin/`](.claude-plugin) | Claude plugin and marketplace metadata |
| [`commands/`](commands) | Claude slash commands such as `/pear:briefing` |
| [`skills/pear-icloud/`](skills/pear-icloud) | OpenClaw skill definition |
| [`.mcp.json`](.mcp.json) | Direct MCP server config template |
| [`README.md`](README.md) | User-facing install and usage guide |

## MCP Capabilities

This is an overview, not a fixed tool count or a guarantee that every tool is available to every account. Use the [current tool reference](https://pearmcp.com/mcp-tools) and the connected client's `tools/list` result for available tools and their input schemas. Writes must follow the approval flow exposed by your connection.

| Domain | What You Can Do When Available |
|--------|-------------------------------|
| 📅 **Calendar** | Read and manage events, find free slots, and check availability |
| ✅ **Legacy reminders** | Read and manage only the reminder data Apple still exposes through CalDAV `VTODO`; upgraded Apple Reminders are unavailable |
| 👤 **Contacts** | Search and manage contacts and groups |
| 🧠 **Scheduling** | Find meeting times using preferences and conflicts |
| ⚡ **Batch** | Supported bulk operations within the limits in the tool schema |
| ✉️ **Mail** | Read inbox context and use permitted mail-management and sending workflows |

### Slash Commands

| Command | Description |
|---------|-------------|
| `/pear:briefing` | Today's events and available legacy reminders at a glance |
| `/pear:schedule` | Find the best time for a meeting |
| `/pear:pear-setup` | Verify your connection |

## Highlights

- **🎂 Virtual Birthdays** — Birthday events auto-generated from contact data
- **🧠 AI Scheduling** — Scores time slots by work hours, preferences, and conflicts
- **👥 Attendee Resolution** — Event attendees matched to your contacts automatically
- **✉️ iCloud Mail** — Read inbox context, send replies, and manage email folders through the same hosted MCP endpoint
- **⚡ Batch Operations** — Use supported bulk tools within their published limits; reminder operations remain legacy-only
- **🌍 Timezone Support** — Full IANA timezone handling across all operations
- **🔒 Data Handling** — Reads fetch provider records live; Pear also stores encrypted connection credentials, operational metadata, and persisted approved-write records. See [data handling](https://pearmcp.com/data-handling).

## How It Works

```
Claude Code                    Pear API                     iCloud
    │                             │                            │
    │── PEAR_API_KEY (Bearer) ──▶ │                            │
    │                             │── CalDAV/CardDAV/IMAP/SMTP ─▶ │
    │                             │◀── Calendar, Contacts, legacy reminders, Mail ─│
    │◀── MCP JSON-RPC ───────── │                            │
```

## Privacy & Security

| Concern | How Pear Handles It |
|---------|-------------------|
| iCloud credentials | Encrypted at rest, never shared with Claude |
| Ordinary provider reads | Fetched live and processed in memory; Pear does not maintain a synced content database |
| Connection and operational records | Encrypted credentials/tokens, connection metadata, usage counts, and activity/audit metadata are retained |
| Persisted approved writes | May retain the exact approved action, including relevant content, approval evidence, and provider receipt/result |
| API authentication | Bearer token (`PEAR_API_KEY`) — Claude never sees your Apple ID |
| Data in transit | HTTPS/TLS everywhere |

Retention and deletion details are described in [data handling](https://pearmcp.com/data-handling) and the [privacy policy](https://pearmcp.com/privacy). Do not treat this plugin as a no-retention service.

## Requirements

- A free [Pear](https://pearmcp.com) account
- An Apple ID with an [app-specific password](https://support.apple.com/en-us/102654)
- Claude Code with MCP support (or any MCP-compatible client)

## Links

- 🌐 [pearmcp.com](https://pearmcp.com) — Sign up & dashboard
- 📖 [Documentation](https://pearmcp.com/docs)
- 🐛 [Report Issues](https://github.com/AshtonAU/pear-plugin/issues)

## License

MIT — see [LICENSE](LICENSE) for details.
