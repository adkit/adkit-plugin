![Ads MCP - let your AI agents manage your ads across Google Ads, Meta Ads, TikTok Ads, LinkedIn Ads, Microsoft Ads, Reddit Ads, and X Ads](./assets/cover.png)

# Ads MCP - Manage your ads from your AI agent

[![GitHub stars](https://img.shields.io/github/stars/adkit/ads-mcp?style=flat&logo=github&color=f97316)](https://github.com/adkit/ads-mcp/stargazers) [![Latest release](https://img.shields.io/github/v/release/adkit/ads-mcp?color=f97316)](https://github.com/adkit/ads-mcp/releases) [![MCP Registry](https://img.shields.io/badge/MCP-Registry-f97316)](https://registry.modelcontextprotocol.io) [![License: MIT](https://img.shields.io/badge/License-MIT-green)](./LICENSE)

**Ads MCP** is a Model Context Protocol (MCP) server for managing ad campaigns across **Google Ads, Meta Ads, TikTok Ads, LinkedIn Ads, Microsoft Ads, Reddit Ads, and X Ads** from any MCP-compatible AI agent — Claude, Claude Code, ChatGPT, Cursor, and Codex. Create campaigns, analyze performance, and spy on competitor ads without leaving your chat. _(Pinterest and Snapchat coming soon.)_

> **Draft-first:** every change starts as a draft — nothing goes live without your explicit approval. Multi-account for agencies and teams.

## What it does

- 🚀 **Create campaigns** — Build campaigns from scratch with audience research, keyword targeting, and media uploads
- 📊 **Analyze performance** — Pull metrics with date, placement, and demographic breakdowns; diagnose why ROAS dropped
- 🕵️ **Spy on competitor ads** — Search real ad libraries to research strategies, creative formats, and landing pages
- 🎨 **Generate creatives** — Use AI to create ad images and copy from a brief
- 🔗 **Connect ad accounts** — Link multiple Google, Meta, TikTok, LinkedIn, Microsoft, Reddit, and X accounts in one workspace

## Platforms & tools

| Platform | What you can do |
| --- | --- |
| **Google Ads** | Search campaigns, keyword targeting, performance analysis, competitor ad spying |
| **Meta Ads** (Facebook + Instagram) | Campaign creation, audience targeting, performance breakdowns, competitor ad spying |
| **TikTok Ads** | Campaign creation and performance analysis |
| **LinkedIn Ads** | Campaign creation, performance analysis, competitor ad spying |
| **Microsoft Ads** (Bing) | Campaign creation and performance analysis |
| **Reddit Ads** | Campaign creation and performance analysis |
| **X Ads** | Campaign creation and performance analysis |
| **Pinterest Ads · Snapchat Ads** | _Coming soon_ |

## Tools

| Tool | What it does |
| --- | --- |
| `adkit_projects` | List your projects and pick one to work in |
| `adkit_status` | Show connected platforms and available ad accounts |
| `adkit_setup` | Get links to connect your ad platforms |
| `adkit_help` | Look up what each platform supports, with exact params |
| `adkit_manage` | Create, edit, and publish campaigns, ad sets, and ads. Pull spend, ROAS, and performance |
| `adkit_library` | Search 500k+ ads from 1,000+ advertisers on Meta, Google, and LinkedIn |
| `adkit_studio` | Generate ad images and copy from a brief |
| `adkit_upload_file` | Upload images and videos for your ads |
| `adkit_feedback` | Report bugs or missing features to the AdKit team |
| `adkit_checkin` | Confirm your setup worked during onboarding |

## Example prompts

- "How are my Google Ads doing this week? Which keywords spent money without converting?"
- "What ads is Notion running on Meta right now? Which ones have been live the longest?"
- "Pull last month's search terms, find the ones with spend but zero conversions, and add them as negative keywords."
- "Create a Meta campaign for our spring sale. $50/day, US only, use our three best images. Draft it, don't publish."
- "Take our top-performing ad and generate square and story-size variants."
- "Give me an overview of all my client accounts. Which ones need attention today?"
- "Build me an HTML dashboard of this month's performance across all my ad accounts."

## Install

### Claude Code (recommended)

```
/plugin marketplace add adkit/ads-mcp
/plugin install ads@adkit
```

Then run `/ads:setup` to connect your ad accounts.

**MCP-only (no plugin):**

```
claude mcp add --transport http adkit https://mcp.adkit.so
```

### Claude (desktop & web)

Settings → **Connectors** → **Add custom connector** → URL: `https://mcp.adkit.so` → sign in on first use.

### ChatGPT

Settings → **Connectors** → **Add custom connector** → URL: `https://mcp.adkit.so`

### Cursor

Add to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "adkit": {
      "url": "https://mcp.adkit.so"
    }
  }
}
```

### Codex

Add to `~/.codex/config.toml`:

```toml
[mcp_servers.adkit]
url = "https://mcp.adkit.so"
```

## Skills

| Skill           | Description                                  |
| --------------- | -------------------------------------------- |
| `/ads:setup`    | Connect your ad accounts                     |
| `/ads:launch`   | Create campaigns, ad sets, and ads           |
| `/ads:analyze`  | Pull performance data and metrics            |
| `/ads:spy`      | Research competitor ads across ad libraries  |
| `/ads:studio`   | Generate ad images and copy with AI          |

## How it works

The plugin connects to the AdKit MCP server, which manages your ad accounts across platforms. It follows a **draft-first workflow** — nothing publishes without your explicit approval. Supports multi-account setups for agencies and teams.

## Learn more

- [Google Ads MCP](https://adkit.so/features/ads-mcp/google) — connect Google Ads to your AI agent
- [Meta Ads MCP](https://adkit.so/features/ads-mcp/meta) — connect Facebook & Instagram Ads
- [TikTok Ads MCP](https://adkit.so/features/ads-mcp/tiktok) — connect TikTok Ads
- [LinkedIn Ads MCP](https://adkit.so/features/ads-mcp/linkedin) — connect LinkedIn Ads
- [Microsoft Ads MCP](https://adkit.so/features/ads-mcp/microsoft) — connect Microsoft (Bing) Ads
- [Reddit Ads MCP](https://adkit.so/features/ads-mcp/reddit) — connect Reddit Ads
- [X Ads MCP](https://adkit.so/features/ads-mcp/x) — connect X Ads
- [Claude integration](https://adkit.so/integrations/claude) — full setup guide for Claude
- [AdKit Dashboard](https://adkit.so) — account management and documentation

## Strategy skills

For campaign planning and platform-specific strategy, pair this plugin with the free [Ads Strategy Skills](https://github.com/adkit/ads-skills).

## Connect

[Website](https://adkit.so) · [X](https://x.com/TryAdkit) · [YouTube](https://www.youtube.com/@TryAdKit) · [LinkedIn](https://linkedin.com/company/adkit-ads) · [Facebook](https://www.facebook.com/TryAdkit)

## License

MIT
