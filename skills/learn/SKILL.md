---
name: learn
description: Propose an update to an existing CoreMem mem. Use when the user wants to correct or add to an existing mem. Do NOT use this to create a new mem — use create for that.
disable-model-invocation: true
allowed-tools: mcp__coremem__list_mems, mcp__coremem__get_mem, mcp__coremem__search_mems, mcp__coremem__propose_update, Bash
argument-hint: [mem name or topic] [content to add or update]
---

Propose an update to a CoreMem mem using $ARGUMENTS as guidance.

## MCP path (preferred)

If the `coremem` MCP server is connected:

1. Parse $ARGUMENTS to identify the target mem and the proposed content
   - If a mem name or slug is provided, look it up directly with `get_mem`
   - Otherwise, use `search_mems` to find the most relevant mem
2. Read the current mem content with `get_mem` so the proposal is coherent with what is already there
3. Draft the proposed update — incorporate new information rather than replacing existing content unless the user explicitly asked to replace it
4. Call `propose_update` with the mem ID and the proposed new content
5. Confirm the proposal was submitted and remind the user to review it in the CoreMem dashboard before it is applied

## CLI fallback

If the MCP server is not connected, check for the CLI and token:

```bash
which coremem 2>/dev/null && echo "${COREMEM_TOKEN:-not set}"
```

If both are available, run:

```bash
coremem learn --token $COREMEM_TOKEN --content "<proposed content>"
```

If neither is available, tell the user what to set up.

If $ARGUMENTS is empty, ask the user what they want to update and what the new content should be.

Note: proposals are never applied automatically. The user reviews and approves all changes in the CoreMem web app or via `coremem-admin proposals`.
