---
name: list
description: List all available CoreMem mems in the user's account.
disable-model-invocation: true
allowed-tools: mcp__coremem__list_mems
---

Call `list_mems` and present the results as a clean list showing each mem's name and slug. Do not show IDs. Note the total count.

If $ARGUMENTS is provided, filter the list to mems whose name contains that string.
