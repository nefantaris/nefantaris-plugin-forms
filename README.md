# nefantaris-plugin-forms

Contact forms for Nefantaris sites, delivered via notification URLs. No server,
no stored submissions — a Cloudflare Pages Function receives the post and fans
it out to Slack, Discord, or a generic webhook.

This is also the reference plugin: it proves the Nefantaris plugin contract
(directive + build hook + Pages Function) end to end.

See [BRIEF.md](./BRIEF.md) for the mission and v1 scope.

## Commands

| Command             | Purpose                                             |
| ------------------- | --------------------------------------------------- |
| `npm run build`     | Compile to `dist/`                                  |
| `npm run typecheck` | Type-check without emitting                         |
| `npm run format`    | Format with Prettier (`format:check` to only check) |

## Layout

| Path            | What lives there                                       |
| --------------- | ------------------------------------------------------ |
| `src/notify`    | Notification-URL router and delivery services          |
| `src/directive` | The `::contact-form` component and its registration    |
| `functions/`    | Cloudflare Pages Function template that receives posts |

## Configuration

Notification URLs are configured through the site's Nefantaris config and stored
as Cloudflare secrets — never committed to a site repo.

## License

MIT — see [LICENSE](./LICENSE).
