---
name: list
description: List all available CoreMem mems in the user's account.
disable-model-invocation: true
allowed-tools: mcp__coremem__list_mems
---

Fetch and display the user's CoreMem mems.

1. Call `list_mems` to retrieve all available mems
2. Present them as a clean list showing each mem's name, slug, and a brief description if available
3. Note the total count

If $ARGUMENTS is provided, filter the list to mems whose name or description contains that string.
