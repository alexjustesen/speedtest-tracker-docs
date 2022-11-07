# Reverse Proxy

## Traefik

1. In the dynamic file config, enable skip verification of the endpoint's SSL certificate:
    ```
        http:
            ...
            serversTransports:
                ignorecert:
                    insecureSkipVerify: true
    ```
2. Within your docker config, use the following configuration:
    ```
      - traefik.http.services.{name}.loadbalancer.serversTransport=ignorecert@file
      - traefik.http.services.{name}.loadbalancer.server.scheme=https
      - traefik.http.routers.{name}.tls=true
    ```