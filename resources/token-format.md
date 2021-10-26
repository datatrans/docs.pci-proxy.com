---
description: PCI Proxy token format overview
---

# Token format

PCI Proxy supports the following token format:

| Name               | Example                          | Format | Description                                                                                                                                                                                                                                                                                                                                      |
| ------------------ | -------------------------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Alias 2.0          | AAABcH0Bq92s3kgAESIAAbGj5NIsAHWC | AN32   | <p>This format consists in numbers, letters, dash and underline.<br></p><p>When using the Alias 2.0 format we additionally return the parameter <code>fingerprint</code> from our APIs. It's a unique identifier for the underlying card.<br><br>It helps you for example to identify customers who signed up with the same card number.</p>     |
| Masked Alias       | 123456ABCDEF3456                 | AN20   | <p>This format consists of the first 6 digits of the real credit card number, the actual BIN Range (Bank Identification Number), followed by the token in form of 6 upper-case letters.<br>The Masked Credit Card Token ends with the last 4 digits of the actual credit card number.<br>Based on card brand the length of the token varies.</p> |
| Full Substitution  | 1198182968382186732              | AN20   | This format consists of digits only.                                                                                                                                                                                                                                                                                                             |
| Masked Card Number | 424242XXXXXX4242                 | AN20   | Masked card number is returned with all APIs.                                                                                                                                                                                                                                                                                                    |

{% hint style="warning" %}
Although all formats are supported and compliant according PCI DSS we highly recommend to use `Alias 2.0` format to run certain operations. Please refer to [Convert API](https://docs.pci-proxy.com/use-stored-cards/manage) if you want to migrate from a legacy to the new format.
{% endhint %}
