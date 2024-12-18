# Encryption

### Application Key

An application key (`APP_KEY`) is used for encryption. It is a base64 encoded string that is used by Speedtest Tracker to encrypt and decrypt data, such as user sessions and other sensitive information and is required as part of the setup process.

You can either get a generated key on [https://speedtest-tracker.dev/](https://speedtest-tracker.dev/) or run the command below:

```bash
echo -n 'base64:'; openssl rand -base64 32;
```

