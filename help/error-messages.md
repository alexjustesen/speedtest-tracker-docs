# Error Messages

### Troubleshooting

For all below errros there will be more information provided in the container logs. You can check the logs for more details by checking the container logs by running;

`docker logs speedtest-tracker`&#x20;

or any other equivalent command for your setup.&#x20;

<details>

<summary>Enable Debugging</summary>

By default `APP_DEBUG` is set to `false` in production to prevent verbose error outputs. To debug the issue follow the steps below.

1. Set `APP_DEBUG=true` as a environment variable
2. Restart the container
3. Reproduce the error by visiting the page or performing the action that caused the error
4. View the output in the UI or in the logs to help resolve the issue, if you can not resolve it open an issue in the [GitHub](https://github.com/alexjustesen/speedtest-tracker/issues) repository
5. In the output the line that starts with `[timestamp] production.ERROR:` is the error the server ran into
6. Once the issue is resolved you can remove the `APP_DEBUG` environment variable

</details>

### Application

<details>

<summary>I'm getting a <code>500 | SERVER ERROR</code> error</summary>

The `500 | SERVER ERROR` is caused by either a bug or a misconfiguration. You must e[nable debugging](error-messages.md#enable-debugging) to determine the exact cause of the error.

</details>

<details>

<summary>Unsupported cipher or incorrect key length. Supported ciphers are: <code>aes-128-cbc</code>, <code>aes-256-cbc</code>, <code>aes-128-gcm,</code> <code>aes-256-gcm</code>.</summary>

This error is shown when the `APP_KEY` is not set or not set correctly. Make suer you set the `APP_KEY`  as described in the [installation steps](../getting-started/installation/using-docker-compose.md#install-with-docker-compose).

</details>

### Speedtest Process

<details>

<summary>Failed to connected to hostname</summary>

When a speedtest is being [processed](../other/speedtest-process.md) Speedtest Tracker will make a ICMP ping to [icanhazip.com](http://icanhazip.com) to check if there is an internet connection before starting the Speedtest

**Possible reasons**:

* There is a docker network problem or no internet connection.
* Some DNS blocks lists will block this domain, if you're getting errors and your server has access to the internet you'll need to add this to your allow lists.
* _Most_ Docker setups can send ICMP requests without needed elevated privileges on the host or in the container. That being said if your Docker user doesn't run with elevated permissions or doesn't belong to the Docker group you can get a failure on this step. To allow the user to send ICMP requests you need to add the permission to the container.

**Configuration options**

* Use available [Environment Variables](../getting-started/environment-variables.md#speed-tests) to change the endpoint to your liking

</details>

<details>

<summary>Failed to fetch external IP address</summary>

When the `SPEEDTEST_SKIP_IPS` environment variable is  Speedtest Tracker will make a call to [http://icanhazip.com](http://icanhazip.com/) to get your external IP address. This is done check if your external IP address (WAN IP) should be skipped.

**Possible reasons**:

* There is a docker network problem or no internet connection.
* Some DNS blocks lists will block this domain, if you're getting errors and your server has access to the internet you'll need to add this to your allow lists.

**Configuration options**

* Use available [Environment Variables](../getting-started/environment-variables.md#speed-tests) to change the endpoint to your liking. :warning: Whatever service you choose needs to only return an IP address in the body of the response for this to work.

</details>

### Ookla Related

<details>

<summary>Configuration - Could not retrieve or read configuration (ConfigurationError)</summary>

This is usually thrown when the CLI fails to reach the internet (internet down) or the specified server.

</details>

<details>

<summary>Configuration - No servers defined (NoServersException)</summary>

This usually means the defined server is no longer available. Remove it from your server list and try testing with a different server.

</details>

<details>

<summary>Server Selection - Failed to find a working test server. (NoServers)</summary>

Not 100% sure what causes this exception yet but it's likely when the CLI can't locate a local server. You should specify a list of servers to see if that addresses the issue.

</details>

<details>

<summary>Unable to retrieve Ookla servers, check internet connection and see logs.</summary>

This errors is shown when we try to retrieve the Ookla server list when selecting an server wehn running an manual speedtest. We get the list from: [https://www.speedtest.net/api/js/servers](https://www.speedtest.net/api/js/servers).&#x20;

This error is useually caused by a docker network problem or no internet connection. You can check the [container logs](error-messages.md#troubleshooting) for more details.&#x20;

</details>

### InfluxDB

<details>

<summary>Failed to bulk write to InfluxDB</summary>

When Speedtest Tracker fails to write data to InfluxDB this error is shown. The [container logs](error-messages.md#troubleshooting) will show more details on why it failed.&#x20;

**Possible reasons:**

* Connectivity problem to InfluxDB
* Problem with authentication
* Specified bucket does not exist in InfluxDB

</details>

<details>

<summary>Failed to write test data to InfluxDB.</summary>

When Speedtest Tracker fails to write data to InfluxDB this error is shown. The [container logs](error-messages.md#troubleshooting) will show more details on why it failed.&#x20;

**Possible reasons:**

* Connectivity problem to influxdb
* Problem with authentication
* Specified bucket does not exist in InfluxDB

</details>

<details>

<summary>Failed to write to InfluxDB.</summary>

When Speedtest Tracker fails to write data to InfluxDB this error is shown. The [container logs](error-messages.md#troubleshooting) will show more details on why it failed.&#x20;

**Possible reasons:**

* Connectivity problem to influxdb
* Problem with authentication
* Specified bucket does not exist in InfluxDB

</details>



