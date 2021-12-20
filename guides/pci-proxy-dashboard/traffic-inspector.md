---
description: Monitor and debug traffic in real time
---

# Traffic Inspector

The Traffic Inspector allows you to monitor and debug traffic on a specific integration in real time.\
It allows you to see the entire stream of a request sent through PCI Proxy as well you can access payload data and see what's sent to and returned by a target. Simply navigate to the `Traffic Inspector` menu on the left hand side menu bar or access it within the `Developers` menu directly and activate the logging for 15 minutes to help you to introspect the traffic and to adjust your integration or payload accordingly.

{% hint style="info" %}
Due to logging of sensitive cardholder data the Traffic Inspector is currently available on Sandbox environment only.
{% endhint %}

### Activate the Traffic Inspector

To activate the record function choose an integration assigned to your account and hit the Start recording button.

![How to activate traffic logging](<../../.gitbook/assets/image (15).png>)

### Get an overview about logged requests

Once you sent data to the PCI Proxy API wait until the record has been loaded into the dashboard to see an overview of the collected request. This overview displays some basic information like target HTTP status code, target URI, timestamp or number of applied Conversions.

You can have multiple activated sessions (integrations). Choose the sessions you want to view data in the top right menu by simply clicking on it.

![Request overview](<../../.gitbook/assets/image (16).png>)

### View detailed request data

To access the entire stream of a request simply click on the record you want to view. Once done you can view request specific data of the payload like HTTP properties, multiple Headers and the Body of the request and response. All those information are grouped as a stream. From the very beginning of the request until the end you see all performed operations including internal PCI Proxy application processing time.

![Request data](<../../.gitbook/assets/image (17).png>)
