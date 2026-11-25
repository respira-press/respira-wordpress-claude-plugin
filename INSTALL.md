# Installing Respira for Claude

This guide installs the Respira plugin for Claude and connects your first WordPress site. The plugin brings Respira's skills, slash commands and a reviewer agent. It starts no program on your computer and needs no Node.js.

> **Already use the Respira plugin for Cowork** (added from `respira-press/cowork-plugin-wordpress`, with its `connect-site` command and a setup code)? You do not need this one. That plugin keeps working as it is. This plugin is the version for Claude's plugin directory: it connects straight to your own site and starts nothing on your computer.

## Before you start

You need:

- A WordPress site where you can install plugins, with the **Respira for WordPress** plugin installed and activated (download it from your dashboard at https://www.respira.press/dashboard).
- Claude Code, or Claude with plugins (Cowork, claude.ai, the desktop and mobile apps).

## Install the plugin

### Claude Code (terminal or VS Code)

Open `/plugin`, find **Respira for WordPress** in the directory and install it. Claude Code then asks for three settings:

1. **WordPress site address**, for example `https://example.com`, with no slash at the end.
2. **Respira site key.** In WordPress admin open **Respira, Settings, API Keys**, choose **Add New Key**, and copy the key. Claude Code keeps it in your system's credential store, not in a file, and sends it only to your own site.
3. **Respira address on the site.** Leave the default `wp-json/respira/v1/mcp` for every Respira tool. For the short Focus list of tools, use `wp-json/respira/v1/mcp/focus`.

Run `/mcp` to see the `respira-wordpress` entry connected, then ask Claude to list your pages. To change a setting later, open `/plugin`, pick Respira and choose its settings.

### Cowork, claude.ai and the Claude apps

Install the plugin from **Customize, Plugins, Discover** (the directory). These apps do not ask a plugin for settings, so the plugin brings the skills and commands, and you add your site once as a connector:

1. Open https://www.respira.press/dashboard/mcp, sign in, and choose **claude.ai** (or **Claude Desktop** for the desktop app). Copy the site link it shows.
2. In Claude, open **Settings, Connectors, Add custom connector**, paste the link, sign in to Respira and press **Approve**.
3. Start a new chat and ask "list my WordPress pages". Your real page titles coming back is the proof. The desktop app needs a full restart before a new connector appears.

Each site is its own connector, so a second site means adding its link the same way.

## A second site in Claude Code

The plugin connects one site. Add more with one command each, using the site's own address and key:

```
claude mcp add --transport http respira-second-site https://second-site.example/wp-json/respira/v1/mcp --header "X-Respira-API-Key: YOUR_SITE_KEY"
```

Replace `YOUR_SITE_KEY` with the key from that site's **Respira, Settings, API Keys**.

## What gets stored where

- Your site key is kept by Claude Code in your system's credential store. It is sent to your own WordPress site and nowhere else.
- The site address and path are saved in your Claude Code settings.
- The Respira plugin on your WordPress site stores nothing about you outside your own site.

## Staging site behind a password

If your browser asks for a username and password before WordPress loads, Respira's key cannot get past that prompt by itself. Ask whoever set the password (often your host) to let addresses starting with `/wp-json/respira/` through.

## Troubleshooting

### No Respira tools appear in Claude Code

1. Run `/mcp`. If `respira-wordpress` is missing, open `/plugin`, pick Respira and check that the site address and key are filled in.
2. If it shows as failed, open the address `https://your-site/wp-json/respira/v1/mcp` in a browser. A JSON answer or a short error from Respira means the site is reachable. A host login prompt, a firewall page or a 404 means the host is blocking it.
3. A site with plain permalinks has no `/wp-json/` path. Turn on pretty permalinks in WordPress (Settings, Permalinks).

### The key is refused

Create a new key under **Respira, Settings, API Keys** and paste it again. Keys are shown once, and an extra space at either end breaks them. Check that the Respira plugin is activated on the site.

### "Page builder not detected"

Run `/respira-wordpress:audit-site` and pick "all of the above". The audit reports which builder Respira detected on each page. Supported builders: Gutenberg, Elementor, Divi 4, Divi 5, Bricks, Oxygen Classic, Oxygen 6, Beaver Builder, Breakdance, Flatsome, Brizy, Visual Composer, WPBakery, Spectra, Kadence Blocks, GenerateBlocks, plus SeedProd audit-only. For another builder, email word@respira.press.

### Anything else

Email word@respira.press with what you tried and what you saw. The Respira founder reads every message.

## Uninstalling

In Claude Code run `/plugin` and remove Respira. In Cowork and the apps, remove it from **Customize, Plugins**, and remove the connector under **Settings, Connectors**. To remove Respira from your site, deactivate and delete the Respira plugin in WordPress admin. Nothing about your WordPress content changes when you uninstall.
