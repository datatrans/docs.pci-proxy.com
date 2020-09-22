---
description: PCI Proxy token format overview
---

# Token format

PCI Proxy supports the following token format: 

| Name | Example | Format | Description |
| :--- | :--- | :--- | :--- |
| Alias 2.0 | AAABcH0Bq92s3kgAESIAAbGj5NIsAHWC | AN32 | This format consists numbers, letters and special characters.  |
| Masked Alias | _123456ABCDEF3456_ | AN20 | This format consists of the first 6 digits of the real credit card number, the actual BIN Range \(Bank Identification Number\), followed by the token in form of 6 upper-case letters. The Masked Credit Card Token ends with the last 4 digits of the actual credit card number. Based on card brand the length of the token varies.  |
| Full Substitution | _1198182968382186732_ | AN20 | This format consists of digits only.  |
| Masked Card Number | _424242XXXXXX4242_ | AN20 | Masked card number is returned on all APIs.  |

{% hint style="warning" %}
Although all formats are supported and compliant according PCI DSS we highly recommend to use `Alias 2.0` format to run certain operations. Please refer to [Convert API](../use-stored-cards/) if you want to migrate from a legacy to the new format. 
{% endhint %}



