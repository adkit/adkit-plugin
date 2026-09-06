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

Use a `projectId` from `adkit_projects`. Pass it at the top level of library calls to choose whose watchlist to read or change.

## 1. Find the advertiser

Search by name:
```
adkit_library entity: "advertisers" action: "search" projectId: "<projectId>" params: { query: "Notion" }
```

Or browse by industry:
```
adkit_library entity: "advertisers" action: "list" params: { industry: "SaaS", sort: "spend" }
```

### Advertiser actions

| Action | Key params |
|--------|-----------|
| `list` | `scope` (library/watchlist), `industry`, `category`, `platform`, `sort` (name/newest/spend; default: newest), `limit`, `page` |
| `search` | `query` (required), plus any list filters |
| `get` | Top-level `id` — full advertiser details and stats |
| `similar` | `advertiserId` — find similar advertisers |
| `add` | `website` or a platform library URL required; `name` optional — find or create an advertiser and save it to the project watchlist |
| `track` | Top-level `id` — save an existing advertiser to the project watchlist |
| `untrack` | Top-level `id` — remove it from this project only |

### My Watchlist

Omitted `scope` (or `library`) includes all advertisers. Use `watchlist` to match the selected project's My Watchlist in the dashboard. Filters, pagination, and totals apply inside that scope.

```
adkit_library entity: "advertisers" action: "list" projectId: "<projectId>" params: { scope: "watchlist" }
adkit_library entity: "advertisers" action: "track" projectId: "<projectId>" id: "<advertiserId>"
adkit_library entity: "advertisers" action: "untrack" projectId: "<projectId>" id: "<advertiserId>"
```

Track/untrack return `advertiserId` and `tracked: true/false`. Repeating either is safe. Tracking requires an existing advertiser; untracking also removes stale membership for deleted advertisers. Untracking keeps the shared advertiser and other projects' watchlists. With only a name, search first and track the returned ID.

CLI equivalents:
```bash
adkit library advertisers list --scope watchlist --project <projectId>
adkit library advertisers search Notion --scope watchlist --project <projectId>
adkit library advertisers add --website notion.so --project <projectId>
adkit library advertisers track <advertiserId> --project <projectId>
adkit library advertisers untrack <advertiserId> --project <projectId>
```
Add `--json` for automation.

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
