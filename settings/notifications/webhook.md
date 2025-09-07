# Webhook

A webhook will send a JSON payload to a receiver of your choice

<figure><img src="../../.gitbook/assets/webhook_notification.png" alt=""><figcaption><p>Webhook settings</p></figcaption></figure>

### Payload

Payload sent for a completed test

```json
{
  "result_id": 2,
  "site_name": "Speedtest Tracker",
  "server_name": "Speedtest",
  "server_id": 12345,
  "isp": "Speedtest Communications",
  "ping": 6.7,
  "download": 93281280,
  "upload": 28769728,
  "packet_loss": 0,
  "speedtest_url": "https://docs.speedtest-tracker.dev",
  "url": "http://localhost/admin/results"
}
```

Payload sent for a threshold failure

```json
{
  "result_id": 8,
  "site_name": "Speedtest Tracker",
  "service": "Ookla",
  "serverName": "Speedtest",
  "serverId": 12345,
  "isp": "Speedtest Communications",
  "metrics": [
    {
      "name": "Download",
      "threshold": "1000 Mbps",
      "value": "91.78 Mbps"
    },
    {
      "name": "Upload",
      "threshold": "1000 Mbps",
      "value": "28.18 Mbps"
    },
    {
      "name": "Ping",
      "threshold": "2 ms",
      "value": "6.41 ms"
    }
  ],
  "speedtest_url": "https://docs.speedtest-tracker.dev",
  "url": "http://localhost/admin/results"
}
```

### Triggers

<table><thead><tr><th width="237">Name</th><th>Description</th></tr></thead><tbody><tr><td>On completed speedtest</td><td>On each successful speedtest a notification will be send to the application.</td></tr><tr><td>On absolute threshold failure</td><td>On any absolute threshold failure a notification will be send to the application.</td></tr></tbody></table>
