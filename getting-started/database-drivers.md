---
description: >-
  Speedtest Tracker supports multiple database drivers including SQLite, MySQL
  and Postgres.
---

# Database Drivers

Since Speedtest Tracker is built on the Laravel Framework any of the framework's supported database [drivers](https://laravel.com/docs/10.x/database#configuration) are also supported.

SQLite ships as the default driver but you can also use MySQL/MariaDB and Postgres. While SQL Server is supported by Laravel it hasn't been tested with Speedtest Tracker so no support will be provided for that driver.

***

### Driver Options

#### SQLite (Default)

SQLite is a good option for simple installs. The database will be create automatically inside the docker volume.&#x20;

| Environment Variable | Value    |
| -------------------- | -------- |
| `DB_CONNECTION`      | `sqlite` |

#### MariaDB

| Environment Variable | Value                                                    |
| -------------------- | -------------------------------------------------------- |
| `DB_CONNECTION`      | `mariadb`                                                |
| `DB_HOST`            | The FQDN or address to the database instance.            |
| `DB_PORT`            | `3306` is the default port but can depend on your setup. |
| `DB_DATABASE`        | Name of the database you'll connect to.                  |
| `DB_USERNAME`        | User that'll be used to connect to the database.         |
| `DB_PASSWORD`        | Password for the user above.                             |

#### MySQL

| Environment Variable | Value                                                    |
| -------------------- | -------------------------------------------------------- |
| `DB_CONNECTION`      | `mysql`                                                  |
| `DB_HOST`            | The FQDN or address to the database instance.            |
| `DB_PORT`            | `3306` is the default port but can depend on your setup. |
| `DB_DATABASE`        | Name of the database you'll connect to.                  |
| `DB_USERNAME`        | User that'll be used to connect to the database.         |
| `DB_PASSWORD`        | Password for the user above.                             |

#### Postgres

| Environment Variable | Value                                                    |
| -------------------- | -------------------------------------------------------- |
| `DB_CONNECTION`      | `pgsql`                                                  |
| `DB_HOST`            | The FQDN or address to the database instance.            |
| `DB_PORT`            | `5432` is the default port but can depend on your setup. |
| `DB_DATABASE`        | Name of the database you'll connect to.                  |
| `DB_USERNAME`        | User that'll be used to connect to the database.         |
| `DB_PASSWORD`        | Password for the user above.                             |
