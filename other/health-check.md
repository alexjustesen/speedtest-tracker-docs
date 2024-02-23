# Health Check

Using the health check URL you can test to make sure the application is up and working. The URL `/api/healthcheck` will response with a 200 HTTP response code and a JSON message.

### Health Check Endpoint

```bash
curl {APP_URL}/api/healthcheck
```

You can also add this to your Docker Compose file so the Docker service can monitor that the container has started successfully.

```docker
healthcheck:
    test: curl -fSs {APP_URL}/api/healthcheck || exit 1
    interval: 10s
    retries: 3
    start_period: 30s
    timeout: 10s
```

### Response

```json
{"message":"Speedtest Tracker is running!"}
```
