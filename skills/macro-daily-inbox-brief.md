---
name: macro-daily-inbox-brief
description: Summarize a Macro unified inbox into an action-oriented brief (needs reply today / FYI / waiting on others) using the Macro MCP server.
api: Macro
method: generated
source: https://docs.macro.com/AI/recipes.md
generated: '2026-07-20'
mcp_server: https://mcp-server.macro.com/mcp
operations:
- ListEntities
- ReadThread
- GetThread
- ReadMetadata
- ContentSearch
---

# Macro: Daily Inbox Brief

Produce a morning triage of the user's Macro unified inbox. Grounded in the Macro
MCP server tools; connect over OAuth first (browser sign-in).

## Steps
1. Use `ListEntities` to enumerate recent inbox threads/emails, or `ContentSearch`
   to scope to unread/needs-attention items.
2. For each thread, call `GetThread` / `ReadThread` and `ReadMetadata` to read the
   conversation and sender/label metadata.
3. Classify each item into: **needs a reply today**, **FYI**, or **waiting on others**.
4. Emit a compact grouped brief with a one-line summary and the @mention link for each item.

## Conventions
- Auth: OAuth via MCP connect (see authentication/macro-authentication.yml).
- Read-only skill — do not send or modify. Use the reply skill for drafting.
- Permissions follow channel membership; only surface items the connected user can see.
