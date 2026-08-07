---
name: studio
description: >
  Generate AI ad creatives — images, copy, and briefs. Use when the user wants
  to generate ad images, create ad creatives with AI, make an ad, build a
  creative brief, clone a competitor ad, resize creatives for different placements,
  or edit existing images. Also use when the user mentions "AI ad generation",
  "ad creative", or "make me an ad". Not for launching campaigns, pulling
  performance data, or browsing competitor ads.
---

# Studio — AI Creative Generation

Requires AdKit to be connected — run `/ads:setup` first if needed.

## 1. Generate images

Use `adkit_studio` with `entity: "ads"` and `action: "generate"`. Omit `id` to auto-create an ad, or pass an ad ID to add variants.

```
adkit_studio entity: "ads" action: "generate" params: { mode: "create", aspectRatio: "1:1", instructions: "Minimal SaaS hero image, dark background" }
```

### Generate params

| Param | Description |
|-------|-------------|
| `mode` | `create`, `clone`, `resize`, `edit` (default: create) |
| `aspectRatio` | `1:1`, `16:9`, `9:16` (required) |
| `instructions` | Generation prompt |
| `audience` | Target audience context |
| `quantity` | 1-10 (default: 1) |
| `model` | AI model (auto-detected from project config) |
| `quality` | Model-specific quality setting |
| `colors` | Hex color array, e.g. `["#FF5733"]` |
| `references` | Array for clone/edit/resize (see below) |
| `title` | Used when auto-creating ad |

### Clone from library

Clone a proven competitor ad discovered via `adkit_library`:
```
adkit_studio entity: "ads" action: "generate" params: { mode: "clone", aspectRatio: "1:1", references: [{ type: "library-ad", id: "<adId>" }] }
```

### Reference types

| Type | Use case |
|------|----------|
| `library-ad` | Clone/edit from a library ad by ID |
| `media` | Reference a previously generated studio media item |
| `temporary_upload` | User's own file (get uploadId via `action: "request_upload_url"` first) |

Clone, edit, and resize each require exactly one reference.

## 2. Create a brief (optional)

```
adkit_studio entity: "ads" action: "create" params: { title: "Spring Sale Ad", specs: { format: "image", targetAudience: "SaaS founders" }, content: { headline: "20% Off", copy: "Start your free trial today" } }
```

## 3. Upload user files

Call `entity: "media" action: "request_upload_url"` with `filename` and `contentType`, PUT file bytes to the returned URL, then pass `{ type: "temporary_upload", id: "<uploadId>" }` in generate references.

## 4. Use in campaigns

Studio media can be used in campaign creation via the launch skill. Studio ads are creative drafts, not launched ads.
