# Speedtest Process

Speedtest Tracker uses the [Official Ookla CLI](https://www.speedtest.net/apps/cli) client to execute the speedtest. There a couple of stages the Speedtest Tracker goes through, below explains the process.

{% stepper %}
{% step %}

#### Waiting

The speedtest run request was created but has not been started.
{% endstep %}

{% step %}

#### Started

The speedtest process has been started by a queue worker.
{% endstep %}

{% step %}
#### Checking

The application checks for an internet connection by calling `https://icanhazip.com`
{% endstep %}

{% step %}
#### Skipped \[Optional]

If you have the `SPEEDTEST_SKIP_IPS` the test will be marked as skipped as the IP returning during `Checking` matches your defined IP.
{% endstep %}

{% step %}
#### Running

The application runs the speedtest by simply running the speedtest command. This command runs the speedtest like another other speedtest and returns the result in json format so the application an easily process it.

```
speedtest -accept-license --accept-gdpr --format=json
```

Or when you have defined a server id:

```
speedtest -accept-license --accept-gdpr --format=json --server-id=YOURSERVERID
```
{% endstep %}

{% step %}
#### Failed

If for various reasons the Ookla CLI returns an error, because the defined server was offline for example the tests is marked as failed. As well when the `Checking` stage fails when there is no internet.
{% endstep %}

{% step %}
#### Benchmarking

When you have thresholds set this step will evaluate the results against the threshold to determine if the test was healthy or not.
{% endstep %}

{% step %}
#### Completed

This is the end stage of the process when every step is completed the test is marked as such.
{% endstep %}
{% endstepper %}
