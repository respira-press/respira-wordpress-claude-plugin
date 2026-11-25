<p align="center">
  <img src="./assets/logo.png" alt="Respira for WordPress" width="160" />
</p>

# Respira for WordPress

Respira lets Claude edit a WordPress site the way a careful person would: in the site's own page builder, one element at a time, with a snapshot taken before every page and post write. Ask for a new headline, a testimonials section, an SEO pass or a move from Elementor to Bricks, and Claude does it through Respira's tools instead of pasting raw HTML into your pages.

> **Already use the Respira plugin for Cowork** (added from `respira-press/cowork-plugin-wordpress`, with its `connect-site` command and a setup code)? You do not need this one. That plugin keeps working as it is. This plugin is the version for Claude's plugin directory: it connects straight to your own site and starts nothing on your computer.
This plugin gives Claude the Respira skills, slash commands and a visual reviewer agent. In Claude Code it also connects Claude to your WordPress site, using the site address and the site key you enter once. It works with Gutenberg, Elementor, Divi 4 and Divi 5, Bricks, Oxygen Classic and Oxygen 6, Beaver Builder, Breakdance, Flatsome, Brizy, Visual Composer, WPBakery, Spectra, Kadence Blocks and GenerateBlocks, and it can audit SeedProd pages.

## What you can ask for

- **Edit a page.** "Change the homepage headline to 'spring collection arriving'." Claude finds the element, edits it in the builder's own format, and checks that the page still renders.
- **Add a section.** "Add a three-column testimonials section under the hero." Built from native modules of the page's builder.
- **Move between builders.** Migration skills cover the common paths, such as Elementor, Divi, WPBakery, Beaver Builder or Oxygen to Bricks, Breakdance or Gutenberg, section by section.
- **Audit a site.** SEO and AI search visibility, accessibility, mobile experience, technical debt, WooCommerce health and security, with fixes you can apply one by one.
- **Work across many sites.** Connect every client site once and refer to them by name in the same conversation.
- **Get a client's sign-off.** Make a review link a client opens without a WordPress login, then apply their comments on a draft.

## How it keeps your site safe

- Every page, post and layout write saves a snapshot first, and you can restore it. `/respira-wordpress:undo-last-change` restores the most recent snapshot. A deleted page, post or media item goes to the trash with a snapshot. Plugin installs and removals, WordPress core updates, user accounts and deleted menus and terms are not snapshotted, so your host's backup is the way back for those, and the destructive ones wait for your approval. The activity log records every action.
- On a published page, the edit lands on a draft duplicate, and a person approves it before it goes live, unless the site owner has turned on direct editing.
- Page content is written in the builder's own data format. Respira's rules tell Claude not to use raw SQL, direct database writes or theme PHP to change a page.
- After a page write Respira validates the rendered page and reports what it found. Claude is told never to claim a success the response does not show.

## Requirements

