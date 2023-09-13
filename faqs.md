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

### User

<details>

<summary></summary>



</details>
