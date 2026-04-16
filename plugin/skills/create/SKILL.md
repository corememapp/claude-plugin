---
name: create
description: Create a brand-new mem in the user's CoreMem library. Use only when the user explicitly asks to save or create something new in CoreMem. The proposal is queued for their review — it is never saved automatically.
disable-model-invocation: false
allowed-tools: mcp__coremem__create_mem
argument-hint: [mem name] [content]
---

Propose a new mem using $ARGUMENTS as guidance.

1. Parse $ARGUMENTS to identify the name and content for the new mem
   - If $ARGUMENTS is empty, ask the user for the mem name and what it should contain
2. Call `create_mem` with the name, content, and `is_public: false` unless the user explicitly asked for it to be public
3. Confirm the proposal was submitted and remind the user to review it in the CoreMem dashboard before it is saved

Note: proposals are never applied automatically. The user reviews and approves all changes in the CoreMem web app or via `coremem-admin proposals`.
