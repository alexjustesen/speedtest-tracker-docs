# Mail

Notifications sent to the mail channel will be emailed to the list of recipients.

<figure><img src="../../.gitbook/assets/mail_notification.png" alt=""><figcaption><p>Mail settings</p></figcaption></figure>

### Triggers

| Name                          | Description                                                                       |
| ----------------------------- | --------------------------------------------------------------------------------- |
| On completed speedtest        | On each successful speedtest a notification will be send to the application.      |
| On absolute threshold failure | On any absolute threshold failure a notification will be send to the application. |

### Setting Up SMTP

Speedtest Tracker uses SMTP maill protocol to send email messages, you can use any service that allows you to send emails via SMTP.&#x20;

To configure the mail server settings you'll need to update the following variables in your `.env` file in your mounted data directory.

```
MAIL_HOST=mailhog
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
```
