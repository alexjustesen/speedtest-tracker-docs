---
description: >-
  A complete inventory of all environment variables for configuring Speedtest
  Tracker.
---

# Environment Variables

### Application

<table><thead><tr><th width="225">Name</th><th>Description</th></tr></thead><tbody><tr><td><code>PUID</code><br><br>(required)</td><td>Used to set the user the container should run as.<br><br>- Default:<code>1000</code></td></tr><tr><td><code>PGID</code><br><br>(required)</td><td>Used to set the group the container should run as.<br><br>- Default:<code>1000</code></td></tr><tr><td><code>APP_NAME</code></td><td>Used to define the application's name in the dashboard and in notifications.<br></td></tr><tr><td><code>APP_KEY</code><br><br>(required)</td><td><p>Key used to encrypt and decrypt data. </p><p></p><p>You can generate a key at <a href="https://speedtest-tracker.dev">https://speedtest-tracker.dev</a>.</p></td></tr><tr><td><code>APP_URL</code></td><td>URL used for assets and links in emails and notifications.</td></tr><tr><td><code>APP_TIMEZONE</code></td><td>Application timezone should be set if your database does not use UTC as it's default timezone.</td></tr><tr><td><code>DISPLAY_TIMEZONE</code></td><td>Display timestamps in your local time.</td></tr><tr><td><code>CONTENT_WIDTH</code></td><td>Width of the content section of each page. Can be set to any value found in the Filament <a href="https://filamentphp.com/docs/3.x/panels/configuration#customizing-the-maximum-content-width">docs</a>.<br><br>- Default:<code>7xl</code></td></tr><tr><td><code>PUBLIC_DASHBOARD</code></td><td>Enables the public dashboard for guest (unauthenticated) users.<br><br>- Default:<code>false</code></td></tr><tr><td><code>DASHBOARD_POLLING</code></td><td>Frequency charts and stats refresh on the dashboard. Can be represented using a string in seconds or<code>false</code>to disable.<br><br>- Default:<code>60s</code></td></tr><tr><td><code>NOTIFICATION</code><br><code>_POLLING</code></td><td>Frequency database notifications are polled. Can be represented using a string in seconds or<code>false</code>to disable.<br><br>- Default:<code>60s</code></td></tr><tr><td><code>RESULTS_POLLING</code></td><td>Frequency data refreshes in the results table. Can be represented using a string in seconds or<code>false</code>to disable.<br><br>- Default:<code>false</code></td></tr></tbody></table>

### Speedtest

<table><thead><tr><th width="226">Name</th><th>Description</th></tr></thead><tbody><tr><td><code>SPEEDTEST</code><br><code>_SCHEDULE</code></td><td>Cron expression used to run speedtests on a scheduled basis.</td></tr><tr><td><code>SPEEDTEST</code><br><code>_SERVERS</code></td><td>Comma separated list of servers to randomly use for speedtests.</td></tr><tr><td><code>PRUNE_RESULTS</code><br><code>_OLDER_THAN</code></td><td>Set the value to greated than zero to prune stored results. This value should be represented in days.</td></tr></tbody></table>

