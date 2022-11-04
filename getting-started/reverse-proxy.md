# Reverse Proxy

## Traefik

1. Download the [SSL certificate export script](https://blog.cubieserver.de/2021/minimal-traefik-v2-certificate-export/) to export SSL certificates stored in `acme.json` to physical `ssl.cert` and `ssl.key` files.

2. Adjust the variables as necessary
    1. `TRAEFIK_CERT_STORE`: the location of the `.json` file containing the SSL certificate information; the default location is `acme.json`
    2. `TRAEFIK_RESOLVER`: The resolver used by Traefik for certificates. This should match the `certResolver` defined in the Traefik config.
    3. `OUTPUT_DIR`: Where to export the certificate files
 
3. Run the script - `sh ./export-traefik-v2-certificate.sh DOMAIN` where `DOMAIN` is your domain that has the certificates you wish to export.

4. Add a volume map of the `OUTPUT_DIR` in 2.3 above to `/etc/ssl/web` to your `speedtest-tracker` container

5. The `speedtest-tracker` Traefik configuration should utilize a TCP router with TLS passthrough enabled; do NOT use a HTTP router. 

    ex: `traefik.tcp.routers.speedtest-tracker.tls.passthrough=true`