# Tailscale

[Tailscale](https://tailscale.com) Mesh VPN service can be used as an sidecar container to access the Speedtest Tracker within your Tailnet on its own MagicDNS name.

## Tailscale Auth key

Generate an auth key for tailscale so the docker container can access your tailnet.

1. Open the [**Keys**](https://login.tailscale.com/admin/settings/keys) page of the admin console.
2. Select **Generate auth key**.
3. Fill out the form fields to specify characteristics about the auth key, such as the description, whether its reusable, when it expires, and device settings.
4. Select **Generate key**.

Save this Auth Key. We will need this later on.

## Docker Configuration

Docker-Compose:

```yaml
services:
  tailscale-speedtest:
    image: tailscale/tailscale
    container_name: tailscale_speedtest-tracker
    hostname: speedtest
    environment:
      - TS_AUTHKEY=
      - TS_STATE_DIR=/var/lib/tailscale
      - TS_USERSPACE=false
    volumes:
      - ./tailscale-traefik/state:/var/lib/tailscale
      - /dev/net/tun:/dev/net/tun
    cap_add:
      - net_admin
      - sys_module
    restart: unless-stopped

  speedtest-tracker:
    container_name: speedtest-tracker-tailscale
    depends_on:
      - tailscale-speedtest
    network_mode: service:tailscale-speedtest
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
        - APP_URL=https://speedtest.yourtailnet.ts.net # Change this to your MagicDNS name
        - ASSET_URL=https://speedtest.yourtailnet.ts.net # Change this to your MagicDNS name
    volumes:
        - /path/to/data:/config
        - /path/to-custom-ssl-keys:/config/keys
    image: lscr.io/linuxserver/speedtest-tracker:latest
    restart: unless-stopped
```

| Added compose part | Description                                                                             |
| ------------------ | --------------------------------------------------------------------------------------- |
| `APP_URL`          | URL you want to access the WebGui on. This will need to be the Tailscale Magic DNS name |
| `ASSET_URL`        | URL used for loading all the needed assets. Need to be the same as the `APP_URL`.       |
| `TS_AUTHKEY`       | Auth key for Tailscale                                                                  |
