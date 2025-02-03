# Latest Result (deprecated)

{% hint style="warning" %}
This endpoint is deprecated and will be removed in a future release.
{% endhint %}

### Authentication

No authentication required.

### Get the latest speedtest result

<mark style="color:blue;">`GET`</mark> `/api/speedtest/latest`

Provides backwards compatibility for [Homepage](https://github.com/benphelps/homepage) and [Organizr](https://github.com/causefx/Organizr) home lab dashboards.

{% hint style="info" %}
Homepage now [supports](https://github.com/gethomepage/homepage/pull/4695) the latest API spec which requires a token.
{% endhint %}



{% tabs %}
{% tab title="200: OK " %}
```javascript
{
    "message": "ok",
    "data": {
        "id": 1,
        "ping": 11.111,
        "download": 694.20,
        "upload": 420.69,
        "server_id": 12345,
        "server_host": "host.of.server.com",
        "server_name": "Name of Server",
        "url": "https://www.speedtest.net/result/c/slug-to-results",
        "scheduled": false,
        "failed": true,
        "created_at": "2023-03-10T13:17:46.000000Z",
        "updated_at": "2023-03-10T13:17:46.000000Z"
    }
}
```
{% endtab %}

{% tab title="404: Not Found " %}
```javascript
{
    "message": "No results found."
}
```
{% endtab %}
{% endtabs %}
