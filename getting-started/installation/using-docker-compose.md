---
description: >-
  These instructions will run you through setting up Speedtest Tracker on a
  Docker server using Docker Compose.
---

# Using Docker Compose

Setting up your environment with Docker Compose is the recommended way as it'll setup the application and a database for you. These steps will run you through setting up the application using Docker and Docker Compose.

{% hint style="info" %}
Docker run commands can be found on the [Using Docker](using-docker.md) page and assume you already have a database installed and configured.
{% endhint %}

### Install with Docker Compose

{% stepper %}
{% step %}
#### Generate an Application Key

You can get a generated key on [https://speedtest-tracker.dev/](https://speedtest-tracker.dev/) or run the command below. The key is required for [encryption](../../security/encryption.md).

Copy this key including the `base64:` prefix and paste it as your `APP_KEY` value.

```bash
echo -n 'base64:'; openssl rand -base64 32;
```
{% endstep %}

{% step %}
#### **Setting Up Docker**

SQLite is fine for most installs but you can also use more traditional relational databases like MariaDB, MySQL and Postgres.

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
        volumes:
            - /path/to/data:/config
            - /path/to-custom-ssl-keys:/config/keys
```
{% endtab %}

{% tab title="MariaDB" %}
<pre class="language-yaml"><code class="lang-yaml">services:
<strong>    speedtest-tracker:
</strong>        image: lscr.io/linuxserver/speedtest-tracker:latest
        restart: unless-stopped
        container_name: speedtest-tracker
        ports:
            - 8080:80
            - 8443:443
        environment:
            - PUID=1000
            - PGID=1000
            - APP_KEY=
            - DB_CONNECTION=mariadb
            - DB_HOST=db
            - DB_PORT=3306
            - DB_DATABASE=speedtest_tracker
            - DB_USERNAME=speedtest_tracker
            - DB_PASSWORD=password
        volumes:
            - /path/to/data:/config
            - /path/to-custom-ssl-keys:/config/keys
        depends_on:
            - db
    db:
        image: mariadb:11
        restart: always
        environment:
            - MYSQL_DATABASE=speedtest_tracker
            - MYSQL_USER=speedtest_tracker
            - MYSQL_PASSWORD=password
            - MYSQL_RANDOM_ROOT_PASSWORD=true
        volumes:
            - speedtest-db:/var/lib/mysql
        healthcheck:
            test: ["CMD", "healthcheck.sh", "--connect", "--innodb_initialized"]
            interval: 5s
            retries: 3
            timeout: 5s
volumes:
  speedtest-db:
</code></pre>
{% endtab %}

{% tab title="MySQL" %}
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
            - DB_USERNAME=speedtest_tracker
            - DB_PASSWORD=password
        volumes:
            - /path/to/data:/config
            - /path/to-custom-ssl-keys:/config/keys
        depends_on:
            - db
    db:
        image: mysql:8
        restart: always
        environment:
            - MYSQL_DATABASE=speedtest_tracker
            - MYSQL_USER=speedtest_tracker
            - MYSQL_PASSWORD=password
            - MYSQL_RANDOM_ROOT_PASSWORD=true
        volumes:
            - speedtest-db:/var/lib/mysql
        healthcheck:
            test: ["CMD", "mysqladmin", "ping", "-p${MYSQL_PASSWORD}"]
            interval: 5s
            retries: 5
            timeout: 5s
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
            - DB_USERNAME=speedtest_tracker
            - DB_PASSWORD=password
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
            - POSTGRES_USER=speedtest_tracker
            - POSTGRES_PASSWORD=password
        volumes:
            - speedtest-db:/var/lib/postgresql/data
        healthcheck:
            test: ["CMD-SHELL", "pg_isready -U ${POSTGRES_USER} -d ${POSTGRES_DB}"]
            interval: 5s
            retries: 5
            timeout: 5s
volumes:
  speedtest-db:
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you would like to provide your own SSL keys, they must be named `cert.crt` (full chain) and `cert.key` (private key), and mounted in the container folder `/config/keys`.
{% endhint %}
{% endstep %}

{% step %}
#### **Environment Variables**

In order for the application to run smoothly, some environment variables need to be set. Check out the [Environment Variables](../environment-variables.md) section. Make sure all r**equired** variables are configured.
{% endstep %}

{% step %}
#### **Configuration Variables (Optional)**

You can set configuration variables to have automatic speedtest on an schedule. Check out the [Environment Variables](../environment-variables.md#speedtest) section on how to set the variables. Also see the [FAQ](../../help/faqs.md#speedtest) for tips effectively scheduling tests.

{% hint style="info" %}
Complete overview of the Environment Variables for custom configuration can be found [here](../environment-variables.md).
{% endhint %}
{% endstep %}

{% step %}
#### **Start the Container**

You can now start the container accordingly the platform you are on.
{% endstep %}

{% step %}
#### **First Login**

During the start the container there is a default username and password created. Use the [default login](../../security/authentication.md#default-user-account) credentials to login to the application. You can [change the default user](../../security/authentication.md#change-account-details) after logging in.
{% endstep %}
{% endstepper %}
