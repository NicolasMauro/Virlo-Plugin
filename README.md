# Virlo Cursor plugin

Connects Cursor to [Virlo](https://virlo.ai)'s social media intelligence API — TikTok, YouTube Shorts, and Instagram Reels trend discovery, creator lookups, niche research agents, and long-term tracking.

Single-plugin repo (see the [Cursor plugin template](https://github.com/cursor/plugin-template) for the multi-plugin layout this was generated from).

## Included

- `mcp.json`: points at Virlo's hosted remote MCP server (`https://dev.virlo.ai/api/mcp/mcp`, 46 tools)
- `rules/virlo-api-usage.mdc`: baseline rules for intent-first research, async job polling, and credit awareness
- `skills/virlo-social-research/`: research workflows (full niche analysis, creator deep dive, trend scout, genre monitor)
- `commands/`: slash commands for the same four workflows (`/trend-scout`, `/creator-deep-dive`, `/niche-analysis`, `/genre-monitor`)
- `assets/logo.svg`: Virlo logo

## Setup

1. Get an API key at [dev.virlo.ai/dashboard/api-keys](https://dev.virlo.ai/dashboard/api-keys) (starts with `virlo_tkn_`).
2. Set `VIRLO_API_KEY` in your environment (`mcp.json` reads it via `${VIRLO_API_KEY}`).
3. Install this plugin in Cursor. Restart Cursor after installing.

Full tool reference: [dev.virlo.ai/docs/mcp](https://dev.virlo.ai/docs/mcp).

## Layout

This is a single-plugin repo (plugin files live at the repo root, one `.cursor-plugin/plugin.json`, no `.cursor-plugin/marketplace.json`) — see the [Cursor plugin template](https://github.com/cursor/plugin-template#single-plugin-vs-multi-plugin) for the multi-plugin alternative and its `scripts/validate-template.mjs` checker.
