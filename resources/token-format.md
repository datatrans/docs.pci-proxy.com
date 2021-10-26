---
description: PCI Proxy token format overview
---

# Token format

PCI Proxy supports the following token formats:

### Alias 2.0

This format consists in numbers, letters, dash and underline.

\
When using the Alias 2.0 format we additionally return the parameter `fingerprint` from our APIs. It's a unique identifier for the underlying card. It helps you for example to identify customers who signed up with the same card number.

* example: AAABcH0Bq92s3kgAESIAAbGj5NIsAHWC
* format: AN32

### Masked Alias

This format consists of the first 6 digits of the real credit card number, the actual BIN Range (Bank Identification Number), followed by the token in form of 6 upper-case letters. The Masked Credit Card alias ends with the last 4 digits of the actual credit card number.\
Based on card brand the length of the token varies.

* example: 123456ABCDEF3456
* format: AN20

### Full substitution

This format consists of digits only.

* example: 1198182968382186732
* format: AN20

### Masked card number

Masked card number is returned with all APIs.

* example: 424242XXXXXX4242
* format AN20



{% hint style="warning" %}
Although all formats are supported and compliant according PCI DSS we highly recommend to use `Alias 2.0` format to run certain operations. Please refer to [Convert API](https://docs.pci-proxy.com/use-stored-cards/manage) if you want to migrate from a legacy to the new format.
{% endhint %}
