---
name: macro-call-transcript-to-tasks
description: Turn a Macro call transcript into assigned tasks, one per committed action item, using the Macro MCP server.
api: Macro
method: generated
source: https://docs.macro.com/AI/recipes.md
generated: '2026-07-20'
mcp_server: https://mcp-server.macro.com/mcp
operations:
- ContentSearch
- ReadContent
- CreateDocument
- SetEntityProperty
- ListEntities
---

# Macro: Call Transcript to Tasks

Extract action items from a call transcript and create one Macro task per commitment,
assigned to the owner. Grounded in the Macro MCP server tools.

## Steps
1. Locate the call with `ContentSearch` (or `ListEntities` scoped to calls), then
   `ReadContent` to load the transcript.
2. Identify each committed action item and who took it.
3. Create a task per item (via the create/entity tools, e.g. `CreateDocument` for a
   task entity), then `SetEntityProperty` to set assignee, status, and priority.
4. @mention the source call on each task so context is linked.

## Conventions
- Auth: OAuth via MCP connect (see authentication/macro-authentication.yml).
- Writes are not documented as idempotent — avoid re-running blindly; check with
  `ContentSearch` for existing tasks before creating duplicates.
- Assign only to workspace members surfaced by the connected user's permissions.
