# Virlo plugin

Connects [Virlo](https://virlo.ai)'s TikTok, YouTube Shorts, and Instagram Reels intelligence API — trend discovery, creator lookups, niche research agents, and long-term tracking — to Cursor and Grok Build.

## Included

- `mcp.json`: Virlo's hosted remote MCP server (`https://dev.virlo.ai/api/mcp/mcp`, ~49 tools — check [dev.virlo.ai/docs/mcp](https://dev.virlo.ai/docs/mcp) for the current count)
- `rules/virlo-api-usage.mdc`: intent-first research, async job polling, and credit-cost awareness (Cursor rule; not a component Grok Build reads)
- `commands/`: `/trend-scout`, `/creator-deep-dive`, `/niche-analysis`, `/genre-monitor`
- `assets/logo.svg`: Virlo logo
- `.cursor-plugin/plugin.json`, `.grok-plugin/plugin.json`: per-client manifests (Cursor, Grok Build), both pointing at the same `mcp.json`

## Setup

1. Get an API key at [dev.virlo.ai/dashboard/api-keys](https://dev.virlo.ai/dashboard/api-keys) (starts with `virlo_tkn_`).
2. Set `VIRLO_API_KEY` in your environment (`mcp.json` reads it via `${env:VIRLO_API_KEY}`, Cursor's substitution syntax — confirm your client's equivalent if it differs).
3. Install this plugin and restart your client.

Full tool reference: [dev.virlo.ai/docs/mcp](https://dev.virlo.ai/docs/mcp).

## Network & credentials

The only endpoint this plugin talks to is Virlo's own MCP server, `https://dev.virlo.ai/api/mcp/mcp`, authenticated with the `VIRLO_API_KEY` you provide (a `virlo_tkn_...` bearer token, sent only in the `Authorization` header of that request). No other network calls, no telemetry, no filesystem access beyond what your client already grants the MCP process.

## Layout

Single-plugin repo per the [Cursor plugin template](https://github.com/cursor/plugin-template): plugin files live at the repo root, one `.cursor-plugin/plugin.json`, no `marketplace.json`. `.grok-plugin/plugin.json` is the equivalent manifest for [xAI's plugin marketplace](https://github.com/xai-org/plugin-marketplace).

Most research tools here are billed per call (see the pricing table at the link above) — they're exposed as explicit slash commands rather than a skill, so the agent doesn't spend credits without the user asking.
