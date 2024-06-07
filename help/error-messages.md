# Error Messages

### Speedtest errors

<details>

<summary>Could not resolve host.</summary>

This means the container can't reach the internet to run a speedtest successfully.

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

Not 100% sure what causes this exception  yet but it's likely when the CLI can't locate a local server. You should specify a list of servers to see if that addresses the issue.

</details>
