# Mail

Notifications sent to the mail channel will be emailed to the list of recipients.

<figure><img src="../../.gitbook/assets/mail_notification.png" alt=""><figcaption><p>Mail settings</p></figcaption></figure>

### Setting Up SMTP

Speedtest Tracker uses SMTP mail protocol to send email messages, you can use any service that allows you to send emails via SMTP.

To configure the mail server settings you'll need to update the following variables in your `.env` file or add them to the environment variables passed into the container. When choosing mail scheme both `ssl` and `tls` protocols are supported and you'll want to check with your mail provider for which to use and which port.

{% hint style="warning" %}
Make sure these are not set in both your `.env` file or your `docker-compose.yml` file as that can cause issues.
{% endhint %}

```
MAIL_MAILER=smtp
MAIL_HOST=
MAIL_PORT=
MAIL_USERNAME=
MAIL_PASSWORD=
MAIL_FROM_ADDRESS=
MAIL_FROM_NAME=
```

{% hint style="info" %}
`MAIL_SCHEME` is optional, only use it if you need to define `smtp` or `smtps` otherwise Laravel will determine the scheme based on the port provided.
{% endhint %}

***

### Examples

#### Gmail

1. Go to [https://myaccount.google.com/](https://myaccount.google.com/) and click on the "Security" tab.
2. Under the "How you sign in to Google" section, click on "2-Step Verification".
3. Click on "App passwords".
4. Enter a name for your app password and click "Create". Use this password for the `MAIL_PASSWORD` env variable in the example configuration below.

```
MAIL_MAILER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=465
MAIL_USERNAME="username@gmail.com"
MAIL_PASSWORD="password"
MAIL_FROM_ADDRESS="username@gmail.com"
MAIL_FROM_NAME="Speedtest Tracker"
```

### Triggers

<table><thead><tr><th width="237">Name</th><th>Description</th></tr></thead><tbody><tr><td>on every scheduled speedtest run</td><td>On each successful scheduled speedtest a notification will be send to the application.</td></tr><tr><td>on threshold failures for scheduled speedtests</td><td>On any absolute threshold failure for scheduled speedtest  a notification will be send to the application.</td></tr></tbody></table>

### Recipients

A recipient is any valid email address, you can add one or many recipients that will receive notifications based on the triggers selected.
