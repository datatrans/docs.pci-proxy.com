---
description: Use the PCI Proxy Show API to display sensitive card data
---

# Show

PCI Proxy show enables your end users to reveal the underlying credit card number or CVV code of a previously created Card or CVV token directly in your application without ever touching your servers. It offloads the PCI DSS burden and reduces your scope to a minimum.&#x20;

PCI Proxy Show comes with two fully configurable iframes hosted by PCI Proxy. The iframes can be embedded into your HTML to show cardholder data and allow you to control styling and layout to match the user interface of the application. They also provide transparent button UI elements to copy card number and CVV code to the clipboard.&#x20;

{% hint style="danger" %}
Before you start with the integration please carefully read the [Security and Compliance](security-and-compliance.md) section.
{% endhint %}

\
Depending on your use-case, we offer the following two integration methods:

1. [Display card data in web applications](web/)
2. [Display card data in native mobile applications](native-mobile-apps.md)
