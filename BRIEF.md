# nefantaris-plugin-forms

## Mission

The first plugin, and the template for all future ones. Gives brochure sites the one dynamic thing they actually need — a contact form — without a server, and proves the plugin contract (directive + build hook + Pages Function) end to end.

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
- Exactly how a plugin declares its function so nefantaris-core deploys it — this decision becomes the plugin spec

## Layout

`src/notify` (URL router + services), `src/directive` (form component + registration), `functions/` (Pages Function template).
