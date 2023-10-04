# Latest Result

### Legacy Endpoints

#### Authentication

No authentication required.

{% swagger method="get" path="" baseUrl="/api/speedtest/latest" summary="Get the latest speedtest result" expanded="false" %}
{% swagger-description %}
Provides backwards compatibility for [Homepage](https://github.com/benphelps/homepage) and [Organizr](https://github.com/causefx/Organizr) home lab dashboards.
{% endswagger-description %}

{% swagger-response status="200: OK" description="" %}
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
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="" %}
```javascript
{
    "message": "No results found."
}
```
{% endswagger-response %}
{% endswagger %}
