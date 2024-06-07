---
description: >-
  Commands offer additional functionality like providing debug information and
  performing maintenance tasks.
---

# Commands

Commands are intended to be run from within the CLI of the container and from the application's root directory. The application directory is located at: `/app/www`

When using the commands below they should be prefixed with `php artisan`, so the `about` command will look like `php artisan about`.

### Core commands

Core commands exist at the framework level and might be extended to provide additional functionality.

<table><thead><tr><th width="261">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>about</code></td><td>Provides information on the current version of Speedtest Tracker, Laravel and Filament.</td></tr></tbody></table>

### Application commands

Application commands are built to extend Speedtest Tracker's functionality from the CLI.

<table><thead><tr><th width="261">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>app:install</code></td><td>Installs a fresh version of Speedtest Tracker. If you have an existing install <em><strong>this will delete all data</strong></em>.</td></tr><tr><td><code>app:ookla-list-servers</code></td><td>Get a list of local Ookla speedtest servers.</td></tr><tr><td><code>app:user-change-role</code></td><td>Change the role for a user.</td></tr><tr><td><code>app:user-reset-password</code></td><td>Change the password for a user.</td></tr><tr><td><code>app:version</code></td><td>Sends a notification to the admin users when Speedtest Tracker is outdated.</td></tr></tbody></table>

### Maintenance commands

Maintenance commands help fix issues that might crop up over time.

<table><thead><tr><th width="261">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>app:result-fix-statuses</code></td><td>Reviews the data payload of each result and corrects the status attribute.</td></tr></tbody></table>
