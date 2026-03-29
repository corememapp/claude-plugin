---
name: list
description: List all available CoreMem mems in the user's account.
disable-model-invocation: true
allowed-tools: mcp__coremem__list_mems, Bash
---

List the user's CoreMem mems.

## MCP path (preferred)

If the `coremem` MCP server is connected, call `list_mems` and present the results as a clean list showing each mem's name, slug, and description. Note the total count.

## CLI fallback

If the MCP server is not connected, check for the CLI and token:

```bash
which coremem 2>/dev/null && echo "${COREMEM_TOKEN:-not set}"
```

If both are available, run:

```bash
coremem recall --token $COREMEM_TOKEN
```

Parse the JSON and display the available mems.

If neither is available, tell the user what to set up.

If $ARGUMENTS is provided, filter the list to mems whose name or description contains that string.
