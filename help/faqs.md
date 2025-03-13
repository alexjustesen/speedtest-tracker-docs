---
description: A running list of frequently ask questions and their answers.
---

# Frequently Asked Questions

### Docker

<details>

<summary>I get a warning on container start up that the <code>APP_KEY</code> is missing</summary>

You need a `APP_KEY` for the encryption. See the [installation docs](../getting-started/installation/) how to generate one.

</details>

### Notifications

<details>

<summary>Links in emails don't point to the correct URL</summary>

1. Set the correct URL as the `APP_URL` environment variable
2. Restart the container

</details>

### Time zones

<details>

<summary>How do I set the display and schedule time zone?</summary>

1. Set `DISPLAY_TIMEZONE` environment variables to your local timezone.
2. Restart the container

</details>

<details>

<summary>My display timestamps or scheduled tests aren't correct.</summary>

Speedtest Tracker assumes your application and database containers are set to `UTC` by default. If your database instance has your local time zone set it needs to **match** that set in `APP_TIMEZONE` and `DISPLAY_TIMEZONE` environment variables.

Once set restart the container.

</details>

### Speedtest

<details>

<summary>Scheduled tests give lower results then manual tests</summary>

Starting your cron schedule at an off-peak minute can help reduce network congestion or avoid overloading a speed test server. This [comment](https://github.com/alexjustesen/speedtest-tracker/issues/552#issuecomment-2028532010) on this issue can help you get the formatting right.

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
