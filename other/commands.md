---
description: >-
  Commands offer additional functionality like providing debug information and
  performing maintenance tasks.
---

# Commands

Commands are intended to be run from within the CLI of the container and from the application's root directory.

* In my build the root directory is located at: `/var/www/html`
* In LinuxServer's build the root directory is located at: `/app/www`

### Core commands

Core commands exist at the framework level and might be extended to provide additional functionality.

<table><thead><tr><th width="261">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>about</code></td><td>Provides information on the current version of Speedtest Tracker, Laravel and Filament.</td></tr></tbody></table>

### Application commands

Application commands are built to extend Speedtest Tracker's functionality from the CLI.

<table><thead><tr><th width="261">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>app:install</code></td><td>Installs a fresh version of Speedtest Tracker. If you have an existing install <em><strong>this will delete all data</strong></em>.</td></tr><tr><td><code>app:reset-user-password</code></td><td>Can be used to reset a user's password.</td></tr><tr><td><code>app:update-user-role</code></td><td>Can be used to change a user's role.</td></tr></tbody></table>

### Maintenance commands

Maintenance commands help fix issues that might crop up over time.

<table><thead><tr><th width="261">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>app:fix-result-statuses</code></td><td>Reviews the data payload of each result and corrects the status attribute based on Ookla's CLI response.</td></tr></tbody></table>
