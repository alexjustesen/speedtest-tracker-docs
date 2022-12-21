# Installation

<figure><img src="https://github.com/alexjustesen/speedtest-tracker/blob/main/.github/screenshots/results_screenshot.png?raw=true" alt=""><figcaption><p><em>Results</em></p></figcaption></figure>

### Required Configuration

| Variable | Default Value | Description                                   |
| -------- | ------------- | --------------------------------------------- |
| PUID     | 1000          | Update with your UID by running `id username` |
| PGID     | 1000          | Update with your GID by running `id username` |

### Port Mapping

| Protocol | Internal port |
| -------- | ------------- |
| HTTP     | 80            |
| HTTPS    | 443           |

### Install with Docker

{% hint style="info" %}
MariaDB/MySQL and PostgreSQL instructions assumes you have a database instance that already exists.
{% endhint %}

{% tabs %}
{% tab title="Docker (Sqlite)" %}
```bash
docker run -d --name speedtest-tracker \
    -p 8080:80 \
    -p 8443:443 \
    -e PUID=1000 \ 
    -e PGID=1000 \
    -v /path/to/directory:/config \
    ghcr.io/alexjustesen/speedtest-tracker:latest
    restart: unless-stopped
```
{% endtab %}

{% tab title="Docker (MariaDB/MySQL)" %}
```bash
docker run -d --name speedtest-tracker \
    -p 8080:80 \
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
    restart: unless-stopped
```
{% endtab %}

{% tab title="Docker (PostgreSQL)" %}
```bash
docker run -d --name speedtest-tracker \
    -p 8080:80 \
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
    restart: unless-stopped
```
{% endtab %}
{% endtabs %}

### Install with Docker Compose

{% tabs %}
{% tab title="Docker (Sqlite)" %}
```yaml
version: '3.3'
services:
    speedtest-tracker:
        container_name: speedtest-tracker
        ports:
            - '8080:80'
            - '8443:443'
        environment:
            - PUID=1000
            - PGID=1000
        volumes:
            - '/path/to/directory:/config'
        image: 'ghcr.io/alexjustesen/speedtest-tracker:latest'
        restart: unless-stopped
```
{% endtab %}

{% tab title="Docker (MariaDB/MySQL)" %}
```yaml
version: '3.3'
services:
    speedtest-tracker:
        container_name: speedtest-tracker
        ports:
            - '8080:80'
            - '8443:443'
        environment:
            - PUID=1000
            - PGID=1000
            - DB_CONNECTION=mysql
            - DB_HOST=db
            - DB_PORT=3306
            - DB_DATABASE=speedtest_tracker
            - DB_USERNAME=speedy
            - DB_PASSWORD=password
        volumes:
            - '/path/to/directory:/config'
        image: 'ghcr.io/alexjustesen/speedtest-tracker:latest'
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

{% tab title="Docker (PostgreSQL)" %}
```yaml
version: '3.3'
services:
    speedtest-tracker:
        container_name: speedtest-tracker
        ports:
            - '8080:80'
            - '8443:443'
        environment:
            - PUID=1000
            - PGID=1000
            - DB_CONNECTION=pgsql
            - DB_HOST=db
            - DB_PORT=5432
            - DB_DATABASE=speedtest_tracker
            - DB_USERNAME=speedy
            - DB_PASSWORD=password
        volumes:
            - '/path/to/directory:/config'
        image: 'ghcr.io/alexjustesen/speedtest-tracker:latest'
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
            - MARIADB_RANDOM_ROOT_PASSWORD
        volumes:
            - speedtest-db:/var/lib/postgresql/data
volumes:
  speedtest-db:
```
{% endtab %}
{% endtabs %}

### Install on unRAID

The unRAID community app store contains an app template managed by ZappyZap. Search "Speedtest Tracker" to install. Template support can be found [here](https://forums.unraid.net/topic/130245-support-devzwf-speedtest-tracker/).

### Install on Synology

Activate SSH on your Synology Device and connect to the command line.  

Create your desired installation directory, for example:

```yaml
mkdir -p /opt/speedtest-tracker/config
```

Generate a `docker-compose.yml`:

```yaml
version: '3.3'
services:
    speedtest-tracker:
        container_name: speedtest-tracker
        ports:
            - '8080:80'
            - '8443:443'
        environment:
            - PUID=1000
            - PGID=1000
            - DB_CONNECTION=mysql
            - DB_HOST=db
            - DB_PORT=3306
            - DB_DATABASE=speedtest_tracker
            - DB_USERNAME=speedy
            - DB_PASSWORD=password
        volumes:
            - '/path/to/directory:/config'
        image: 'ghcr.io/alexjustesen/speedtest-tracker:latest'
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

{% hint style="info" %}
Generate secure passwords, adjust volume mapping and ports to your setup. 
{% endhint %}

Start the Speedtest-Tracker containers with:

```
docker-compose up -d
```

Check status of the docker containers with `docker-compose ps` or the docker logs with `docker logs -f speedtest-tracker`.  
You can now access the Web GUI via `http://172.0.0.1:8080` or `https://172.0.0.1:8443`.

{% hint style="info" %}
Remember to allow the used ports in your Synology Firewall.
{% endhint %}
