# Pear — iCloud Integration for Claude Code

Give Claude read/write access to your **iCloud Calendar, Reminders & Contacts** through 27 MCP tools.

Works cross-platform via CalDAV/CardDAV — no macOS required.

## Quick Start

### 1. Get a Pear API Key

Sign up at [pearmcp.com](https://pearmcp.com), connect your iCloud account, and generate an API key.

> You'll need an [Apple app-specific password](https://support.apple.com/en-us/102654) to connect your iCloud account.

### 2. Set Your API Key

```bash
# Add to your shell profile (.bashrc, .zshrc, etc.)
export PEAR_API_KEY=pear_sk_your_key_here
```

### 3. Install the Plugin

**From GitHub:**
```
/plugin marketplace add AshtonAU/pear-plugin
/plugin install pear@pear-marketplace
```

**Or add the MCP server directly:**
```bash
claude mcp add --transport http pear https://pearmcp.com/api/mcp \
  --header "Authorization: Bearer $PEAR_API_KEY"
```

### 4. Verify Setup

```
/pear:pear-setup
```

## What You Get

### 27 MCP Tools

| Domain | Tools | Capabilities |
|--------|-------|-------------|
| **Calendar** | 8 | List calendars, CRUD events, find free slots, check availability |
| **Reminders** | 4 | CRUD reminders with priorities, due dates, completion |
| **Contacts** | 9 | CRUD contacts, groups, photo management, search |
| **Briefing** | 1 | Daily summary with contact-enriched attendees |
| **Scheduling** | 1 | AI-scored optimal meeting times |
| **Batch** | 4 | Bulk create/delete up to 50 items per call |

### Slash Commands

| Command | Description |
|---------|-------------|
| `/pear:briefing` | Get today's events and reminders at a glance |
| `/pear:schedule` | Find the best time for a meeting |
| `/pear:pear-setup` | Verify your API key and iCloud connection |

### Smart Features

- **Virtual Birthdays** — Birthday events generated from contact data
- **AI Scheduling** — Scores time slots by work hours, preferences, and conflicts
- **Attendee Resolution** — Names in events are matched to your contacts
- **Batch Operations** — Create up to 50 events/reminders/contacts in one call
- **Full Timezone Support** — IANA timezone handling across all operations

## Examples

```
> What's on my calendar today?
> Schedule a 45-minute meeting with Sarah this week
> Remind me to submit the report by Friday
> What's John's phone number?
> Create a recurring weekly standup on Mondays at 9am
> Find me 3 free slots for a 2-hour workshop next week
```

## How It Works

Pear acts as a secure bridge between Claude and iCloud:

```
Claude Code                    Pear API                     iCloud
    │                             │                            │
    │── PEAR_API_KEY (Bearer) ──▶ │                            │
    │                             │── CalDAV/CardDAV (TLS) ──▶ │
    │                             │◀── Calendar/Contact data ──│
    │◀── MCP JSON-RPC ───────── │                            │
```

## Data Access & Privacy

- Pear reads and writes to your iCloud Calendar, Reminders, and Contacts
- Your iCloud credentials are stored encrypted on Pear's servers, never shared with Claude
- Claude only receives your `PEAR_API_KEY`, which authenticates to the Pear API
- All data in transit is encrypted via HTTPS/TLS
- Pear does not store your calendar or contact data — it proxies requests to iCloud in real time

## Requirements

- A [Pear](https://pearmcp.com) account with a connected iCloud account
- An Apple [app-specific password](https://support.apple.com/en-us/102654)
- Claude Code 1.0.33+

## Links

- [Pear Documentation](https://pearmcp.com/docs)
- [Pear Dashboard](https://pearmcp.com/dashboard)
- [Report Issues](https://github.com/AshtonAU/pear-plugin/issues)

## License

MIT
