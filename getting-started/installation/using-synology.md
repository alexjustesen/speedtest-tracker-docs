---
description: >-
  These instructions will run you through setting up Speedtest Tracker on a
  Synology NAS using Container Manager.
---

# Using Synology

{% hint style="warning" %}
The following directions are for the old "Docker" application, if you're using "Container Manager" you can follow the docker compose instructions in [using-docker-compose.md](using-docker-compose.md "mention").
{% endhint %}

### Install on a Synology NAS

Open the Docker interface of your Synology Device, search for `ajustesen/speedtest-tracker` in the Registry and download it.

![download\_image](https://user-images.githubusercontent.com/92191413/210480118-b15f83af-6617-4a0d-b631-760f419425b9.png)

Create a local directory (i.e. `/volume1/docker/speedtest-tracker`) which later can be mapped to the docker container.

Launch the image once the download is completed.

![launch\_image](https://user-images.githubusercontent.com/92191413/210480210-baa06b52-c3b0-41a4-b50e-ce7af82d683c.png)

Map the ports to available ports.

![port\_mapping](https://user-images.githubusercontent.com/92191413/210481629-6fa76992-403a-415e-9967-af7b00c97d87.png)

{% hint style="info" %}
Make sure the ports you choose are not used by any other application or DSM service on your device and remember to adjust the Synology Firewall settings accordingly.
{% endhint %}

Map the directory you created earlier to the mount path `/config`.

![volume\_mapping](https://user-images.githubusercontent.com/92191413/210480901-069703e3-c6ab-446c-b53b-8c5ef3c87085.png)

Review your settings and click "done".

![summary](https://user-images.githubusercontent.com/92191413/210480977-3e24ba39-b23e-463f-acba-0a1aad1e57ec.png)

You can now access Speedtest-Tracker via `http://YOUR_IP_ADDRESS:8080` or `https://YOUR_IP_ADDRESS:8443`.
