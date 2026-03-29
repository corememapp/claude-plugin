---
name: recall
description: Load relevant CoreMem mems into context. Use when starting a new task, when the user mentions "mems" or "context", when the task involves a domain the user may have documented, or when background knowledge would improve your response.
allowed-tools: mcp__coremem__list_mems, mcp__coremem__get_mem, mcp__coremem__search_mems, Bash
---

Load relevant context from the user's CoreMem mem store.

## MCP path (preferred)

If the `coremem` MCP server is connected, use it:

1. Call `search_mems` with 2-3 keywords that describe the current task or topic
2. If no relevant results, call `list_mems` to browse what is available
3. Call `get_mem` on any mems that look relevant
4. Briefly acknowledge what context was loaded before proceeding

If $ARGUMENTS is provided, treat it as the search query instead of inferring keywords from context.

## CLI fallback

If the MCP server is not connected, check for the CLI:

```bash
which coremem 2>/dev/null && echo "available" || echo "not available"
```

If available, check for a token:

```bash
echo "${COREMEM_TOKEN:-not set}"
```

If the token is set, run:

```bash
coremem recall --token $COREMEM_TOKEN
```

Parse the JSON output and use the mem content as context.

If neither MCP nor CLI is available, tell the user how to set up one of the two options.

Do not load mems that are clearly unrelated to the current task. Prefer relevance over completeness.
