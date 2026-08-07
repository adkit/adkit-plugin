---
name: setup
description: >
  Connect ad platforms to AdKit. Use when the user wants to set up AdKit,
  link their Meta, Google, or TikTok ad accounts, or verify their connection.
  Not for campaign creation, performance analysis, or ad library browsing — 
  use the launch or analyze skills for those.
---

# Setup

## Check Current Connection

Call `adkit_status` to see which platforms are connected and what ad accounts are available.

```
adkit_status
```

If all platforms are connected and ad accounts are visible, you're ready. If platforms are missing, continue.

## Link a Platform

If platforms are not connected, call `adkit_setup` with the target platform:

```
adkit_setup platform: "meta"
```

(Replace `"meta"` with `"google"` or `"tiktok"` as needed.)

The tool returns a browser URL. Share it with the user and ask them to open it and complete the OAuth authorization flow in their browser.

## Verify Connection

After the user confirms they've completed the authorization:

```
adkit_checkin agentId: "claude-code"
```

Then check the connection again:

```
adkit_status
```

You should now see the connected platform and its ad accounts listed. Setup is complete.
