# Nginx

[Nginx](https://nginx.org) can be used as a Reverse Proxy in front of Speedtest
Tracker to expose the Dashboard publicly with a trusted certificate.

First, you will need to add the `APP_URL` and `ASSET_URL` environment variables
to your `docker-compose.yml`.

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
            # Change both below to the desired domain
            - APP_URL=https://speedtest.yourdomain.com
            - ASSET_URL=https://speedtest.yourdomain.com
        volumes:
            - /path/to/data:/config
            - /path/to-custom-ssl-keys:/config/keys
        image: lscr.io/linuxserver/speedtest-tracker:latest
        restart: unless-stopped
```

Next, you will need to configure nginx to proxy to the Speedtest Tracker app.

{% hint style="info" %}
Depending on how you generate your SSL certificates and how you configure your
Docker network, you may need to adjust the `ssl_` and `proxy_pass` values.
{% endhint %}

```nginx
server {
        listen 80;
        server_name speedtest.yourdomain.com;
        return 301 https://$host$request_uri;
}

server {
        listen 443 ssl;
        server_name speedtest.yourdomain.com;

        ssl_certificate /etc/letsencrypt/live/speedtest.yourdomain.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/speedtest.yourdomain.com/privkey.pem;

        ssl_protocols TLSv1.2;
        ssl_ciphers
'ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA';
        ssl_prefer_server_ciphers on;
        ssl_session_cache shared:SSL:10m;
        ssl_session_timeout 10m;
        ssl_dhparam /etc/ssl/certs/dhparam.pem;

        add_header Strict-Transport-Security "max-age=31536000;includeSubdomains";

        location / {
                proxy_set_header X-Forwarded-Host $host;
                proxy_set_header X-Forwarded-Server $host;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;

                proxy_pass http://speedtest-container-host:80;
        }
}
```
