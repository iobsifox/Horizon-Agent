# Horizon Ticket System — downloads

Support tickets for WordPress and WooCommerce, with a companion portal theme and
native agent apps for the desktop and Android.

**This repository holds the downloads only.** The source lives in a private
repository; every release here is built from a tagged commit by a GitHub Actions
workflow, so what you download is what was tested, not something assembled by
hand.

## What you need

| | |
| --- | --- |
| WordPress | 6.4 or newer |
| PHP | 8.0 or newer (8.2+ recommended) |
| WooCommerce | 7.0 or newer — optional; the order context and the automatic tickets from failed payments, held orders and refunds need it, the rest does not |
| MySQL / MariaDB | 5.7 / 10.4 or newer |

## Downloads

Every release carries the same set of files:

| File | What it is |
| --- | --- |
| `horizon-ticket-system-<version>.zip` | **The plugin.** Install it, then activate it — it creates its own tables on activation. |
| `horizon-support-<version>.zip` | **The portal theme.** Optional but recommended: it is what renders the customer-facing support pages. |
| `horizon-agent-<version>-linux-x64.zip` | The **Linux** agent app. |
| `horizon-agent-<version>-windows-x64.zip` | The **Windows** agent app. |
| `horizon-agent-<version>-macos.zip` | The **macOS** agent app. |
| `horizon-agent-<version>-android.apk` | The **Android** agent app. Sideload it; it is not on the Play Store. |
| `SHA256SUMS.txt` | Checksums for everything above. |

## Installing the plugin and the theme

1. Download `horizon-ticket-system-<version>.zip` and `horizon-support-<version>.zip`.
2. In wp-admin, go to **Plugins → Add New → Upload Plugin**, choose the plugin
   zip, install, then activate.
3. Go to **Appearance → Themes → Add New → Upload Theme**, choose the theme zip,
   install, then activate.
4. Open **Horizon Tickets → Settings** and work through the tabs. Only the
   *General* tab needs attention to get going: your support address and the page
   that holds the portal.
5. Put `[horizon_ts_ticket_form]` on a page — that is the customer's way in.
   The rest of the shortcodes are listed under **Horizon Tickets → Help**.

Activating the plugin creates 22 tables, a read-only `hts_ticket` post type that
mirrors each ticket so it is searchable and linkable, three roles
(`hts_agent`, `hts_supervisor`, plus capabilities on `administrator`), four SLA
policies, eight email templates, four canned responses and about forty settings
with sensible defaults. Deactivating leaves your data where it is; deleting the
plugin through wp-admin asks before it removes anything.

## Installing an agent app

The apps talk to your site over its REST API — they are not a hosted service, and
nothing leaves your server.

- **Windows / Linux**: unzip and run the executable. On Linux, `chmod +x` it
  first.
- **macOS**: unzip, then open the `.app`. The build is unsigned, so Gatekeeper
  will complain the first time — right-click → Open, or
  `xattr -dr com.apple.quarantine "Horizon Agent.app"`.
- **Android**: enable installing from unknown sources for your file manager and
  open the `.apk`.

On first launch, enter your site URL and sign in with a WordPress account that
has agent or supervisor capabilities, or turn the app's **Agent account** setting
on to mint a dedicated one.

## Verifying a download

```bash
sha256sum -c SHA256SUMS.txt        # GNU coreutils
shasum -a 256 -c SHA256SUMS.txt    # macOS
```

## Language

The interface is English by default, and the Persian translation is complete —
including right-to-left layout — in the plugin, the theme and the agent app. It
follows the site language, and the app can be pinned to either language
independently of the site.

## Support and licensing

Everything published here is under the **GNU General Public License v2.0 or
later**, the same licence WordPress itself uses; the full text ships inside each
archive.

The source is private, so there is no issue tracker to file against — but the
repository's release notes for each version list what changed, and the checksums
let you confirm a file arrived intact.
