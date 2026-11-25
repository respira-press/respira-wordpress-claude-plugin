---
name: respira-setup-assistant
description: "Use when the user says 'set up respira', 'respira not connecting', 'check my respira connection', or 'fix respira'. Walks through first-time setup of the Respira connection in Claude and diagnoses failures: timeouts, 401s, 403s, and plugin version mismatches."
license: MIT
metadata:
  author: Respira for WordPress
  author_url: https://respira.press
  version: 1.3.0
  mcp-server: respira-wordpress
  category: onboarding
---

> **Before anything else:** this needs a connected Respira site. If no Respira tools (names that start with `respira_`) are available in this chat, the site is not connected yet: say so in one plain sentence, tell the person to run `/respira-wordpress:connect-site` (it adds their site once), and stop. Do not guess, do not invent a result, and do not carry on as if the tools had answered.

# Respira Setup Assistant

Diagnose the Respira connection, walk through first-time setup and fix the common connection problems. This is the Claude plugin's own version: the plugin brings skills and commands only, and the person adds their own WordPress site to Claude once, so there is no local server to install or update.

## Trigger phrases

"set up respira", "connect respira", "respira not working", "respira connection failed", "fix respira", "check my respira connection", "is respira connected", "respira not connecting", "help me set up respira".

Do not trigger for general WordPress tasks, or for requests that assume Respira already works.

## Step 1: check what is there

1. Call `respira_diagnose_connection`. If it answers with a site, the connection works: report the site title, WordPress version and the page builder, and stop.
2. If no Respira tools exist in this chat, the connection is not set up. Tell the person to run `/respira-wordpress:connect-site`, which covers both ways to add their site (one `claude mcp add` command in Claude Code, or a custom connector in Cowork and the Claude apps).
3. If the tools exist but a call fails, use the table below.

## Step 2: read the error

| What you see | Cause and fix |
|---|---|
| 401 or "sign-in expired" | The sign-in to Respira ran out or was replaced. In Claude Code run `/mcp`, choose the Respira server and sign in again; in Cowork and the apps open the connector and sign in again. |
| 401 with a Basic challenge | The site has a server password in front of it (common on staging, shown as a login prompt). Ask the host to let addresses starting with `/wp-json/respira/` through. Never ask for the password in the chat. |
| 403 | A firewall or security plugin blocks the request. Allow `/wp-json/respira/` in it, or ask the host. |
| 404 or an empty answer | The site uses plain permalinks, or the address has a path in it. In WordPress, Settings, Permalinks: pick any option except Plain. The site address must be the homepage address, not `/wp-admin`. |
| Timeout | The host cut the call short. Retry once. If a call that edits a page timed out, read the page back before trying again. |
| "plugin not active" | In WordPress admin, Plugins: activate Respira for WordPress. |

## Step 3: version check

Call `respira_get_server_compatibility`. If it says the Respira plugin on the site is older than the tools need, give this instruction: in WordPress admin go to Dashboard, Updates (or Respira, Settings, Updates), update Respira for WordPress, then ask again.

## Report

End with one plain sentence on what works now and the one next step, if any. If it still fails after three tries, point to word@respira.press with a short summary of what was tried.
