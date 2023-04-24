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

{% hint style="info" %}
In case you want to make sure that your ssl certs are kept between stops and starts make sure that you map /etc/ssl/web 
to make it persistent
{% endhint %}

{% tabs %}
{% tab title="Docker (Sqlite)" %}
```bash
docker run -d --name speedtest-tracker --restart unless-stopped \
    -p 8080:80 \
    -p 8443:443 \
    -e PUID=1000 \
    -e PGID=1000 \
    -v /path/to/directory:/config \
    -v /path/to/directory/web:/etc/ssl/web \
    ghcr.io/alexjustesen/speedtest-tracker:latest
```
{% endtab %}

{% tab title="Docker (MariaDB/MySQL)" %}
```bash
docker run -d --name speedtest-tracker --restart unless-stopped \
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
    -v /path/to/directory/web:/etc/ssl/web \
    ghcr.io/alexjustesen/speedtest-tracker:latest
```
{% endtab %}

{% tab title="Docker (PostgreSQL)" %}
```bash
docker run -d --name speedtest-tracker --restart unless-stopped \
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
    -v /path/to/directory/web:/etc/ssl/web \
    ghcr.io/alexjustesen/speedtest-tracker:latest
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
            - '/path/to/directory/web:/etc/ssl/web'
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
            - '/path/to/directory/web:/etc/ssl/web'
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
            - '/path/to/directory/web:/etc/ssl/web'
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

Open the Docker interface of your Synology Device, search for `ajustesen/speedtest-tracker` in the Registry and download it.

![download\_image](https://user-images.githubusercontent.com/92191413/210480118-b15f83af-6617-4a0d-b631-760f419425b9.png)

Create a local directory (i.e. `/volume1/docker/speedtest-tracker`) which later can be mapped to the docker container.

Launch the image once the download is completed.

![launch\_image](https://user-images.githubusercontent.com/92191413/210480210-baa06b52-c3b0-41a4-b50e-ce7af82d683c.png)

Map the ports to available ports.

![port\_mapping](https://user-images.githubusercontent.com/92191413/210481629-6fa76992-403a-415e-9967-af7b00c97d87.png)

{% hint style="info" %}
Make sure the ports you choose are not used by any other application or DSM service on your device and remember to adjust the Synology Firewall settings accordingly.
{% endhint %}

Map the directory you created earlier to the mount path `/config`.

![volume\_mapping](https://user-images.githubusercontent.com/92191413/210480901-069703e3-c6ab-446c-b53b-8c5ef3c87085.png)

Review your settings and click "done".

![summary](https://user-images.githubusercontent.com/92191413/210480977-3e24ba39-b23e-463f-acba-0a1aad1e57ec.png)

You can now access Speedtest-Tracker via `http://YOUR_IP_ADDRESS:8080` or `https://YOUR_IP_ADDRESS:8443`.
