---
description: Use PCI Proxy as a standalone authentication service for 3D Secure v2.
---

# 3D Secure v2

Secure Fields _Authentication Only_ integration allows you to securely collect sensitive card data \(card number and CVV code\) by injecting iframes to your DOM and perform an _Authentication Only_ call to validate a cardholder via 3D Secure v2. Decoupling _Authentication_ from _Authorization_ enables you to forward 3D data to an independent 3rd party payment provider. 

{% hint style="success" %}
A 3D Secure transaction can go either through a challenge or a frictionless flow.
{% endhint %}

If you decide to do Authorization with Datatrans payment gateway please continue with sending the payment request to our [Authorize](https://api-reference.datatrans.ch/#operation/authorize) API after finishing the authentication. 

{% hint style="success" %}
**Using Secure Fields qualifies you for SAQ A.**
{% endhint %}

If your business is located outside the European Economic Area \(EEA\) or if you don't need to apply 3D Secure process for another reason please go with our default [Secure Fields](authentication-only/securefields-1/) implementation. 

{% hint style="info" %}
You are a PCI Level 1 compliant company, running a native mobile application or simply want to separate card capturing and authentication flow? 

That's solved as well. Just have a look at our [Server-to-Server based approach](authentication-only/api-3d.md). 
{% endhint %}

### Dynamic 3D Secure 

Our product Dynamic 3D Secure takes care of applying 3D Secure authentication only if your client's card issuer is from an EEA country. Based on the card number, we are able to identify if this is the case or not. While this product may reduce friction during checkouts, especially for countries where 3D Secure is not as dominant as it is in EEA countries, the liability shift protection will be completely missing for such transactions. We do recommend to enforce 3D Secure whenever possible. To activate Dynamic 3D Secure, please get in touch with your account manager at Datatrans or send us a message by using our [contact form](https://www.pci-proxy.com/pci-proxy/contact/).

