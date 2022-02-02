# API Authentication Data

The PCI Proxy APIs require different authentication methods depending on the called API:

* The **​**[**API Key**](api-authentication-data.md#api-key) - is used **only** for the following endpoints:
  * https://sandbox.pci-proxy.com/v1/pull
  * https://sandbox.pci-proxy.com/v1/push/uniquePushKey
* **​**[**Basic Authentication**](https://docs.pci-proxy.com/guides/pci-proxy-dashboard/api-authentication-data#basic-authentication) - is used for **all the other** endpoints.

See an overview below about which authentication method should be applied to protect your requests.

The productive authentication data can be accessed once you activated your account for production.

## API Key <a href="#api-key" id="api-key"></a>

Use your API key as the value for the `pci-proxy-api-key` HTTP header to send **PULL** requests. It is possible to create and name multiple API keys for each project.

You can obtain the API key within the Developers menu item in the Project section in the Dashboard.API Keys in PCI Proxy Dashboard.

![](../../.gitbook/assets/API-keys.png)

If you don’t have an [administrator role](user-management.md) you may not have access to view your API keys in the Dashboard. Contact someone in your organisation with appropriate access and ask to be added with required rights.

## Basic Authentication

Generate the Basic Authentication HTTP header using:

* `API Username / Merchant ID` as the basic authentication username value
* `API Password` as the basic authentication password value

You can obtain those values within the Developers menu item in the Project section in Dashboard.

![](<../../.gitbook/assets/basic authentication.png>)

Create a base64 encoded value of **API Username** and **API Password** (most HTTP clients are able to handle the base64 encoding automatically) and submit the Authorization header with each request. For example:

```
base64(merchantId:password) = MTAwMDAxMTAxMTpYMWVXNmkjJA==
```

```
Authorization: Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==
```

All API requests must be done over HTTPS with TLS >= 1.2.

