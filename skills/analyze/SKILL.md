---
name: analyze
description: >
  Pull ad campaign performance data from connected platforms. Use when the user
  asks about campaign results, ROAS, ad spend, CTR, conversions, search terms,
  negative keywords, ad fatigue, budget pacing, delivery issues, or wants to
  diagnose why ads aren't spending. Also use for Google search term reports
  and keyword performance analysis. Not for creating campaigns, browsing
  competitor ads, or generating creatives.
---

# Analyze Performance

Requires a connected platform — run `/ads:setup` first if needed.

## 1. Fetch results

Use `adkit_manage` with `entity: "results"` and `action: "list"` on any connected platform:

```
adkit_manage platform: "<platform>" entity: "results" action: "list" params: { level: "campaigns", period: "30d" }
```

### Common params (all platforms)

| Param | Description |
|-------|-------------|
| `level` | `campaigns`, `adsets`/`ad-groups`, `ads` (Meta also: no level = account; Google also: `keywords`) |
| `period` | `today`, `yesterday`, `7d`, `14d`, `30d`, `this_month`, `last_month`, `this_quarter`, `last_year`, `maximum` |
| `from` / `to` | `YYYY-MM-DD` custom date range (use instead of period) |
| `sort` | `cost`, `clicks`, `impressions`, `conversions` |
| `limit` | Max rows to return |

Use `period` for presets, or `from` + `to` for custom ranges. Don't combine both.

### Platform-specific features

Available breakdowns, metrics, and additional actions vary by platform. Call `adkit_help path: "manage <platform> results"` for the full list. Key differences:

- **Meta**: `breakdown` (day, age, gender, country, device), `attribution-window`, `actions` filter
- **Google**: `breakdown` (device, network), plus separate `search-terms`, `placements`, and `keywords` actions
- **TikTok**: `dimensions` and `metrics` pass through to TikTok reporting API

### Filtering by entity

Filter results to a specific campaign or ad group:

| Platform | Param |
|----------|-------|
| Meta | `campaign: "<id>"`, `adset: "<id>"`, `ad: "<id>"` |
| Google | `campaignId: "<id>"`, `adGroupId: "<id>"` |
| TikTok | Uses `dimensions` — check `adkit_help` |

## 2. Google-specific entities

Google Ads has additional entities beyond standard results:

| Entity | Action | Use case |
|--------|--------|----------|
| `results` | `search-terms` | Actual queries that triggered ads |
| `results` | `placements` | Where ads appeared (Display/YouTube) |
| `keywords` | `list` | Managed keyword list for an ad group |
| `keywords` | `create` | Add keywords (including negative match types) |

`search-terms` and `keywords` are different: search terms are what users typed, keywords are what you're targeting/excluding.

## 3. Multi-account

If the user has multiple ad accounts, pass `accountId` in params. Call `adkit_status` to see available accounts — if omitted, the first account is used.
