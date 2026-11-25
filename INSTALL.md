# Installing Respira for Claude

This guide installs the Respira plugin for Claude and then connects your first WordPress site. The plugin brings Respira's skills, slash commands and a reviewer agent. It starts no program on your computer and needs no Node.js. It does not connect to your site by itself: you add your own site to Claude once, in step 2, because every Respira site has its own address.

> **Already use the Respira plugin for Cowork** (added from `respira-press/cowork-plugin-wordpress`, with its `connect-site` command and a setup code)? You do not need this one. That plugin keeps working as it is. This plugin is the version for Claude's plugin directory: skills and commands only.

## Before you start

You need:

- A WordPress site where you can install plugins, with the **Respira for WordPress** plugin installed and activated (download it from your dashboard at https://www.respira.press/dashboard).
- Claude Code, or Claude with plugins (Cowork, claude.ai, the desktop and mobile apps).

## 1. Install the plugin

### Claude Code (terminal or VS Code)

Open `/plugin`, find **Respira for WordPress** in the directory and install it. It asks for no setting.

### Cowork, claude.ai and the Claude apps

Install the plugin from **Customize, Plugins, Discover** (the directory).

## 2. Add your site, once

Run `/respira-wordpress:connect-site` for a guided walkthrough, or follow the steps for your app.

### Claude Code

In a terminal, run this with your own site address (the form is `claude mcp add --transport http <name> <url>`, from https://code.claude.com/docs/en/mcp):

```
claude mcp add --transport http respira-mysite https://example.com/wp-json/respira/v1/mcp
```

Then run `/mcp` in Claude Code, choose the `respira-mysite` server and sign in to Respira in your browser. Ask Claude to list your pages: your real page titles coming back is the proof.

Your dashboard at https://www.respira.press/dashboard/mcp can also show a ready-made command for your site. For the short Focus list of tools, use `https://example.com/wp-json/respira/v1/mcp/focus` as the address instead.

A second site is one more command with a different name and that site's own address, for example `respira-second-site` and `https://second-site.example/wp-json/respira/v1/mcp`.

### Cowork, claude.ai and the Claude apps

1. Open https://www.respira.press/dashboard/mcp, sign in, and choose **claude.ai** (or **Claude Desktop** for the desktop app). Copy the site link it shows.
2. In Claude, open **Customize, Connectors**, choose **+ Add**, then **Add custom connector**. Enter a name, paste the link, choose **Continue**, sign in to Respira and press **Approve**.
3. Start a new chat and ask "list my WordPress pages". Your real page titles coming back is the proof. The desktop app needs a full restart before a new connector appears.

Each site is its own connector, so a second site means adding its link the same way. The steps are also described at https://www.respira.press/docs.

## What gets stored where

- The plugin stores nothing and asks for nothing. It holds no address and no key.
- Claude keeps the connection you added in step 2, and Respira's sign-in stays between your browser, Claude and respira.press.
- The Respira plugin on your WordPress site stores nothing about you outside your own site.

## Staging site behind a password

If your browser asks for a username and password before WordPress loads, Respira cannot get past that prompt by itself. Ask whoever set the password (often your host) to let addresses starting with `/wp-json/respira/` through.

## Troubleshooting

### The skills say the site is not connected

No Respira tools are available in this chat yet. Do step 2, then start a new chat (in Claude Code, run `/mcp` to see the server listed).

### No Respira tools appear in Claude Code

1. Run `/mcp`. If your server is missing, run the `claude mcp add` command again. If it shows as needing sign-in, choose it and sign in.
2. If it shows as failed, open the address `https://your-site/wp-json/respira/v1/mcp` in a browser. A JSON answer or a short error from Respira means the site is reachable. A host login prompt, a firewall page or a 404 means the host is blocking it.
3. A site with plain permalinks has no `/wp-json/` path. Turn on pretty permalinks in WordPress (Settings, Permalinks).

### "Page builder not detected"

Run `/respira-wordpress:audit-site` and pick "all of the above". The audit reports which builder Respira detected on each page. Supported builders: Gutenberg, Elementor, Divi 4, Divi 5, Bricks, Oxygen Classic, Oxygen 6, Beaver Builder, Breakdance, Flatsome, Brizy, Visual Composer, WPBakery, Spectra, Kadence Blocks, GenerateBlocks, plus SeedProd audit-only. For another builder, email word@respira.press.

### Anything else

Email word@respira.press with what you tried and what you saw. The Respira founder reads every message.

## Uninstalling

In Claude Code run `/plugin` and remove Respira, and run `claude mcp remove respira-mysite` to remove the site you added. In Cowork and the apps, remove the plugin from **Customize, Plugins**, and the connector under **Customize, Connectors**. To remove Respira from your site, deactivate and delete the Respira plugin in WordPress admin. Nothing about your WordPress content changes when you uninstall.
