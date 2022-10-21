---
description: >-
  A Docker image to check your internet speed using Ookla's Speedtest service.
  Build using Laravel and the Speedtest CLI.
---

# 🐇 Speedtest Tracker

{% hint style="info" %}
These docs are up-to-date for version `0.1.0-alpha7`
{% endhint %}

{% hint style="warning" %}
Speedtest Tracker is in active development, during this "alpha" phase expect things to change and maybe break.
{% endhint %}

### Introduction

Speedtest Tracker runs a speedtest check against Ookla's Speedtest service on a schedule.

### Features

* Scheduled speedtest
* Ad-hoc speedtest
* Specify a speedtest server or use the default "closest" server
* Store results to your database of choice `sqlite`, `mariadb` / `mysql` or `postgresql`
