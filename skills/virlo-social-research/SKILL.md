---
name: virlo-social-research
description: Research TikTok, YouTube Shorts, and Instagram Reels trends, creators, sounds, and niches using the Virlo API. Use for competitive research, content strategy, influencer scouting, or trend reports.
---

# Virlo social research

## When to use

- A user wants to understand what's trending in a niche, genre, or platform right now.
- A user wants a deep profile on a specific creator, video, or sound.
- A user wants ongoing tracking of a creator, video, or niche over time.

## Prerequisites

Requires the `virlo` MCP server connected (see `mcp.json`) with a valid `virlo_tkn_...` API key in `VIRLO_API_KEY`, and enough credit balance (`get_credit_balance`).

## Workflows

### Full niche analysis

1. Draft a concrete one-sentence intent for the niche (goal + content type + exclusions) and call `suggest_keywords`. Sharpen and retry if `quality.passes` is false.
2. Run `search_keywords` (one-shot Content Research Agent) with that intent and the suggested keywords. Do not pass `min_views` or `time_period` — filter at read time instead.
3. Poll `get_keyword_search_results` until `finalized: true`. Review videos, creator outliers (`order_by=weighted_score`), AI analysis, and trend themes.
4. `lookup_creator` on the top 2-3 outlier creators for full profiles.
5. Stand up a recurring agent with `create_niche_monitor` (same intent + keywords, cadence `weekly`) for ongoing tracking.
6. Summarize: top keywords/hashtags, most promising creators, content patterns, and the recurring monitor now in place.

### Creator deep dive

1. `lookup_creator` for the platform + username, including `videos,outliers`.
2. Identify top-performing videos, recurring themes/hashtags, posting cadence, and engagement ratios (views vs likes vs comments).
3. Ask before offering to `track_creator` for ongoing growth monitoring.
4. Summarize strengths, content strategy, and growth trajectory.

### Trend scout

1. `get_emerging_trends` (momentum-ranked, early-stage) and `get_trends_digest` (today's curated digest).
2. `get_trending_videos` (optionally filtered by platform) and `get_breakout_sounds`.
3. `search_hashtags` on the top 3-5 emerging topics.
4. Summarize: what's emerging, today's top trends, hottest videos (ranked by weighted virality, not raw views), and rising hashtags/sounds to watch.

### Genre monitor (TikTok)

1. Draft an intent for monitoring the genre/scene and call `suggest_keywords`; include synonyms and sub-scenes of the same concept.
2. `create_niche_monitor` with platforms `["tiktok"]`, cadence `weekly`.
3. Poll `get_niche_monitor_data` (`data_type: "overview"`) until `finalized: true`.
4. Read discovery signals (all free): `sounds` (`order_by: rising`), `hashtags` (`order_by: growth`), `outliers` (`order_by: rising`, filter by `follower_tier`), `benchmarks`, and `affinity`.
5. Deliver a genre brief: sound to ride this week, hashtags heating up, rising creators by tier, and how they compare to genre norms.

## Notes

- All research/analysis endpoints are billed per the pricing table in the Virlo MCP `MCP.md` / `dev.virlo.ai/docs/mcp` — check `get_credit_balance` first and confirm cost with the user before any paid call beyond the first.
- Async job status can also be polled generically via `check_job_status`.
