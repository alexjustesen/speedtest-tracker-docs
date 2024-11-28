---
description: >-
  Speedtest Tracker can be run on a variety of platforms, the preferred platform
  is  Docker.
---

# Copy of Installation

These steps will run you through setting up the application using Docker and Docker Compose.

### Install with Docker

{% stepper %}
{% step %}
### Setup Docker Compose

Setting up your environment with Docker Compose is the recommended way as it'll setup the application and a database for you. SQLite is fine for most installs but we also provide instructions for setting up MariaDB, MySQL and Postgres should you prefer those database drivers.

If you would like to provide your own SSL keys, they must be named `cert.crt` (full chain) and `cert.key` (private key), and mounted in the container folder `/config/keys`.

{% tabs %}
{% tab title="SQLite" %}
```yaml
services:
    speedtest-tracker:
        image: lscr.io/linuxserver/speedtest-tracker:latest
        restart: unless-stopped
        container_name: speedtest-tracker
        ports:
            - 8080:80
            - 8443:443
        environment:
            - PUID=1000
            - PGID=1000
            - APP_KEY=
            - DB_CONNECTION=sqlite
            - SPEEDTEST_SCHEDULE= # Optional
            - SPEEDTEST_SERVERS= # Optional
            - DATETIME_FORMAT=
            - APP_TIMEZONE=
        volumes:
            - /path/to/data:/config
            - /path/to-custom-ssl-keys:/config/keys

```
{% endtab %}

{% tab title="MariaDB/MySQL" %}
```yaml
services:
    speedtest-tracker:
        image: lscr.io/linuxserver/speedtest-tracker:latest
        restart: unless-stopped
        container_name: speedtest-tracker
        ports:
            - 8080:80
            - 8443:443
        environment:
            - PUID=1000
            - PGID=1000
            - APP_KEY=
            - DB_CONNECTION=mysql
            - DB_HOST=db
            - DB_PORT=3306
            - DB_DATABASE=speedtest_tracker
            - DB_USERNAME=speedy
            - DB_PASSWORD=password
            - SPEEDTEST_SCHEDULE=
            - SPEEDTEST_SERVERS=
            - PRUNE_RESULTS_OLDER_THAN=
            - CHART_DATETIME_FORMAT= 
            - DATETIME_FORMAT=
            - APP_TIMEZONE=
        volumes:
            - /path/to/data:/config
            - /path/to-custom-ssl-keys:/config/keys
        depends_on:
            - db
    db:
        image: mariadb:10
        restart: always
        environment:
            - MARIADB_DATABASE=speedtest_tracker
            - MARIADB_USER=speedy
            - MARIADB_PASSWORD=password
            - MARIADB_RANDOM_ROOT_PASSWORD=true
        volumes:
            - speedtest-db:/var/lib/mysql
volumes:
  speedtest-db:
```
{% endtab %}

{% tab title="Postgres" %}
```yaml
services:
    speedtest-tracker:
        image: lscr.io/linuxserver/speedtest-tracker:latest
        restart: unless-stopped
        container_name: speedtest-tracker
        ports:
            - 8080:80
            - 8443:443
        environment:
            - PUID=1000
            - PGID=1000
            - APP_KEY=
            - DB_CONNECTION=pgsql
            - DB_HOST=db
            - DB_PORT=5432
            - DB_DATABASE=speedtest_tracker
            - DB_USERNAME=speedy
            - DB_PASSWORD=password
            - SPEEDTEST_SCHEDULE=
            - SPEEDTEST_SERVERS=
            - PRUNE_RESULTS_OLDER_THAN=
            - CHART_DATETIME_FORMAT= 
            - DATETIME_FORMAT=
            - APP_TIMEZONE=
        volumes:
            - /path/to/data:/config
            - /path/to-custom-ssl-keys:/config/keys
        depends_on:
            - db
    db:
        image: postgres:17
        restart: always
        environment:
            - POSTGRES_DB=speedtest_tracker
            - POSTGRES_USER=speedy
            - POSTGRES_PASSWORD=password
        volumes:
            - speedtest-db:/var/lib/postgresql/data
volumes:
  speedtest-db:
```
{% endtab %}
{% endtabs %}
{% endstep %}

{% step %}
#### Setting Environment Variables

In order for the application to run smoothly, some environment variables need to be test. &#x20;

<table><thead><tr><th width="218">Name</th><th>Description</th><th>Example</th></tr></thead><tbody><tr><td><code>APP_KEY</code></td><td><p>Key used to encrypt and decrypt data.</p><p>You can generate a key at <a href="https://speedtest-tracker.dev">https://speedtest-tracker.dev</a>.</p></td><td><code>base64:ZoOYTjS+LBwFtud8SArwhiw8V4Qi9J+MPiT7z8XjfMo=</code><br>(DONT USE THIS EXAMPLE)</td></tr><tr><td><code>APP_TIMEZONE</code></td><td>Application timezone should be set if your database does not use UTC as its default timezone.</td><td><code>Europe/London</code></td></tr><tr><td><code>DISPLAY_TIMEZONE</code></td><td>Display timestamps in your local time.</td><td><code>Europe/London</code></td></tr></tbody></table>


{% endstep %}
{% endstepper %}





Optionally you can set a schedule for automatic speedtest. Check out the tips for the best schedule [here](../help/faqs.md#cron-schedule-from-a-minute-or-hour).&#x20;

{% hint style="info" %}
Complete overview of the Environment Variables for custom configuration can be found [here](environment-variables.md)
{% endhint %}

### Install with Kubernetes

Check out this amazing community kubernetes manifest to get you started.

{% embed url="https://github.com/maximemoreillon/kubernetes-manifests/tree/master/speedtest-tracker" %}
