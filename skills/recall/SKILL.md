---
name: recall
description: Load relevant CoreMem mems into context. Use when starting a new task, when the user mentions "mems" or "context", when the task involves a domain the user may have documented, or when background knowledge would improve your response.
allowed-tools: mcp__coremem__list_mems, mcp__coremem__get_mem, mcp__coremem__search_mems
---

Load relevant context from the user's CoreMem mem store:

1. Call `search_mems` with 2-3 keywords that describe the current task or topic
2. If no search results are relevant, call `list_mems` to browse what is available
3. Call `get_mem` on any mems that look relevant to the task at hand
4. Briefly acknowledge what context was loaded before proceeding

If $ARGUMENTS is provided, treat it as the search query instead of inferring keywords from context.

Do not load mems that are clearly unrelated to the current task. Prefer relevance over completeness.
