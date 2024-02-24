# QNAP

## Installing Speedtest-Tracker in a QNAP NAS using Container Station.

These instructions will run you through setting up the application on a QNAP NAS and will also create a MariaDB container for you to use as a database.

1. **Open Container Station**, select "Applications" from the left-hand navigation menu.
2. **Press the Create Button**.
3. **Provide a name** for your Application; something like "speedtest-tracker" would work.
4. **Paste the following YAML code** into the text box:

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
      - DB_HOST=192.168.1.4
      - DB_PORT=3306
      - DB_DATABASE=speedtest_tracker
      - DB_USERNAME=speedy
      - DB_PASSWORD=password
    volumes:
      - speedtest-app:/config
      - '/speedtest-tracker:/etc/ssl/web'
    image: 'ghcr.io/alexjustesen/speedtest-tracker:latest'
    networks:
      qnet-network:
        ipv4_address: 192.168.1.3
    restart: unless-stopped
    depends_on:
      - db
  db:
    image: mariadb:latest
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
  speedtest-app:
  speedtest-db:
```

5. **Edit the above code** for your needs, focusing on items such as IP addresses and DB credentials.
6. **Press "Validate"**.
7. **Press "Create"**.

Upon creation completion, you will have an application within Container Station named "speedtest-tracker" that features 2 containers within it, one for your MariaDB database and another one for the actual speed-test tracker container, that you can start up and access.

You can now access Speedtest-Tracker via `http://YOUR_IP_ADDRESS` and use the default credentials of:

- **Username**: admin@example.com
- **Password**: password
