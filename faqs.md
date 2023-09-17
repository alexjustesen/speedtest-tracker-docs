---
description: A running list of frequently ask questions and their answers.
---

# Frequently Asked Questions

### Database

<details>

<summary>Using SQLite</summary>

SQLite is supported by Laravel as a database driver but it is no longer the recommended driver for this project. To setup SQLite as your database driver of choice use the directions below.

`v0.11.22` dropped SQLite support, to reconnect your existing database you can start on Step 3.

1. Create a volume called `speedtest-tracker` and attach it to the container.
2. Create a file called `database.sqlite`, you can do this by running `touch database.sqlite` in the mounted volume or create it in the mounted directory.
3. Update your environment variables to only include the following for under the `DB_` prefix: `DB_CONNECTION=sqlite` and `DB_HOST=/config/database.sqlite`.
4. Restart the container.

</details>

### Docker

<details>

<summary>I get a warning on container start up that the <code>APP_KEY</code> is missing</summary>

As of `v0.12.0` the app key is generated on start-up and it is **OK to ignore this warning**. To set a persisted key follow the steps below

1. Open the CLI of the Speedtest Docker container
2. Run `php artisan key:generate --show`
3. Add the generated string to your environment variables attached to `APP_KEY=generatedstringgoeshere`
4. Restart the container

</details>

### Notifications

<details>

<summary>Links in emails don't point to the correct URL</summary>

1. Set the correct URL as the `APP_URL` environment variable
2. Restart the container

</details>

### Other

<details>

<summary>I'm getting a <code>500 | SERVER ERROR</code> error</summary>

By default `APP_DEBUG` is set to `false` in production to prevent verbose error outputs. To debug the issue follow the steps below.

1. Set `APP_DEBUG=true` as a environment variable
2. Restart the container
3. Reproduce the error by visiting the page or performing the action that caused the error
4. View the output in the UI or in the logs to help resolve the issue, if you can not resolve it open an issue in the [GitHub](https://github.com/alexjustesen/speedtest-tracker/issues) repository
5. Once the issue is resolved you can remove the `APP_DEBUG` environment variable

</details>
