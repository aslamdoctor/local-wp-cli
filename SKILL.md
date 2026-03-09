---
name: local-wp-cli
description: "Run WP-CLI commands against any Local by Flywheel site. Use when the user says 'wp-cli', 'run wp', 'use wp-cli', 'activate plugin', 'deactivate plugin', 'flush cache', 'wp option', 'wp transient', 'wp db', 'wp eval', 'wp cron', 'wp rewrite', or any request involving WordPress CLI commands."
---

# WP-CLI for Local by Flywheel

Run all WP-CLI commands using the wrapper script bundled with this skill:

```bash
bash {{SKILL_DIR}}/scripts/wp <site-name> <command>
```

**Never run bare `wp` commands.** Always use the full path above.

## Usage

The first argument is the **Local site name** (as shown in the Local app), followed by any WP-CLI command.

```bash
WP="bash {{SKILL_DIR}}/scripts/wp"

# Examples with different sites
$WP my-site plugin list
$WP my-site core version
$WP my-site user list
```

**If the user doesn't specify a site name, ask them which Local site to use.** You can run the script with no arguments to list available sites.

## Environment

- **OS**: macOS Apple Silicon
- **WP-CLI**: Global install (`/usr/local/bin/wp`)
- **Sites config**: `~/Library/Application Support/Local/sites.json`

## Requirements

- The target Local site **must be running** (started in the Local app)
- Site name must match exactly as shown in Local

## Common Commands

```bash
WP="bash {{SKILL_DIR}}/scripts/wp"
SITE="my-site"  # replace with actual site name

# Plugin management
$WP $SITE plugin list
$WP $SITE plugin activate <slug>
$WP $SITE plugin deactivate <slug>
$WP $SITE plugin status <slug>

# Cache / transients
$WP $SITE cache flush
$WP $SITE transient delete --all

# Options
$WP $SITE option get <key>
$WP $SITE option update <key> <value>
$WP $SITE option list --search="<pattern>"

# Database
$WP $SITE db query "SELECT * FROM wp_options WHERE option_name LIKE '<pattern>%' LIMIT 10;"
$WP $SITE db export backup.sql
$WP $SITE db import backup.sql

# Eval PHP
$WP $SITE eval 'echo get_option("siteurl");'
$WP $SITE eval-file script.php

# Rewrites / cron
$WP $SITE rewrite flush
$WP $SITE cron event list
$WP $SITE cron event run <hook>

# User / site info
$WP $SITE user list
$WP $SITE option get siteurl
$WP $SITE core version
```
