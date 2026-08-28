# nefantaris-plugin-forms

Contact forms for Nefantaris sites, delivered via notification URLs. No server,
no stored submissions — a Cloudflare Pages Function receives the post and fans
it out to Slack, Discord, or a generic webhook.

This is also the reference plugin: it is what will prove the halves of the
Nefantaris plugin contract that core declares but does not yet consume —
directives and Pages Functions.

See [BRIEF.md](./BRIEF.md) for the mission and v1 scope, and
[THEME-CONTRACT.md](../THEME-CONTRACT.md) for the manifest spec.

## Manifest status

`plugin.json` is a **forward declaration**. Core validates it in full — the
name matches the directory, `contract` is `1`, and every path it names must
exist — but **contract v1 wires `provides.dependencies` only**. The
`contact-form` directive is not reachable from markdown yet, and `functions/`
is not deployed with a site yet. The manifest is written now so it cannot
drift from the plugin as the code lands, and so the wiring work in core has a
real target to build against.

`provides.directives["contact-form"]` points at `src/directive/index.ts`, which
is still a stub. No `provides.hooks` is declared, because there is no hooks
file to declare; it goes in when one exists. No `provides.dependencies` either
— the notification library has no npm dependencies.

## Commands

| Command             | Purpose                                             |
| ------------------- | --------------------------------------------------- |
| `npm run build`     | Compile to `dist/`                                  |
| `npm run typecheck` | Type-check without emitting                         |
| `npm run format`    | Format with Prettier (`format:check` to only check) |

## Layout

| Path            | What lives there                                       |
| --------------- | ------------------------------------------------------ |
| `plugin.json`   | The plugin manifest core reads                         |
| `src/notify`    | Notification-URL router and delivery services          |
| `src/directive` | The `::contact-form` component, named by the manifest  |
| `functions/`    | Cloudflare Pages Function template that receives posts |

## Configuration

Notification URLs are configured through the site's Nefantaris config and stored
as Cloudflare secrets — never committed to a site repo.

## License

MIT — see [LICENSE](./LICENSE).
