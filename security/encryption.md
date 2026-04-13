# Encryption

### Application Key

An application key (`APP_KEY`) is used for encryption. It is a base64 encoded string that is used by Speedtest Tracker to encrypt and decrypt data, such as user sessions and other sensitive information and is required as part of the setup process.

Run the command below to generate your `APP_KEY`.

```bash
echo "base64:$(openssl rand -base64 32 2>/dev/null)"
```

{% hint style="info" %}
Some OpenSSL installs print a warning such as `can't open config file: etc/ssl/openssl.cnf` before the generated key. The command above suppresses that warning so you can copy a clean `APP_KEY` value.
{% endhint %}
