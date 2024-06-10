---
description: >-
  These steps will run you through setting up the application using Docker and
  Docker Compose.
---

# Using Docker or Docker Compose

### Install with Docker Compose (recommended)

Setting up your environment with Docker Compose is the recommended infrastructure pattern as it'll setup the application and a database for you. SQLite is fine for most installs but we also provide instructions for setting up MariaDB, MySQL and Postgres should you prefer those database drivers.

If you would like to provide your own SSL keys, they must be named `cert.crt` (full chain) and `cert.key` (private key), and mounted in the container folder `/config/keys`.

{% hint style="info" %}
Complete overview of the Environment Variables can be found here
[environment-variables.md](environment-variables.md "mention").
{% endhint %}

{% tabs %}
{% tab title="SQLite" %}
```yaml
version: '3.4'
services:
    speedtest-tracker:
        container_name: speedtest-tracker
        ports:
            - 8080:80
            - 8443:443
        environment:
            - PUID=1000
            - PGID=1000
            - APP_KEY=
            - DB_CONNECTION=sqlite
            - SPEEDTEST_SCHEDULE=
            - SPEEDTEST_SERVERS=
            - PRUNE_RESULTS_OLDER_THAN=
            - CHART_DATETIME_FORMAT= 
            - DATETIME_FORMAT=
            - APP_TIMEZONE=
        volumes:
            - /path/to/data:/config
            - /path/to-custom-ssl-keys:/config/keys
        image: lscr.io/linuxserver/speedtest-tracker:latest
        restart: unless-stopped
```
{% endtab %}

{% tab title="MariaDB/MySQL" %}
```yaml
version: '3.4'
services:
    speedtest-tracker:
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
        image: lscr.io/linuxserver/speedtest-tracker:latest
        restart: unless-stopped
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
version: '3.4'
services:
    speedtest-tracker:
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
        image: lscr.io/linuxserver/speedtest-tracker:latest
        restart: unless-stopped
        depends_on:
            - db
    db:
        image: postgres:15
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

***

### Install with Docker

{% hint style="info" %}
These instructions assume you have an appropriate database instance that already exists.
{% endhint %}

{% tabs %}
{% tab title="SQLite" %}
```bash
docker run -d --name speedtest-tracker --restart unless-stopped \
    -p 8080:80 \
    -p 8443:443 \
    -e PUID=1000 \
    -e PGID=1000 \
    -e APP_KEY= \
    -e DB_CONNECTION=sqlite \
    -e SPEEDTEST_SCHEDULE= \
    -e SPEEDTEST_SERVERS= \
    -e PRUNE_RESULTS_OLDER_THAN= \
    -e CHART_DATETIME_FORMAT= \
    -e DATETIME_FORMAT= \
    -e APP_TIMEZONE= \
    -v /path/to/data:/config \
    -v /path/to-custom-ssl-keys:/config/keys \
    lscr.io/linuxserver/speedtest-tracker:latest
```
{% endtab %}

{% tab title="MariaDB/MySQL" %}
```bash
docker run -d --name speedtest-tracker --restart unless-stopped \
    -p 8080:80 \
    -p 8443:443 \
    -e PUID=1000 \
    -e PGID=1000 \
    -e APP_KEY= \
    -e DB_CONNECTION=mysql \
    -e DB_HOST= \
    -e DB_PORT=3306 \
    -e DB_DATABASE=speedtest_tracker \
    -e DB_USERNAME= \
    -e DB_PASSWORD= \
    -e SPEEDTEST_SCHEDULE= \
    -e SPEEDTEST_SERVERS= \
    -v /path/to/data:/config \
    -v /path/to-custom-ssl-keys:/config/keys \
    lscr.io/linuxserver/speedtest-tracker:latest
```
{% endtab %}

{% tab title="Postgres" %}
```bash
docker run -d --name speedtest-tracker --restart unless-stopped \
    -p 8080:80 \
    -p 8443:443 \
    -e PUID=1000 \
    -e PGID=1000 \
    -e APP_KEY \
    -e DB_CONNECTION=pgsql \
    -e DB_HOST= \
    -e DB_PORT=5432 \
    -e DB_DATABASE=speedtest_tracker \
    -e DB_USERNAME= \
    -e DB_PASSWORD= \
    -e SPEEDTEST_SCHEDULE= \
    -e SPEEDTEST_SERVERS= \
    -e PRUNE_RESULTS_OLDER_THAN= \
    -e CHART_DATETIME_FORMAT= \
    -e DATETIME_FORMAT= \
    -e APP_TIMEZONE= \
    -v /path/to/data:/config \
    -v /path/to-custom-ssl-keys:/config/keys \
    lscr.io/linuxserver/speedtest-tracker:latest
```
{% endtab %}
{% endtabs %}
