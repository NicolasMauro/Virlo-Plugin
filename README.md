# Virlo Cursor plugin

Connects Cursor to [Virlo](https://virlo.ai)'s social media intelligence API — TikTok, YouTube Shorts, and Instagram Reels trend discovery, creator lookups, niche research agents, and long-term tracking.

## Included

- `mcp.json`: Virlo's hosted remote MCP server (`https://dev.virlo.ai/api/mcp/mcp`, ~49 tools — check [dev.virlo.ai/docs/mcp](https://dev.virlo.ai/docs/mcp) for the current count)
- `rules/virlo-api-usage.mdc`: intent-first research, async job polling, and credit-cost awareness
- `commands/`: `/trend-scout`, `/creator-deep-dive`, `/niche-analysis`, `/genre-monitor`
- `assets/logo.svg`: Virlo logo

## Setup

1. Get an API key at [dev.virlo.ai/dashboard/api-keys](https://dev.virlo.ai/dashboard/api-keys) (starts with `virlo_tkn_`).
2. Set `VIRLO_API_KEY` in your environment (`mcp.json` reads it via `${env:VIRLO_API_KEY}`).
3. Install this plugin in Cursor and restart.

Full tool reference: [dev.virlo.ai/docs/mcp](https://dev.virlo.ai/docs/mcp).

## Layout

Single-plugin repo per the [Cursor plugin template](https://github.com/cursor/plugin-template): plugin files live at the repo root, one `.cursor-plugin/plugin.json`, no `marketplace.json`.

Most research tools here are billed per call (see the pricing table at the link above) — they're exposed as explicit slash commands rather than a skill, so the agent doesn't spend credits without the user asking.
