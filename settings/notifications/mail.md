# Mail

Notifications sent to the mail channel will be emailed to the list of recipients.

<figure><img src="../../.gitbook/assets/mail_notification.png" alt=""><figcaption><p>Mail settings</p></figcaption></figure>

### Setting Up SMTP

Speedtest Tracker uses SMTP mail protocol to send email messages, you can use any service that allows you to send emails via SMTP.&#x20;

To configure the mail server settings you'll need to update the following variables in your `.env` file in your mounted data directory.

```
MAIL_HOST=mailhog
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
```

### Triggers

<table><thead><tr><th width="237">Name</th><th>Description</th></tr></thead><tbody><tr><td>On completed speedtest</td><td>On each successful speedtest a notification will be send to the application.</td></tr><tr><td>On absolute threshold failure</td><td>On any absolute threshold failure a notification will be send to the application.</td></tr></tbody></table>

### Recipients

A recipient is any valid email address, you can add one or many recipients that will receive notifications based on the triggers selected.
