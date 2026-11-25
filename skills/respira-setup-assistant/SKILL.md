---
name: "respira-setup-assistant"
description: "Use when the user says 'check my respira setup', 'is respira working', 'respira not working', or 'fix respira'. Checks whether the Respira tools are available in the conversation and diagnoses failures: timeouts, 401s, 403s, and plugin version mismatches."
license: "MIT"
metadata:
  author: "Respira for WordPress"
  author_url: "https://respira.press"
  version: "1.4.0"
  category: "onboarding"
---

> **Before anything else:** this needs the Respira tools. If no Respira tools (names that start with `respira_`) are available in this conversation, say so in one plain sentence: the Respira tools are not available here and this plugin does not add them. Then stop. Do not guess, do not invent a result, and do not carry on as if the tools had answered.

# Respira Setup Assistant

Check whether the Respira tools are available in this conversation and, when they are, diagnose the common failures. This is the Claude plugin's own version: the plugin is plain instructions. It adds no tools, connects to nothing and sends nothing.

## Trigger phrases

"check my respira setup", "is respira working", "respira not working", "respira call failed", "fix respira", "is respira available".

Do not trigger for general WordPress tasks, or for requests that assume Respira already works.

## Step 1: check what is there

1. Look for Respira tools (names that start with `respira_`) in this conversation. Call `respira_diagnose_connection`. If it answers with a site, the tools work: report the site title, WordPress version and the page builder, and stop.
2. If no Respira tools exist in this conversation, say this in plain words and stop:

   "The Respira tools are not available here. This plugin does not add them. Respira for WordPress is at https://www.respira.press."

   Do not guess, do not invent a result, and do not walk the person through any other setup.
3. If the tools exist but a call fails, use the table below.

## Step 2: read the error

| What you see | Cause and fix |
|---|---|
| 401 or "sign-in expired" | The sign-in to Respira ran out or was replaced. Ask the person to sign in to Respira again from the place they use the tools, then try again. |
| 401 with a Basic challenge | The site has a server password in front of it (common on staging, shown as a login prompt). Ask the host to let addresses starting with `/wp-json/respira/` through. Never ask for the password in the chat. |
| 403 | A firewall or security plugin blocks the request. Allow `/wp-json/respira/` in it, or ask the host. |
| 404 or an empty answer | The site uses plain permalinks. In WordPress, Settings, Permalinks: pick any option except Plain. |
| Timeout | The host cut the call short. Retry once. If a call that edits a page timed out, read the page back before trying again. |
| "plugin not active" | In WordPress admin, Plugins: activate Respira for WordPress. |

## Step 3: version check

Call `respira_get_server_compatibility`. If it says the Respira plugin on the site is older than the tools need, give this instruction: in WordPress admin go to Dashboard, Updates (or Respira, Settings, Updates), update Respira for WordPress, then ask again.

## Report

End with one plain sentence on what works now and the one next step, if any. If it still fails after three tries, point to word@respira.press with a short summary of what was tried.
