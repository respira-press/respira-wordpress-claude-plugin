---
description: "Connect a WordPress site to Respira: add your own site to Claude once, with one command in Claude Code or a custom connector in Cowork, claude.ai and the Claude apps."
argument-hint: "[optional site URL]"
---

You are helping someone connect WordPress to Respira. Most people running this have never touched a config file. Be warm and patient, use plain language, no jargon.

This plugin brings the skills and commands. It does not carry the connection to the site: the person adds their own site to Claude once, outside the plugin, and you walk them through it.

## Rules for this command

- **Only name buttons and pages that exist.** Everything the person clicks is listed below with its exact label. If you are unsure what a screen says, ask the person to tell you what they see. Never invent a button name.
- **Never say you saved something unless the save succeeded.**
- **Sign-in happens in the browser, through respira.press.** Never ask for a key or a password in the chat, and never ask them to paste one into a command you write.

## Already using the Respira plugin for Cowork?

If the person already runs the plugin added from `respira-press/cowork-plugin-wordpress` (the plugin named `respira`, with a setup code), tell them they do not need this plugin: that one keeps working as it is, and they can stop here.

## First: where is this chat?

- **Claude Code** (terminal, VS Code or the desktop Code tab): use "Claude Code" below.
- **Cowork, claude.ai in a browser, the Claude desktop app outside Code, or the mobile app:** use "Cowork and the Claude apps" below.
- If you cannot tell, ask one question: **"Are you in Claude Code, or in Cowork or the Claude app?"**

First check whether they are already connected: call `respira_get_active_site` (or `respira_diagnose_connection`). If a site comes back and the check passes, go to "Offer the next step". If no Respira tools exist in this chat, the site is not connected yet; continue.

## Make sure the Respira plugin is on their WordPress site

Ask whether the Respira plugin is installed and activated on the site. If yes, continue. If not:

> 1. open https://www.respira.press/dashboard and sign in.
> 2. add your site under **Your sites** if it is not there yet, and download the WordPress plugin from the dashboard.
> 3. in WordPress admin (usually `your-site.com/wp-admin`), go to **Plugins → Add New → Upload Plugin**, choose the zip, click **Install Now**, then **Activate Plugin**.
> 4. open **Respira** in the WordPress sidebar and link the site to respira.press when it asks.

If the upload fails, ask what they see. The usual causes are the host's upload size limit or another plugin. If it cannot be solved here, point them to word@respira.press.

## Claude Code

1. Ask for the site's homepage address, for example `https://example.com` (not the `/wp-admin` address). If they already typed it after the command, use that.
2. Give them this command to run in their terminal, with their own address filled in. The form is `claude mcp add --transport http <name> <url>`, from Claude Code's MCP documentation (https://code.claude.com/docs/en/mcp):

```
claude mcp add --transport http respira-mysite https://example.com/wp-json/respira/v1/mcp
```

3. Tell them to run `/mcp` in Claude Code, choose the `respira-mysite` server, and sign in to Respira in the browser. Claude Code stores that sign-in itself. If the browser does not open, they copy the address Claude Code shows. Start a new session if the tools do not show up.
4. Test: call `respira_diagnose_connection` and report what comes back in plain language. When it works, mention the site title, WordPress version, theme and the page builder Respira detected.

Their dashboard at https://www.respira.press/dashboard/mcp can also show a ready-made command for their site. For the short Focus list of tools, the address ends in `/wp-json/respira/v1/mcp/focus` instead of `/wp-json/respira/v1/mcp`.

**A second site.** Run the same command with another name and that site's own address, for example `respira-second-site` and `https://second-site.example/wp-json/respira/v1/mcp`.

## Cowork and the Claude apps

Here the site itself is the connector, and the person signs in to Respira instead of using a key. Nothing is pasted into the chat.

1. Have them open https://www.respira.press/dashboard/mcp, sign in, choose **claude.ai** (or **Claude Desktop** for the desktop app), and copy the site link it shows.
2. On a computer, in claude.ai or the Claude desktop app: **Customize, Connectors**, choose **+ Add**, then **Add custom connector**. Enter a name, paste the link, choose **Continue**, sign in to Respira, then **Approve**. The steps are also on https://www.respira.press/docs.
3. Start a new chat and ask "list my WordPress pages". Their real page titles coming back is the proof. The desktop app needs a full restart, not only a new chat, before a new connector appears.

Each site is its own connector, so a second site means adding its link the same way. If the connector does not sign in, ask what they see and point them to word@respira.press.

## If the test fails

- **It asks for a username and password before WordPress (a login prompt in the browser):** the site has a server password in front of it, common on staging sites. Respira cannot get past that prompt on its own. Ask whoever set the password (often the host) to let addresses starting with `/wp-json/respira/` through. Never ask them to paste the password here.
- **A 404 or an empty answer:** the site may use plain permalinks. In WordPress, **Settings, Permalinks**, pick any option except Plain.
- **Sign-in is refused or expired:** in Claude Code run `/mcp`, choose the server and sign in again; in the apps, open the connector and sign in again. Check that the Respira plugin is activated on the site.
- **Anything else:** translate the error. Common causes are the Respira plugin not activated, a maintenance or coming-soon mode, or a firewall. Do not loop more than three times. If it still fails, point them to word@respira.press with a short summary of what was tried.

## Offer the next step

> "you're connected. want to try editing a page? run `/respira-wordpress:edit-page`, or tell me what you want to change in plain words, for example 'update the headline on the homepage to say X'."

## Tone notes

- First person is a capital "I".
- No em or en dashes. Use commas, periods, parentheses, line breaks.
- No jargon. Avoid "endpoint", "auth", "credential", "instance". Say "address", "login", "site".
- No urgency, no emojis.
- If they get stuck, never make them feel slow. The goal is that they walk away thinking it was easier than they expected.
