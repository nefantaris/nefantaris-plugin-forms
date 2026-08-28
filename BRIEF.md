# nefantaris-plugin-forms

## Mission

Gives brochure sites the one dynamic thing they actually need — a contact form — without a server. `nefantaris-plugin-date-fns` already proves the dependency half of the plugin contract; this one is the template for every plugin that ships behaviour, and proves the half core declares but does not yet consume: a directive and a Pages Function reaching a build.

## v1 scope

- `::contact-form` directive rendering an accessible form component
- A Cloudflare Pages Function deployed with the site that receives submissions
- `src/notify`: a shoutrrr-inspired TypeScript library that fans submissions out based on notification URLs (e.g. `slack://...`, `discord://...`, generic webhook). Slack and Discord first; email supported but the docs should steer people toward chat notifications
- Configuration through the site's Nefantaris config (notification URLs stored as Cloudflare secrets, never in the repo)

## Non-goals (v1)

- Visual form builder (fields beyond a sensible contact-form preset can wait)
- Running actual shoutrrr (it is Go; Workers can't run it — we borrow its URL-scheme idea only)
- Storing submissions (delivery only)

## Open questions

- Spam protection: Cloudflare Turnstile fits the stack — required or optional?
- Email delivery mechanism when someone insists on email (provider API vs Workers-compatible SMTP service)
- How a plugin declares itself is settled: `plugin.json`, per [THEME-CONTRACT.md](../THEME-CONTRACT.md). What is open is how core _consumes_ `provides.directives` and `provides.functions` — how a plugin directive becomes reachable from markdown alongside the theme's own, and how `functions/` gets deployed with the site

## Layout

`plugin.json` (the manifest), `src/notify` (URL router + services), `src/directive` (form component), `functions/` (Pages Function template).
