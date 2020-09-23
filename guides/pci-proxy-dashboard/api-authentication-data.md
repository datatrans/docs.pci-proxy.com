---
description: Access PCI Proxy API authentication data
---

# API Authentication data

The PCI Proxy APIs require different authentication methods depending on the called API: 

* \*\*\*\*[**API Key**](api-authentication-data.md#api-key) - is used **only** for the following endpoints:
  * https://sandbox.pci-proxy.com/v1/pull
  * https://sandbox.pci-proxy.com/v1/push/uniquePushKey
* \*\*\*\*[**Basic Authentication**](api-authentication-data.md#basic-authentication) **** - is used for **all other** endpoints.

See an overview below about which authentication method should be applied to protect your requests. 

{% hint style="info" %}
The productive authentication data can be accessed once you activated your account for production. 
{% endhint %}

## API Key

Use your API key as the value for the `pci-proxy-api-key` HTTP header to send **PULL/PUSH** requests.   
It is possible to create and name multiple API keys each project. 

You can obtain the API key menu within the Developers menu item in the Project section in the Dashboard. 

![API Keys in PCI Proxy Dashboard](../../.gitbook/assets/image%20%281%29.png)

If you don’t have an [administrator role ](account-structure-user-management.md#user-management)you may not have access to view your API keys in the Dashboard. Contact someone of your organisation with appropriate access and ask to be added with required rights. 

## Basic Authentication

Generate the Basic Authentication HTTP header using: 

* `API Username / Merchant ID` as the basic authentication username value 
* `API Password` as the basic authentication password value

You can obtain those values within the Developers menu item in the Project section in Dashboard. 

![API Username &amp; API Password in PCI Proxy Dashboard](../../.gitbook/assets/2020-07-21-15_43_25-window.png)

Create a base64 encoded value of **API Username** and **API Password** \(most HTTP clients are able to handle the base64 encoding automatically\) and submit the Authorization header with each request. For example:

```text
base64(merchantId:password) = MTAwMDAxMTAxMTpYMWVXNmkjJA==
```

```text
Authorization: Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==
```

{% hint style="info" %}
All API requests must be done over HTTPS with TLS &gt;= 1.2.
{% endhint %}

