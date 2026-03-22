<div align="center">

# 🍐 Pear — iCloud for Claude Code

**Official Claude plugin, slash commands, and OpenClaw skill for Pear.**

27 MCP tools · Cross-platform · No macOS required

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![MCP Tools](https://img.shields.io/badge/MCP_Tools-27-blue.svg)](https://pearmcp.com/docs)
[![Claude Code](https://img.shields.io/badge/Claude_Code-MCP_Compatible-purple.svg)](https://docs.anthropic.com/en/docs/claude-code)

[Get Started](https://pearmcp.com) · [Documentation](https://pearmcp.com/docs) · [Dashboard](https://pearmcp.com/dashboard)

</div>

---

## What is Pear?

Pear is an MCP server that connects Claude Code to your iCloud account. Ask Claude to check your calendar, create events, manage reminders, look up contacts, and find meeting times through natural language.

```
> "What's on my calendar today?"
> "Schedule a 45-minute meeting with Sarah this week"
> "Remind me to submit the report by Friday"
> "What's John's phone number?"
> "Find me 3 free slots for a 2-hour workshop next week"
```

Works on **macOS, Linux, and Windows** via CalDAV/CardDAV — no Apple hardware required.

## Install

### 1. Get a Pear API Key

Sign up at **[pearmcp.com](https://pearmcp.com)**, connect your iCloud account, and generate an API key.

> You'll need an [Apple app-specific password](https://support.apple.com/en-us/102654) to connect your iCloud account.

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
clawhub install pear-icloud
```

### 4. Verify

```
/pear:pear-setup
```

## What You Get

- 27 MCP tools across Calendar, Reminders, Contacts, briefing, scheduling, and batch operations
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

## 27 MCP Tools

| Domain | Tools | What You Can Do |
|--------|:-----:|-----------------|
| 📅 **Calendar** | 8 | List calendars, create/read/update/delete events, find free slots, check availability |
| ✅ **Reminders** | 4 | Create/read/update/complete reminders with priorities and due dates |
| 👤 **Contacts** | 9 | Full CRUD for contacts and groups, photo management, smart search |
| 📋 **Briefing** | 1 | Daily summary with events, reminders, and contact-enriched attendees |
| 🧠 **Scheduling** | 1 | AI-scored optimal meeting times based on preferences and conflicts |
| ⚡ **Batch** | 4 | Bulk create/delete up to 50 items per call |

### Slash Commands

| Command | Description |
|---------|-------------|
| `/pear:briefing` | Today's events and reminders at a glance |
| `/pear:schedule` | Find the best time for a meeting |
| `/pear:pear-setup` | Verify your connection |

## Highlights

- **🎂 Virtual Birthdays** — Birthday events auto-generated from contact data
- **🧠 AI Scheduling** — Scores time slots by work hours, preferences, and conflicts
- **👥 Attendee Resolution** — Event attendees matched to your contacts automatically
- **⚡ Batch Operations** — Create up to 50 events/reminders/contacts in one call
- **🌍 Timezone Support** — Full IANA timezone handling across all operations
- **🔒 Privacy First** — Your data is proxied in real-time, never stored on Pear's servers

## How It Works

```
Claude Code                    Pear API                     iCloud
    │                             │                            │
    │── PEAR_API_KEY (Bearer) ──▶ │                            │
    │                             │── CalDAV/CardDAV (TLS) ──▶ │
    │                             │◀── Calendar/Contact data ──│
    │◀── MCP JSON-RPC ───────── │                            │
```

## Privacy & Security

| Concern | How Pear Handles It |
|---------|-------------------|
| iCloud credentials | Encrypted at rest, never shared with Claude |
| Calendar/contact data | Proxied in real-time, **not stored** on Pear servers |
| API authentication | Bearer token (`PEAR_API_KEY`) — Claude never sees your Apple ID |
| Data in transit | HTTPS/TLS everywhere |

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
