---
description: Use PCI Proxy as a standalone authentication service for 3D Secure v1 and v2.
---

# 3D Secure 1/2

SecureFields Authenticate only integration allows you to securely collect sensitive card data \(cardnumber and CVV code\) by injecting iframes to your DOM and perfom an authenticate only call to check a cardholder for 3D Secure v1 and v2. Decoupling authentication and authorization process enables you to forward 3D data to an independent 3rd party payment provider. 

If you decide to do the authorisation with Datatrans payment gateway please continue with sending payment request to our [Authorize](../../use-stored-cards/authorize.md) API. 

A 3D Secure transaction either can go through a challenge or a frictionless flow. In case the issuer does not support 3D Secure 2 we automatically apply a fallback to 3D Secure 1. 

{% hint style="info" %}
**Using Secure Fields qualifies you for SAQ A.**
{% endhint %}

If your business is located outside the European Economic Area \(EEA\) or if you don't need to apply 3D Secure process for another reason please go with our default [SecureFields ](../../collect-and-store-cards/capture-iframes/)implementation. 

