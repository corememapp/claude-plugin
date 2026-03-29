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

The plugin supports two auth methods. Use whichever fits your setup.

**Option 1 — API key (MCP server)**

Requires a Pro account. Generate a key at [coremem.app](https://coremem.app):

```bash
export COREMEM_API_KEY=your-api-key
```

**Option 2 — Share token (CLI)**

Requires the `coremem` CLI installed and a share token created via `coremem-admin`:

```bash
export COREMEM_TOKEN=your-share-token
```

The CLI path works fully offline against your local SQLite database.

Add whichever export(s) you use to your shell profile, then install the plugin:

```bash
claude plugin install coremem
```

## Test locally

Clone this repo, set `COREMEM_API_KEY`, and load the plugin directly:

```bash
export COREMEM_API_KEY=your-api-key
claude --plugin-dir .
```

Run `/coremem:list` to verify the MCP connection is working.

## Proposals

When Claude runs `/coremem:learn`, it submits a proposal through the MCP server. Nothing changes in your mem store until you review and approve it. Review proposals in the CoreMem web app or with `coremem-admin proposals` if you use the CLI.
