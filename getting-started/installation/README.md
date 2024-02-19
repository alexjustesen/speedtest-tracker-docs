# Installation

Speedtest Tracker can be run on a variety of platforms including using [Docker and Docker Compose](installation.md) along with [Synology NAS](installation-1.md) devices and on [Unraid OS](installation-2.md).

{% hint style="info" %}
Docker Compose is the recommended platform.
{% endhint %}

### Environment Variables

#### Core

<table><thead><tr><th width="225">Name</th><th>Description</th></tr></thead><tbody><tr><td><code>PUID</code><br><br>(required)</td><td>Used to set the user the container should run as. To find your UID run <code>id username</code> on the host machine.<br><br>- Default: <code>1000</code></td></tr><tr><td><code>PGID</code><br><br>(required)</td><td>Used to set the group the container should run as. To find your GID run <code>id username</code> on the host machine.<br><br>- Default: <code>1000</code></td></tr><tr><td><code>APP_KEY</code></td><td>Key used to encrypt and decrypt data. To create a key to persist follow the directions in the <a href="../../help/faqs.md#i-get-a-warning-on-container-start-up-that-the-app_key-is-missing">FAQ</a>.<br><br><em>Currently not used and generated at random on startup of the container</em>.</td></tr><tr><td><code>APP_DEBUG</code></td><td>Used to help narrow down issues in a running container, see <a href="../../help/faqs.md#im-getting-a-500-or-server-error-error">FAQ</a> for when to use it.<br><br>- Default: <code>false</code></td></tr><tr><td><code>DB_CONNECTION</code><br><br>(required)</td><td>Type of database to be used for storing data. Accepted values are <code>sqlite</code>, <code>mysql</code> and <code>pgsql</code>.</td></tr><tr><td><code>DB_HOST</code><br><br>(required)</td><td>FQDN or container name where the database is located.</td></tr><tr><td><code>DB_PORT</code></td><td>Port used to connect to the host where the database is located. Only needs to be defined if the database is running on a different port.<br><br>- Default: <code>3306</code> when using MySQL or MariaDB<br>- Default: <code>5432</code> when using Postgresql</td></tr><tr><td><code>DB_DATABASE</code><br><br>(required)</td><td>Name of the database.</td></tr><tr><td><code>DB_USERNAME</code><br><br>(required)</td><td>Database user used to connect to the database. Needs <code>read/write</code> access.</td></tr><tr><td><code>DB_PASSWORD</code><br><br>(required)</td><td>Password for the user specified to connect to the database.</td></tr><tr><td><code>FORCE_HTTPS</code></td><td>Enforces the user of <code>https</code> protocol when viewing the UI, port 443 must be mapped to the container for this to work.<br><br>- Default: <code>false</code></td></tr></tbody></table>

#### Functional

<table><thead><tr><th width="225">Name</th><th>Description</th></tr></thead><tbody><tr><td><code>CONTENT_WIDTH</code></td><td>Width of the content section of each page. Can be set to any value found in the Filament <a href="https://filamentphp.com/docs/3.x/panels/configuration#customizing-the-maximum-content-width">docs</a>.<br><br>- Default: <code>7xl</code></td></tr><tr><td><code>DASHBOARD_POLLING</code></td><td>Frequency charts and stats refresh on the dashboard. Can be represented using a string in seconds or <code>false</code> to disable.<br><br>- Default: <code>60s</code></td></tr><tr><td><code>NOTIFICATION_POLLING</code></td><td>Frequency database notifications are polled. Can be represented using a string in seconds or <code>false</code> to disable.<br><br>- Default: <code>60s</code></td></tr><tr><td><code>RESULTS_POLLING</code></td><td>Frequency data refreshes in the results table. Can be represented using a string in seconds or <code>false</code> to disable.<br><br>- Default: <code>false</code></td></tr><tr><td><code>ALLOW_EMBEDS</code></td><td>Can be a comma separated list of URLs that the application will allow to be embedded in.<br><br>- Default: <code>null</code></td></tr></tbody></table>

***

### Port Mapping

<table><thead><tr><th>Protocol</th><th data-type="number">External port (default)</th><th data-type="number">Internal port</th></tr></thead><tbody><tr><td>HTTP</td><td>80</td><td>80</td></tr><tr><td>HTTPS</td><td>443</td><td>443</td></tr></tbody></table>

