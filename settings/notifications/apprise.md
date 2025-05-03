# Apprise

Speedtest Tracker uses [Apprise](https://github.com/caronc/apprise-api) to send notifications to a wide variety of messaging services with a simple, unified configuration.

Apprise allows you to easily deliver alerts to popular platforms such as Discord, Slack, Telegram  and many more.

{% hint style="warning" %}
To use Apprise notifications, you must deploy the [Apprise API](https://github.com/caronc/apprise-api) service. This is out of scope of this documentation.
{% endhint %}

<figure><img src="../../.gitbook/assets/apprise_notification.png" alt=""><figcaption><p>Apprise Settings</p></figcaption></figure>

<table><thead><tr><th width="200">Name</th><th width="535">Description</th></tr></thead><tbody><tr><td>URL</td><td>This is the URL of your running Apprise API instance </td></tr><tr><td>Service URL</td><td>This is the URL of the service that will receive the notification. You can find a full list of supported services and how to format their URLs in the <a href="https://github.com/caronc/apprise/wiki#notification-services">Apprise notification services documentation</a>.</td></tr></tbody></table>

### Triggers

<table><thead><tr><th width="237">Name</th><th>Description</th></tr></thead><tbody><tr><td>On completed speedtest</td><td>On each successful speedtest a notification will be send to the application.</td></tr><tr><td>On absolute threshold failure</td><td>On any absolute threshold failure a notification will be send to the application.</td></tr></tbody></table>

