---
description: Setup for when using Traefik as a Reserve Proxy 
---

# Traefik Proxy

Traefik can be used as a Reverse Proxy in front of Speedtest Tracker when you want to expose the Dashboard publicly with a trusted certificate. You will need at add the `APP_URL` envoirment and needed labels to the docker compose have treafik apply the certificate and routing.

Docker-Compose:

```yaml
version: '3.4'
services:
    speedtest-tracker:
        container_name: speedtest-tracker
        environment:
            - PUID=1000
            - PGID=1000
            - DB_CONNECTION=sqlite
            - APP_URL=speedtest.yourdomain.com
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

<table><thead><tr><th width="261">Added compose part </th><th>Description</th></tr></thead><tbody><tr><td><code>APP_URL</code></td><td>URL you want to access the WebGui on.</td></tr><tr><td><code>traefik.enable=true</code></td><td>Explicitly tell Traefik to expose this container</td></tr><tr><td><code>traefik.http.routers.speedtest-tracker.rule=Host(`speedtest.yourdomain.com`)</code></td><td>The domain the service will respond to</td></tr><tr><td><code>traefik.http.routers.speedtest-tracker.entrypoints=websecure</code></td><td>Allow request only from the predefined entry point</td></tr><tr><td><code>traefik.http.routers.speedtest-tracker.tls=true</code></td><td>When a TLS section is specified, it instructs Traefik that the current router is dedicated to HTTPS requests only</td></tr><tr><td><code>traefik.http.routers.speedtest-tracker.tls.certresolver=yourresolver</code></td><td>Explicitly tell Traefik which Certificate provider to use matching your Traefik configuration </td></tr><tr><td><code>traefik.http.services.speedtest-tracker.loadbalancer.server.port=80</code></td><td>Explicitly tell Traefik port to use to connect to the container </td></tr></tbody></table>