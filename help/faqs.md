---
description: A running list of frequently ask questions and their answers.
---

# Frequently Asked Questions

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

### Settings

<details>

<summary>Speedtest server</summary>

#### Q: Why do only some servers have the server name in the list?

By default Ookla's CLI only returns the "closest" 20 servers. If the server you've selected isn't in that list Speedtest Tracker can label it.

</details>

### Time zones

<details>

<summary>How do I set the display and schedule time zone?</summary>

Your local time can be set in the UI under `Settings -> General -> Time zone`.

</details>

<details>

<summary>My display timestamps or scheduled tests aren't correct.</summary>

Speedtest Tracker assumes your application and database containers are set to `UTC` by default.

If your database instance runs with a local time zone set it needs to **match** that set in `Time zone` and `Database has time zone` needs to be enabled for the offset to be correctly displayed.

</details>

### Other

<details>

<summary>I'm getting a <code>500 | SERVER ERROR</code> error</summary>

By default `APP_DEBUG` is set to `false` in production to prevent verbose error outputs. To debug the issue follow the steps below.

1. Set `APP_DEBUG=true` as a environment variable
2. Restart the container
3. Reproduce the error by visiting the page or performing the action that caused the error
4. View the output in the UI or in the logs to help resolve the issue, if you can not resolve it open an issue in the [GitHub](https://github.com/alexjustesen/speedtest-tracker/issues) repository
5. In the output the line that starts with `[timestamp] production.ERROR:` is the error the server ran into
6. Once the issue is resolved you can remove the `APP_DEBUG` environment variable

</details>
