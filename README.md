# Respira for WordPress

Respira lets Claude edit a WordPress site the way a careful person would: in the site's own page builder, one element at a time, with a snapshot taken before every page and post write. Ask for a new headline, a testimonials section, an SEO pass or a move from Elementor to Bricks, and Claude does it through Respira's tools instead of pasting raw HTML into your pages.

## What this plugin is

Skills, commands and one reviewer agent, all plain text. They tell Claude how to do Respira work well. The plugin runs nothing, connects to nothing and sends nothing by itself. It works with Gutenberg, Elementor, Divi 4 and Divi 5, Bricks, Oxygen Classic and Oxygen 6, Beaver Builder, Breakdance, Flatsome, Brizy, Visual Composer, WPBakery, Spectra, Kadence Blocks and GenerateBlocks, and it can audit SeedProd pages.

## What it needs

A WordPress site with the Respira for WordPress plugin, and the Respira tools present in the conversation. Without them the skills stop and say so.

Respira for WordPress: https://www.respira.press

## What you can ask for

- **Edit a page.** "Change the homepage headline to 'spring collection arriving'." Claude finds the element, edits it in the builder's own format, and checks that the page still renders.
- **Add a section.** "Add a three-column testimonials section under the hero." Built from native modules of the page's builder.
- **Move between builders.** Migration skills cover the common paths, such as Elementor, Divi, WPBakery, Beaver Builder or Oxygen to Bricks, Breakdance or Gutenberg, section by section.
- **Audit a site.** SEO and AI search visibility, accessibility, mobile experience, technical debt, WooCommerce health and security, with fixes you can apply one by one.
- **Work across many sites.** When the Respira tools cover more than one site, refer to them by name in the same conversation.
- **Get a client's sign-off.** Make a review link a client opens without a WordPress login, then apply their comments on a draft.

## How it keeps your site safe

- Every page, post and layout write saves a snapshot first, and you can restore it. `/respira-wordpress:undo-last-change` restores the most recent snapshot. A deleted page, post or media item goes to the trash with a snapshot. Plugin installs and removals, WordPress core updates, user accounts and deleted menus and terms are not snapshotted, so your host's backup is the way back for those, and the destructive ones wait for your approval. The activity log records every action.
- On a published page, the edit lands on a draft duplicate, and a person approves it before it goes live, unless the site owner has turned on direct editing.
- Page content is written in the builder's own data format. Respira's rules tell Claude not to use raw SQL, direct database writes or theme PHP to change a page.
- After a page write Respira validates the rendered page and reports what it found. Claude is told never to claim a success the response does not show.

## The commands

| Command | What it does |
|---|---|
| `/respira-wordpress:edit-page` | Edit any page on your site. |
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

The plugin itself sends no data. It has no server, holds no address and no key, runs no program on your computer and reads no environment variable or key file. It does not change Claude's permission settings.

The Respira tools, when they are present in your conversation, run on your own WordPress site and are covered by Respira's privacy policy. The full policy is at [respira.press/privacy](https://www.respira.press/privacy) and the terms at [respira.press/terms](https://www.respira.press/terms).

## Support

- Help and questions: [respira.press/community](https://www.respira.press/community)
- Email: word@respira.press
- Documentation: [respira.press/docs](https://www.respira.press/docs)

Respira is built by Mihai Dragomirescu in Brașov, Romania.

## License

MIT. See [LICENSE](./LICENSE).
