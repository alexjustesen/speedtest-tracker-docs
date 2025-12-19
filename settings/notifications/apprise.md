# Apprise

Apprise provides a unified notification channel that lets you send alerts to numerous services—like Discord, Pushover, and Ntfy as well as many additional platforms

### Why Apprise

Apprise allows the application to sent notifications to a wide variety of services. It let us focus on features instead of maintaining X number of notification channels. Essentially helping us cut down on maintenance/feature requests.

### Apprise Server

To use Apprise, you’ll need to set up your own Apprise instance. This container isn’t created automatically, so make sure to include it in your deployment. See the Apprise [Github Repo](https://github.com/caronc/apprise-api) for the setup instructions. On the notification page you will need to define the location of your Apprise instance. Make sure this instance is reachable for the Speedtest Tracker.

{% hint style="info" %}
We don't offer support on setting up Apprise, incase of any problems with the Apprise Container please reach out to the Apprise team.&#x20;
{% endhint %}

### Notification Channels

Notification channels are the formatted URLs used by Apprise to send notifications to various services. Refer to the [Apprise documentation](https://github.com/caronc/apprise?tab=readme-ov-file#supported-notifications) for a full list of supported channels and their required formats. You can add as many different channels as you wish. The notifications will be sent to all of them.&#x20;

### Tips and Tricks

#### Format

By default the format used for message is `markdown`  This allows us to do some formatting on the message like bold text etc.

#### Preview Images

By default Apprise does not allow preview images for URLs. This is an default setting on the Apprise instance. Depending on the service used you can override this settings in the notification channel URL. Check the Apprise documentation to see if your service support this and how to set it.&#x20;

### Triggers

<table><thead><tr><th width="237">Name</th><th>Description</th></tr></thead><tbody><tr><td>on every scheduled speedtest run</td><td>On each successful scheduled speedtest a notification will be send to the application.</td></tr><tr><td>on threshold failures for scheduled speedtests</td><td>On any absolute threshold failure for scheduled speedtest a notification will be send to the application.</td></tr></tbody></table>
