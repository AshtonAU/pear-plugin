# Pear MCP for the Cursor editor

Connect the Cursor editor to Apple iCloud and Microsoft 365 through Pear's hosted
Streamable HTTP MCP endpoint. Each member signs in to their own Pear account using
OAuth. The package contains a public Client ID, no client secret, and no API key.

## Install

1. Create a [Pear account](https://pearmcp.com) and connect an Apple iCloud or
   Microsoft 365 account in your [dashboard](https://pearmcp.com/dashboard).
2. In the Cursor dashboard, open **Plugins** and add
   `https://github.com/AshtonAU/pear-plugin` as a team marketplace.
3. Install **Pear MCP**. If your team uses an MCP allowlist, allow exactly
   `https://pearmcp.com/api/mcp`.
4. Complete Pear OAuth in Cursor with your own account. Every member must
   authorize separately; a team install does not share another member's access.
5. Begin with a read-only request, such as listing your calendars. Check the
   returned account before making changes.

For a direct editor connection, use [Add Pear to Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=pear&config=eyJ1cmwiOiJodHRwczovL3BlYXJtY3AuY29tL2FwaS9tY3AiLCJhdXRoIjp7IkNMSUVOVF9JRCI6InBlYXJfb2F1dGhfZ3Jva19ib3QifX0=).
The public Client ID `pear_oauth_grok_bot` is the existing editor registration;
its historical name does not indicate Grok Bot support.

## Capabilities and limits

Pear provides email, calendar, contacts, scheduling, and supported task/reminder
tools. Availability depends on the connected provider, granted scopes, account
readiness, and plan. Consult the [tool reference](https://pearmcp.com/mcp-tools)
and the connection's `tools/list` result.

Apple's upgraded Reminders store is not supported. Apple reminder operations
apply only to legacy CalDAV `VTODO` data. Microsoft 365 uses its supported
provider-specific tasks and other capabilities. Google is not supported yet.

## Account safety

- Do not add a personal Pear API key as a team plugin variable or commit it.
- Keep sending, deleting, and other consequential actions behind explicit user
  approval and the approval flow exposed by the connection.
- Revoke the connected app from Pear Settings and remove the plugin when access
  is no longer required.
- Read [data handling](https://pearmcp.com/data-handling),
  [privacy](https://pearmcp.com/privacy), and [terms](https://pearmcp.com/terms).
  Pear retains encrypted connection credentials, operational metadata, and
  persisted approved-write records; it is not a no-retention service.

## Verification and scope

The package uses Pear's documented Cursor editor OAuth configuration. The native
Cursor app discovered and installed this package from a local repository on
20 October 2026. Package checks and installation do not establish a successful
Pear authorization, refresh, revocation, or provider-read lifecycle. That
end-to-end validation is still pending; this package does not claim marketplace
acceptance.

This package targets the editor. Cursor Cloud Agents require a separate OAuth
connection and are not configured by this plugin; see the
[Cursor guide](https://pearmcp.com/guides/cursor). Grok Bot is not supported.

For help, contact [support@pearmcp.com](mailto:support@pearmcp.com).
