# Error Messages

### Speedtest errors

<details>

<summary>Tests are saying there is no internet while there is.</summary>

When a speedtest is being processed Speedtest Tracker will make a call to [http://icanhazip.com](http://icanhazip.com) to get your external IP address. This is done to determine if your server has access to the internet and to check if your external IP address (WAN IP) should be skipped.

Some DNS blocks lists will block this domain, if you're getting errors and your server has access to the internet you'll need to add this to your allow lists.

</details>

### Ookla errors

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
