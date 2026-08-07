---
name: spy
description: >
  Research competitor ads using the ad library. Use when the user wants to spy
  on competitor ads, see what ads a brand is running, browse competitor creatives,
  find top-performing ads, or do ad library research. Also use when the user
  mentions "ad library", "what ads is X running", "competitor creatives", or
  wants to track a new advertiser. Not for creating campaigns or pulling your
  own performance data.
---

# Spy on Competitor Ads

The ad library (`adkit_library`) lets you search advertisers and browse their ads across platforms.

Requires AdKit to be connected — run `/ads:setup` first if needed.

## 1. Find the advertiser

Search by name:
```
adkit_library entity: "advertisers" action: "search" params: { search: "Notion" }
```

Or browse by industry:
```
adkit_library entity: "advertisers" action: "list" params: { industry: "SaaS", sort: "spend" }
```

### Advertiser actions

| Action | Key params |
|--------|-----------|
| `list` | `industry`, `category`, `platform`, `sort` (name/newest/spend) |
| `search` | `search` (required), plus any list filters |
| `get` | `id` — full advertiser details and stats |
| `similar` | `advertiserId` — find similar advertisers |
| `add` | `website` or `name` — track a new advertiser |

## 2. Browse their ads

```
adkit_library entity: "ads" action: "search" params: { advertiser: "<advertiserId>", sort: "score" }
```

### Ad search params

| Param | Description |
|-------|-------------|
| `advertiser` | Advertiser ID filter |
| `query` | Free text search across ad copy |
| `platform` | `meta`, `google`, or `linkedin` |
| `format` | `image`, `video`, or `carousel` |
| `sort` | `random`, `newest`, `oldest`, `score`, `most-used`, `longest`, `spend` |

Advanced filters (min-days, min-spend, min-score, language) available via `adkit_help path: "library ads search"`.

Get full details: `adkit_library entity: "ads" action: "get" id: "<adId>"` — returns creative content, copy, metadata, and landing page.

## 3. Clone an ad

Found an ad worth replicating? Clone it via the studio skill:
```
adkit_studio entity: "ads" action: "generate" params: { mode: "clone", aspectRatio: "1:1", references: [{ type: "library-ad", id: "<adId>" }] }
```
