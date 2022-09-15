# Installation

### Install with Docker

{% hint style="info" %}
MariaDB/MySQL and PostgreSQL instructions assumes you have a database instance that already exists.
{% endhint %}

{% tabs %}
{% tab title="Docker (Sqlite)" %}
```bash
docker run -itd --name speedtest-tracker \
    -p 8080:80 \
    -e "PHP_POOL_NAME=speedtest-tracker_php" \
    -e "DB_CONNECTION=sqlite" \
    -e "DB_DATABASE=/app/database.sqlite" \
    -v /path/to/directory:/app \
    speedtest-tracker
```
{% endtab %}

{% tab title="Docker (MariaDB/MySQL)" %}
```bash
docker run -itd --name speedtest-tracker \
    -p 8080:80 \
    -e "PHP_POOL_NAME=speedtest-tracker_php" \
    -e "DB_CONNECTION=mysql" \
    -e "DB_HOST=" \
    -e "DB_PORT=3306" \
    -e "DB_DATABASE=speedtest_tracker" \
    -e "DB_USERNAME=" \
    -e "DB_PASSWORD=" \
    -v /path/to/directory:/app \
    speedtest-tracker
```
{% endtab %}

{% tab title="Docker (PostgreSQL)" %}
```bash
docker run -itd --name speedtest-tracker \
    -p 8080:80 \
    -e "PHP_POOL_NAME=speedtest-tracker_php" \
    -e "DB_CONNECTION=pgsql" \
    -e "DB_HOST=" \
    -e "DB_PORT=5432" \
    -e "DB_DATABASE=speedtest_tracker" \
    -e "DB_USERNAME=" \
    -e "DB_PASSWORD=" \
    -v /path/to/directory:/app \
    speedtest-tracker
```
{% endtab %}
{% endtabs %}
