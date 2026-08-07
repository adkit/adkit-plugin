---
name: launch
description: >
  Launch ad campaigns on connected platforms. Use when the user wants to create
  a new campaign, set up targeting, configure ads, upload media, duplicate
  campaigns, or go live with new ads. All creations produce drafts that require
  explicit user approval before publishing. Not for performance analysis,
  competitor research, or AI creative generation.
---

# Launch Campaign

Requires a connected platform — run `/ads:setup` first if needed.

## 1. Campaign hierarchy

The structure is the same across platforms — only entity names differ:

| Level | Meta | Google | TikTok |
|-------|------|--------|--------|
| Campaign | `campaigns` | `campaigns` | `campaigns` |
| Ad group | `adsets` | `ad-groups` | `ad-groups` |
| Ad | `ads` | `ads` | `ads` |

Every `adkit_manage` call takes: `platform`, `entity`, `action`, and `params`.

## 2. Discover params then create

Call `adkit_help path: "manage <platform> <entity> create"` for the exact params. Universal params that work on every platform:

| Param | Description |
|-------|-------------|
| `name` | Entity name (required) |
| `budget` | `{ daily: N }` or `{ lifetime: N }` |
| `status` | `active` or `paused` (default: paused) |

Platform-specific params (targeting, optimization, bidding, pixel, channel) vary. Always discover them with `adkit_help` before your first mutation on a platform.

Create example (platform-agnostic pattern):
```
adkit_manage platform: "<platform>" entity: "campaigns" action: "create" params: { name: "Spring Sale", objective: "sales", budget: { daily: 50 } }
```
Then create the ad group referencing the campaign, then the ad referencing the ad group. Each returns a draft ID.

## 3. Media upload (all platforms)

Two upload methods:

**Direct upload** (default — handles most files):
```
adkit_manage platform: "<platform>" entity: "media" action: "upload" params: { source: "url", url: "<public-url>" }
```

**Temporary upload URL** (for local files or large assets):
1. `entity: "media" action: "request_upload_url"` with `filename` and `contentType` → returns a signed PUT URL and `uploadId`
2. PUT the file bytes to the signed URL
3. `entity: "media" action: "upload"` with `{ source: "temporary_upload", uploadId: "<id>" }`

Or use `adkit_studio` to generate AI creatives instead of uploading.

### Bulk media upload

For multiple creatives, repeat the upload flow for each file. Each upload returns a separate media ID. Then create one ad per media ID referencing the same ad group.

## 4. Review and publish

Call `entity: "drafts" action: "list"` — the response includes a review URL for each draft.

**Only after explicit user approval:** `entity: "drafts" action: "publish" ids: ["<draftId>"]`

## Rules

- All creates produce drafts. Never publish without explicit user approval.
- Drafts are editable via `entity: "drafts" action: "update"`.
- `ids` for publish/delete must be an array, even for one draft.
