---
description: >-
  These instructions will run you through setting up Speedtest Tracker on a QNAP
  NAS using Container Station.
---

# Using QNAP

These instructions will run you through setting up the application on a QNAP NAS and will also create a MariaDB container for you to use as a database.

1. Open **"Container Station"** and select **"Applications"** from the left-hand navigation menu.
2. Press the **"Create"** button.
3. Provide a name for the application.
4. Paste the below Docker Compose code into the text box, this is a modification of the MariaDB Docker Compose [install ](using-docker-compose.md)instructions.
5. Click **"Validate"** to make sure there are no errors.
6. Click **"Create"** to deploy the application.

### Example Docker Compose

{% hint style="info" %}
A full list of released versions can be found [here](https://fleet.linuxserver.io/image?name=linuxserver/speedtest-tracker)
{% endhint %}

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
      - DB_CONNECTION=mariadb
      - DB_HOST=db
      - DB_PORT=3306
      - DB_DATABASE=speedtest_tracker
      - DB_USERNAME=speedy
      - DB_PASSWORD=password
      - APP_KEY=
      - DATETIME_FORMAT=
      - APP_TIMEZONE=
      - SPEEDTEST_SCHEDULE= # Optional
      - SPEEDTEST_SERVERS= # Optional
    volumes:
      - /path/to-data:/config
      - /path/to-custom-ssl-keys:/config/keys
    image: lscr.io/linuxserver/speedtest-tracker:latest
    networks:
      qnet-network:
        ipv4_address: 192.168.1.3
    restart: unless-stopped
    depends_on:
      - db
  db:
    image: mariadb:10
    networks:
      qnet-network:
        ipv4_address: 192.168.1.4
    restart: always
    environment:
      - MARIADB_DATABASE=speedtest_tracker
      - MARIADB_USER=speedy
      - MARIADB_PASSWORD=password
      - MARIADB_RANDOM_ROOT_PASSWORD=true
    volumes:
      - speedtest-db:/var/lib/mysql

networks:
  qnet-network:
    driver_opts:
      iface: eth0
    driver: qnet
    ipam:
      driver: qnet
      options:
        iface: eth0
      config:
        - subnet: 192.168.1.0/24
          gateway: 192.168.1.1

volumes:
  speedtest-db:
```
