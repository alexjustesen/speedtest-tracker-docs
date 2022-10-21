# Installation

### Required Configuration

| Variable | Default Value | Description                                   |
| -------- | ------------- | --------------------------------------------- |
| PUID     | 1000          | Update with your UID by running `id username` |
| PGID     | 1000          | Update with your GID by running `id username` |

### Install with Docker

{% hint style="info" %}
MariaDB/MySQL and PostgreSQL instructions assumes you have a database instance that already exists.
{% endhint %}

{% tabs %}
{% tab title="Docker (Sqlite)" %}
```bash
docker run -d --name speedtest-tracker \
    -p 8443:443 \
    -e PUID=1000 \ 
    -e PGID=1000 \
    -v /path/to/directory:/config \
    ghcr.io/alexjustesen/speedtest-tracker:latest
```
{% endtab %}

{% tab title="Docker (MariaDB/MySQL)" %}
```bash
docker run -d --name speedtest-tracker \
    -p 8443:443 \
    -e PUID=1000 \ 
    -e PGID=1000 \
    -e "DB_CONNECTION=mysql" \
    -e "DB_HOST=" \
    -e "DB_PORT=3306" \
    -e "DB_DATABASE=speedtest_tracker" \
    -e "DB_USERNAME=" \
    -e "DB_PASSWORD=" \
    -v /path/to/directory:/config \
    ghcr.io/alexjustesen/speedtest-tracker:latest
```
{% endtab %}

{% tab title="Docker (PostgreSQL)" %}
```bash
docker run -d --name speedtest-tracker \
    -p 8443:443 \
    -e PUID=1000 \ 
    -e PGID=1000 \
    -e "DB_CONNECTION=pgsql" \
    -e "DB_HOST=" \
    -e "DB_PORT=5432" \
    -e "DB_DATABASE=speedtest_tracker" \
    -e "DB_USERNAME=" \
    -e "DB_PASSWORD=" \
    -v /path/to/directory:/config \
    ghcr.io/alexjustesen/speedtest-tracker:latest
```
{% endtab %}
{% endtabs %}
