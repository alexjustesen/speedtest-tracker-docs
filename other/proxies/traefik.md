# Traefik

[Traefik](https://traefik.io) can be used as a Reverse Proxy in front of Speedtest Tracker when you want to expose the Dashboard publicly with a trusted certificate. You will need at add the `APP_URL` envoirment and needed labels to the docker compose have Traefik apply the certificate and routing.

Docker-Compose:

```yaml
services:
    speedtest-tracker:
        container_name: speedtest-tracker
        environment:
            - PUID=1000
            - PGID=1000
            - APP_KEY=
            - DB_CONNECTION=sqlite
            - SPEEDTEST_SCHEDULE=
            - SPEEDTEST_SERVERS=
            - PRUNE_RESULTS_OLDER_THAN=
            - CHART_DATETIME_FORMAT= 
            - DATETIME_FORMAT=
            - APP_TIMEZONE=
            - APP_URL=https://speedtest.yourdomain.com # Change this to your domain name
            - ASSET_URL=https://speedtest.yourdomain.com # Change this to your domain name
        volumes:
            - /path/to/data:/config
            - /path/to-custom-ssl-keys:/config/keys
        labels:
            - "traefik.enable=true"
            - "traefik.http.routers.speedtest-tracker.rule=Host(`speedtest.yourdomain.com`)"
            - "traefik.http.routers.speedtest-tracker.entrypoints=websecure"
            - "traefik.http.routers.speedtest-tracker.tls=true"
            - "traefik.http.routers.speedtest-tracker.tls.certresolver=yourresolver"
            - "traefik.http.services.speedtest-tracker.loadbalancer.server.port=80"
        image: lscr.io/linuxserver/speedtest-tracker:latest
        restart: unless-stopped
```

{% hint style="info" %}
Depending on your Traefik configuration, you need to make sure the Speedtest Tracker and Traefik are on the same docker network.
{% endhint %}

<table><thead><tr><th width="291">Added compose part</th><th>Description</th></tr></thead><tbody><tr><td><code>APP_URL</code></td><td>URL you want to access the WebGui on.</td></tr><tr><td><code>ASSET_URL</code></td><td>URL used for loading all the needed assets. Need to be the same as the <code>APP_URL</code>.</td></tr><tr><td><code>traefik.enable=true</code></td><td>Explicitly tell Traefik to expose this container</td></tr><tr><td><code>traefik.http.routers.speedtest-tracker.rule=Host(`speedtest.yourdomain.com`)</code></td><td>The domain the service will respond to</td></tr><tr><td><code>traefik.http.routers.speedtest-tracker.entrypoints=websecure</code></td><td>Allow request only from the predefined entry point</td></tr><tr><td><code>traefik.http.routers.speedtest-tracker.tls=true</code></td><td>When a TLS section is specified, it instructs Traefik that the current router is dedicated to HTTPS requests only</td></tr><tr><td><code>traefik.http.routers.speedtest-tracker.tls.certresolver=yourresolver</code></td><td>Explicitly tell Traefik which Certificate provider to use matching your Traefik configuration</td></tr><tr><td><code>traefik.http.services.speedtest-tracker.loadbalancer.server.port=80</code></td><td>Explicitly tell Traefik port to use to connect to the container</td></tr></tbody></table>
