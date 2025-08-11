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
MAIL_HOST=mailhog
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="Speedtest Tracker"
MAIL_SCHEME=null
```

**GMAIL example:**

Steps for creating an app password.

* Go to your [Google Account](https://myaccount.google.com) .
* Select Security.
* Under "How you sign in to Google," choose 2-Step Verification.
* Click on App passwords.
* Enter a name and generate a password.
* Remember to copy the password before closing; otherwise, you'll need to create another one.

```
MAIL_MAILER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=465
MAIL_USERNAME=username@gmail.com
MAIL_PASSWORD="password"
MAIL_FROM_ADDRESS="username@gmail.com"
MAIL_FROM_NAME="Speedtest Tracker"
MAIL_SCHEME=tls
```

### Triggers

<table><thead><tr><th width="237">Name</th><th>Description</th></tr></thead><tbody><tr><td>On completed speedtest</td><td>On each successful speedtest a notification will be send to the application.</td></tr><tr><td>On absolute threshold failure</td><td>On any absolute threshold failure a notification will be send to the application.</td></tr></tbody></table>

### Recipients

A recipient is any valid email address, you can add one or many recipients that will receive notifications based on the triggers selected.
