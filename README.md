# CoreMem Claude Plugin

A Claude Code plugin that connects your mems to your coding sessions. Claude loads relevant context automatically, and you can propose updates back to your mem store without leaving the editor.

This plugin uses the [CoreMem MCP server](https://coremem.app) for all reads and writes. No CLI dependency required.

## How it works

When you install the plugin, Claude Code gains access to four MCP tools:

- `list_mems` — see what mems you have
- `get_mem` — read a specific mem
- `search_mems` — find mems by keyword
- `propose_update` — submit a proposed change for your review

Three skills wire those tools into your workflow:

| Skill | How to invoke | What it does |
|---|---|---|
| `recall` | Auto, or `/coremem:recall [query]` | Searches for mems relevant to your current task and loads them |
| `learn` | `/coremem:learn [topic] [content]` | Proposes an update to a mem — nothing is applied until you approve it |
| `list` | `/coremem:list [filter]` | Lists all your mems |

`recall` is model-invoked, meaning Claude decides when to use it. If you are working on something and Claude thinks context from your mems would help, it loads it. You can also call it directly with a query if you want to pull something specific.

`learn` and `list` are user-invoked only. Claude will not trigger them on your behalf.

## Requirements

- Claude Code 1.0.33 or later
- A CoreMem account with a Pro plan (API key required)

## Setup

Install the plugin and Claude Code will prompt you for your CoreMem API key:

```bash
claude plugin install coremem
```

Generate an API key at [coremem.app/developers](https://coremem.app/developers). The key is stored in your system keychain and used to authenticate requests to the CoreMem MCP server.

## Test locally

Clone this repo and load it directly without installing:

```bash
claude --plugin-dir .
```

Run `/help` to confirm the skills are registered under the `coremem` namespace. Try `/coremem:list` to verify the MCP connection is working.

## Proposals

When Claude runs `/coremem:learn`, it submits a proposal through the MCP server. Nothing changes in your mem store until you review and approve it. Review proposals in the CoreMem web app or with `coremem-admin proposals` if you use the CLI.
