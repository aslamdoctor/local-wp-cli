# local-wp-cli

A [Claude Code skill](https://docs.anthropic.com/en/docs/claude-code/skills) that lets you run WP-CLI commands against any [Local by Flywheel](https://localwp.com/) site directly from Claude Code.

## Installation

```bash
claude skill install local-wp-cli
```

Or add to your project's `.claude/skills.json`:

```json
{
  "skills": ["local-wp-cli"]
}
```

## Prerequisites

- **macOS** (Apple Silicon or Intel)
- [Local by Flywheel](https://localwp.com/) installed
- [WP-CLI](https://wp-cli.org/) installed globally (`/usr/local/bin/wp`)
- The target Local site must be **running** (started in the Local app)

## Usage

Once installed, just ask Claude Code to run WP-CLI commands against your Local sites:

- "List all plugins on my-site"
- "Activate the woocommerce plugin on my-site"
- "Flush the cache on my-site"
- "Run a database query on my-site"
- "Export the database from my-site"

If you don't specify a site name, Claude will ask which Local site to target.

## Examples

```
> wp-cli list plugins on my-site
> activate plugin woocommerce on my-site
> flush cache on my-site
> wp option get siteurl on my-site
> wp db query "SELECT * FROM wp_options LIMIT 10;" on my-site
```

## How It Works

The skill includes a wrapper script (`scripts/wp`) that:

1. Reads your Local by Flywheel `sites.json` to find the site configuration
2. Locates the correct PHP and MySQL binaries for the site's configured versions
3. Uses the site-specific `php.ini` (which contains the MySQL socket path) to run WP-CLI with a proper database connection

This avoids the common "Error establishing a database connection" issue when running `wp` directly against Local sites.

## Supported Commands

All standard WP-CLI commands are supported, including:

- **Plugin management** - `plugin list`, `plugin activate`, `plugin deactivate`
- **Cache/transients** - `cache flush`, `transient delete --all`
- **Options** - `option get`, `option update`, `option list`
- **Database** - `db query`, `db export`, `db import`
- **PHP eval** - `eval`, `eval-file`
- **Rewrites/cron** - `rewrite flush`, `cron event list`
- **Users/site info** - `user list`, `core version`

## License

MIT
