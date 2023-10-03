---
description: >-
  Speedtest Tracker supports multiple cache drivers, use the docs below to setup
  your preferred handler.
---

# Caching

## Drivers

You can change your cache driver by setting the environment variable in your configuration file. To change the default driver pass `CACHE_DRIVER` as an environment variable.

### File (default)

{% hint style="info" %}
`v0.13.1` contains a change to `file` as the default driver to improve performance.
{% endhint %}

This is the default cache driver and fine in most use cases, especially if the container runs on the same host system.

### Database

Using the database cache driver can be used if you're running multiple instances and want to share the cache.&#x20;

Change `CACHE_DRIVER` to `database` in your environment variables.

### Redis

Using Redis cache driver can also be used if you're running multiple instances or don't want to use the container's file system as the cache.&#x20;

Change `CACHE_DRIVER` to `redis` in your environment variables.
