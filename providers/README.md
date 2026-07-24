# Provider Plugins

This directory contains plugins for different AI code editors and agent harnesses.

Each provider has the same layout:

```
providers/<provider>/plugin/
├── skills/                 # Agent skills (mastercard-developers-bestpractice)
├── .mcp.json | mcp.json    # Mastercard Developers MCP server wiring
└── .<provider>-plugin/     # Provider-specific plugin manifest (plugin.json)
```

## Providers

| Provider | Plugin manifest | MCP config |
|----------|-----------------|------------|
| `claude` | `.claude-plugin/plugin.json` | `.mcp.json` |
| `codex`  | `.codex-plugin/plugin.json`  | `.mcp.json` |
| `cursor` | `.cursor-plugin/plugin.json` | `mcp.json`  |

## MCP server

Every plugin connects to the remote Mastercard Developers MCP server at
`https://developer.mcp.mastercard.com`, which requires **no authentication**.
A local `npx -y @mastercard/developers-mcp` alternative is documented in the
skill.

## Skills

Each plugin ships the `mastercard-developers-bestpractice` skill under
`skills/`. The skill instructs agents on how to set up the Mastercard
Developers MCP server (remote and local) and how to reach Mastercard
documentation in `llms.txt` format.

> **Do not edit the skill copies under `providers/*/plugin/skills/`.** They are
> generated from the canonical [`skills/`](../skills/) directory at the
> repository root. Edit the canonical file, then run `node scripts/sync.js`
> to propagate the change to every provider. `node scripts/sync.js --check`
> (also run in CI) verifies the copies are in sync.
