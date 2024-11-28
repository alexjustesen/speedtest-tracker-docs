---
description: >-
  Speedtest Tracker can be run on a variety of platforms, the preferred platform
  is  Docker.
---

# Installation

These steps will run you through setting up the application using Docker and Docker Compose.

### Install with Docker&#x20;

Setting up your environment with Docker Compose is the recommended way as it'll setup the application and a database for you. SQLite is fine for most installs but we also provide instructions for setting up MariaDB, MySQL and Postgres should you prefer those database drivers.

If you would like to provide your own SSL keys, they must be named `cert.crt` (full chain) and `cert.key` (private key), and mounted in the container folder `/config/keys`.

{% hint style="info" %}
Complete overview of the Environment Variables can be found [here](environment-variables.md)
{% endhint %}

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

The following environment variables need to be set: `APP_TIMEZONE`, `DATETIME_FORMAT`, and `APP_KEY`. Instructions on how to set them can be found [here](environment-variables.md).

### Install with Kubernetes

Check out this amazing community kubernetes manifest to get you started.

{% embed url="https://github.com/maximemoreillon/kubernetes-manifests/tree/master/speedtest-tracker" %}
