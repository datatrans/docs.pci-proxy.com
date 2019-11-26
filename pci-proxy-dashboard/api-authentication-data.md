---
description: Access PCI Proxy API authentication data
---

# API Authentication data

The PCI Proxy APIs requires different authentication methods depending on the used API. See and overview below which authentication method should be applied to protect your requests.   
  
Simply navigate to the **Developers** menu in the **Project section** to reveal and setup the API Keys and passwords for your project. 

{% hint style="info" %}
The productive authentication data can be accessed once you activated your account for production. 
{% endhint %}

  
PULL/PUSH Proxy API requries `pci-proxy-api-key` sent as a HTTP header.   
  
All other APIs requires HTTP Basic Authentication.  Provide your `merchantId` as the basic authentication username value and the API Password as password.   
  
Create a base64 encoded value of merchantId and password \(most HTTP clients are able to handle the base64 encoding automatically\) and submit the Authorization header with each request. For example:

```text
base64(merchantId:password) = MTAwMDAxMTAxMTpYMWVXNmkjJA==
```

```text
Authorization: Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==
```

All API requests must be done over HTTPS with TLS &gt;= 1.2

