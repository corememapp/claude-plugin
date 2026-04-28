---
name: list
description: List all available CoreMem mems in the user's account.
disable-model-invocation: false
allowed-tools: mcp__coremem__list_mems
---

List the user's CoreMem mems using the `coremem` MCP server.

Call `list_mems` and present the results as a clean list showing each mem's name, slug, and description. Note the total count.

If $ARGUMENTS is provided, filter the list to mems whose name or description contains that string.

If the `coremem` MCP server is not connected, tell the user to run `/mcp` in Claude Code to authenticate via OAuth, then restart their session.
