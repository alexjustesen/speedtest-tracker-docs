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

SQLite is a good option for simple installs and only not recommended because I think separating your application and the database into separate services is a better idea.

To use SQLite follow the steps below to create your database file:&#x20;

1. Create a volume called `speedtest-tracker` or mount a directory to the container.
2. Create a file called `database.sqlite`, you can do this by running `touch database.sqlite` in the mounted volume or create it in the mounted directory.
3. Update your environment variables to only include the following environment variable in the table below.
4. On start-up the container will checked for the database on the file system, if it can find it errors will be thrown to the log.

| Environment Variable | Value    |
| -------------------- | -------- |
| `DB_CONNECTION`      | `sqlite` |

#### MySQL/MariaDB

MariaDB ships as the default database that's included in the `docker-compose.yml` configuration, it's functionally the same as MySQL just an open-source earlier fork.

| Environment Variable | Value                                                                                                          |
| -------------------- | -------------------------------------------------------------------------------------------------------------- |
| `DB_CONNECTION`      | <p><code>mysql</code>  </p><p></p><p>The <code>mysql</code> driver can be used for both MySQL and MariaDB.</p> |
| `DB_HOST`            | The FQDN or address to the database instance.                                                                  |
| `DB_PORT`            | `3306` is the default port but can depend on your setup.                                                       |
| `DB_DATABASE`        | Name of the database you'll connect to.                                                                        |
| `DB_USERNAME`        | User that'll be used to connect to the database.                                                               |
| `DB_PASSWORD`        | Password for the user above.                                                                                   |

#### Postgres

| Environment Variable | Value                                                    |
| -------------------- | -------------------------------------------------------- |
| `DB_CONNECTION`      | `pgsql`                                                  |
| `DB_HOST`            | The FQDN or address to the database instance.            |
| `DB_PORT`            | `5432` is the default port but can depend on your setup. |
| `DB_DATABASE`        | Name of the database you'll connect to.                  |
| `DB_USERNAME`        | User that'll be used to connect to the database.         |
| `DB_PASSWORD`        | Password for the user above.                             |
