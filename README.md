# CoreMem Claude Plugin

A Claude Code plugin that connects your mems to your coding sessions. Claude loads relevant context automatically, and you can propose updates back to your mem store without leaving the editor.

This plugin uses the [CoreMem MCP server](https://coremem.app/integrations#mcp) for all reads and writes. 

## How it works

When you install the plugin, Claude Code gains access to five MCP tools:

- `list_mems` — see what mems you have
- `get_mem` — read a specific mem
- `search_mems` — find mems by keyword
- `create_mem` — propose a brand-new mem for your review
- `propose_update` — propose a change to an existing mem for your review

Four skills wire those tools into your workflow:

| Skill | How to invoke | What it does |
|---|---|---|
| `recall` | `/coremem:recall [query]` | Searches for mems relevant to your current task and loads them |
| `create` | `/coremem:create [name] [content]` | Proposes a new mem — nothing is saved until you approve it |
| `learn` | `/coremem:learn [topic] [content]` | Proposes an update to an existing mem — nothing is applied until you approve it |
| `list` | `/coremem:list [filter]` | Lists all your mems |

`recall` is model-invoked, meaning Claude decides when to use it. If you are working on something and Claude thinks context from your mems would help, it loads it. You can also call it directly with a query if you want to pull something specific.

`create`, `learn`, and `list` are user-invoked only. Claude will not trigger them on your behalf.

## Requirements

- Claude Code 1.0.33 or later
- A CoreMem account (API key required)
- (Optional) [CoreMem Pro](https://coremem.app/pricing) for `learn` feature

## Setup

Generate a key at [coremem.app](https://coremem.app/integrations#mcp). Then, add your key to your environment, e.g.,

```bash
export COREMEM_API_KEY=your-api-key
```

### Install from local clone

Until the plugin is available on the Claude store, you can install it from a local clone:

1. Clone this repository:
   ```bash
   git clone https://github.com/coremem/claude-plugin.git
   ```

2. Register the cloned directory as a local marketplace:
   ```bash
   claude plugin marketplace add /path/to/claude-plugin
   ```

3. Install the plugin from it:
   ```bash
   claude plugin install coremem@coremem
   ```

4. Start a new session of Claude and run `/coremem:list` to verify the plugin is installed and the MCP connection is working

## AI Write-back

When Claude runs `/coremem:create` or `/coremem:learn`, it submits a proposal through the MCP server. Nothing changes in your mem store until you review and approve it. Review proposals in the [CoreMem web app](https://coremem.app/pending).