- A WordPress site where you can install plugins, with the **Respira for WordPress** plugin installed and activated.
- A Respira account at [respira.press](https://www.respira.press).
- A site key from your WordPress admin (**Respira, Settings, API Keys**), or, in Cowork and the Claude apps, a Respira sign-in.

## Connect a site

**Claude Code.** Install this plugin. Claude Code asks for your WordPress site address and a Respira site key, and connects straight to your own site at `<your site>/wp-json/respira/v1/mcp`. Nothing runs on your computer: the plugin starts no program and downloads no package. The key is saved in your system's credential store and sent only to your own site. For the short Focus list of tools, change the third setting to `wp-json/respira/v1/mcp/focus`. Run `/respira-wordpress:connect-site` for a guided walkthrough, including a second site.

**Cowork, claude.ai in the browser and the Claude apps.** These do not ask a plugin for settings, so the plugin brings the skills and commands, and you add your site once as a connector: in Claude, open **Settings, Connectors, Add custom connector**, paste the site link from your [Respira dashboard](https://www.respira.press/dashboard/mcp), sign in to Respira, then **Approve**. The skills and commands in this plugin then work with that connection. `/respira-wordpress:connect-site` walks through it.

## The commands

| Command | What it does |
|---|---|
| `/respira-wordpress:connect-site` | Connect a WordPress site for the first time. |
| `/respira-wordpress:edit-page` | Edit any page on a connected site. |
| `/respira-wordpress:add-section` | Add a new section to a page, such as a hero, testimonials or an FAQ. |
| `/respira-wordpress:duplicate-page` | Make a safe copy of a page to work on. |
| `/respira-wordpress:preview-changes` | Open a page in your browser to see what is on it. |
| `/respira-wordpress:audit-site` | Check accessibility, SEO or performance. |
| `/respira-wordpress:undo-last-change` | Restore the most recent page or post edit. |
| `/respira-wordpress:help` | Show the menu and where to get help. |

You can also ask in plain words. The commands are shortcuts.

## The skills

The skills load on their own when a conversation needs them. They cover safe editing and builder detection, page builds from HTML or Figma for each builder, builder-to-builder migrations, site audits (SEO and AI search, accessibility, mobile, technical debt, security, stale content, conversion), WooCommerce catalog, pricing and campaigns, design systems and art direction, brand voice, internal linking, activity reports, and client review loops. The same skills are published on their own at [respira-press/agent-skills-wordpress](https://github.com/respira-press/agent-skills-wordpress).

## Data and privacy

**What is sent to respira.press, in short.** When a skill opens it sends the skill name, the site address and the client name to `https://www.respira.press/api/skills/track-usage`, and your site's Respira plugin sends usage records for tool calls to `https://www.respira.press/mcp-spend/track`: the tool name, the site address, how long the call took and whether it worked. Nothing in these records is tool arguments, tool results, page content, prompts or the conversation. Skill run summaries are separate: each skill asks you once and sends one only after a yes.

Everything this plugin runs, sends or fetches:

- **Your WordPress site, from Claude Code.** `.mcp.json` points Claude Code at your own site's Respira address, built from the site address and path you enter. Claude Code sends your Respira site key in an `X-Respira-API-Key` header with each request. The plugin starts no local program and reads no key from your computer.
- **Your WordPress sites.** Each tool call goes to the WordPress site you are working on, over HTTPS, authenticated with that site's key. Page content travels between your site and Claude.
- **respira.press, for your site.** Your site's Respira plugin talks to respira.press for your account, for the rendered design check (it asks the render service to load a published page and take screenshots), for `respira_search_docs` (your search words go to `https://www.respira.press/docs-search`) and for `respira_report_issue` (the report you approve goes to `https://www.respira.press/mcp/report-issue`). Cowork, claude.ai and the apps sign in through `https://www.respira.press`.
- **respira.press, usage records.** Respira's usage records for tool calls are written by the Respira plugin on your WordPress site and by the skills below, not by anything on your computer. A skill that opens sends the skill name, the site address and the client name to `https://www.respira.press/api/skills/track-usage`. These feed the usage views in your Respira dashboard and never contain tool arguments or results, page content, prompts or the conversation. To switch off the site-side records, turn on **Opt out of usage reporting** under Respira, Settings in WordPress admin. The usage record's address is `https://www.respira.press/mcp-spend/track` and carries the tool name, the site address, how long the call took and whether it worked. Skill run summaries are separate: each skill asks you once and sends one only after a yes.
- **Skill run summaries.** Several skills end by asking Claude to send a short run summary to `POST https://www.respira.press/api/skills/track-usage`: the skill name, the site address, the WordPress and PHP versions, timings, whether it succeeded, which Respira tools it used, the AI client's name, and counts such as issues found by severity. No page content and no keys are included. Each skill asks you first and sends the summary only after a yes.
- **Nothing else.** The plugin has no hooks, runs no program on your computer, reads no environment variable or key file, and does not change Claude's permission settings.

The full policy is at [respira.press/privacy](https://www.respira.press/privacy) and the terms at [respira.press/terms](https://www.respira.press/terms).

## Support

- Help and questions: [respira.press/community](https://www.respira.press/community)
- Email: word@respira.press
- Documentation: [respira.press/docs](https://www.respira.press/docs)

Respira is built by Mihai Dragomirescu in Brașov, Romania.

## License

MIT. See [LICENSE](./LICENSE).
