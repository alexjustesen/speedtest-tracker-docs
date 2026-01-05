---
description: >-
  These instructions will run you through setting up Speedtest Tracker on a
  Docker server using Docker run.
---

# Using Docker

Setting up your environment with Docker Compose is the recommended way as it'll setup the application and a database for you. These steps will run you through setting up the application using Docker and Docker Compose.

{% hint style="info" %}
Docker run commands assume you already have a database installed and configured.
{% endhint %}

### Install with Docker Run

{% stepper %}
{% step %}
**Generate an Application Key**

Run the command below to generate a key, the key is required for [encryption](../../security/encryption.md). Copy this key including the `base64:` prefix and paste it as your `APP_KEY` value.

```bash
echo -n 'base64:'; openssl rand -base64 32;
```
{% endstep %}

{% step %}
**Setting Up Docker**

SQLite is fine for most installs but you can also use more traditional relational databases like MariaDB, MySQL and Postgres.

{% hint style="info" %}
You will need to get your user's `PUID` and `PGID`, you can do this by running `id $user` on the host.

[https://docs.linuxserver.io/general/understanding-puid-and-pgid/](https://docs.linuxserver.io/general/understanding-puid-and-pgid/)
{% endhint %}

{% tabs %}
{% tab title="SQLite" %}
<pre class="language-docker"><code class="lang-docker">docker run -d --name speedtest-tracker --restart unless-stopped \
    -p 8080:80 \
    -p 8443:443 \
    -e PUID= \
    -e PGID= \
    -e <a data-footnote-ref href="#user-content-fn-1">APP_KEY</a>= \
    -e <a data-footnote-ref href="#user-content-fn-2">APP_URL</a>= \
    -e DB_CONNECTION=sqlite \
    -v /path/to/data:/config \
    -v /path/to-custom-ssl-keys:/config/keys \
    lscr.io/linuxserver/speedtest-tracker:latest
</code></pre>
{% endtab %}

{% tab title="MariaDB" %}
```
docker run -d --name speedtest-tracker --restart unless-stopped \
    -p 8080:80 \
    -p 8443:443 \
    -e PUID= \
    -e PGID= \
    -e APP_KEY= \
    -e DB_CONNECTION=mariadb \
    -e DB_HOST= \
    -e DB_PORT=3306 \
    -e DB_DATABASE=speedtest_tracker \
    -e DB_USERNAME= \
    -e DB_PASSWORD= \
    -v /path/to/data:/config \
    -v /path/to-custom-ssl-keys:/config/keys \
    lscr.io/linuxserver/speedtest-tracker:latest
```
{% endtab %}

{% tab title="MySQL" %}
```
docker run -d --name speedtest-tracker --restart unless-stopped \   
    -p 8080:80 \
    -p 8443:443 \
    -e PUID= \
    -e PGID= \
    -e APP_KEY= \
    -e DB_CONNECTION=mysql \
    -e DB_HOST= \
    -e DB_PORT=3306 \
    -e DB_DATABASE=speedtest_tracker \
    -e DB_USERNAME= \
    -e DB_PASSWORD= \
    -v /path/to/data:/config \
    -v /path/to-custom-ssl-keys:/config/keys \
    lscr.io/linuxserver/speedtest-tracker:latest
```
{% endtab %}

{% tab title="Postgres" %}
```
docker run -d --name speedtest-tracker --restart unless-stopped \   
    -p 8080:80 \
    -p 8443:443 \
    -e PUID=1000 \
    -e PGID=1000 \
    -e APP_KEY=
    -e DB_CONNECTION=pgsql \
    -e DB_HOST= \
    -e DB_PORT=5432 \
    -e DB_DATABASE=speedtest_tracker \
    -e DB_USERNAME= \
    -e DB_PASSWORD= \
    -v /path/to/data:/config \
    -v /path/to-custom-ssl-keys:/config/keys \
    lscr.io/linuxserver/speedtest-tracker:latest
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you would like to provide your own SSL keys, they must be named `cert.crt` (full chain) and `cert.key` (private key), and mounted in the container folder `/config/keys`.
{% endhint %}
{% endstep %}

{% step %}
**Environment Variables**

In order for the application to run smoothly, some environment variables need to be set. Check out the [Environment Variables](../environment-variables.md) section. Make sure all **required** variables are configured.
{% endstep %}

{% step %}
**Configuration Variables (Optional)**

You can set configuration variables to have automatic speedtest on an schedule. Check out the [Environment Variables](../environment-variables.md#speedtest) section on how to set the variables. Also see the [FAQ](../../help/faqs.md#speedtest) for tips effectively scheduling tests.

{% hint style="info" %}
Complete overview of the Environment Variables for custom configuration can be found [here](../environment-variables.md).
{% endhint %}
{% endstep %}

{% step %}
**Start the Container**

You can now start the container accordingly the platform you are on.
{% endstep %}

{% step %}
**First Login**

During the start the container there is a default username and password created. Use the [default login](../../security/authentication.md#default-user-account) credentials to login to the application. You can [change the default user](../../security/authentication.md#change-account-details) after logging in.
{% endstep %}
{% endstepper %}

[^1]: Generate with: `echo -n 'base64:'; openssl rand -base64 32`

[^2]: The URL where you'll access the app (e.g., `http://localhost:8080`)
