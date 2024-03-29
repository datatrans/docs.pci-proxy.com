---
description: Token format overview
---

# Token Formats

{% hint style="warning" %}
Although all formats are supported and compliant according to PCI DSS we highly recommend using the`Alias 2.0` format to run certain operations and obtain the maximum of security. \
\
Please refer to [Convert API](../store/manage/convert.md) if you want to migrate from a legacy to the new format.&#x20;
{% endhint %}

## Alias 2.0

The Alias 2.0 is our default token format. All the tokens are unique. When using the Alias 2.0 format we additionally return the parameter  `fingerprint` from our APIs. It's a unique identifier for the underlying card. This allows you to identify the same card usage across different customer accounts.&#x20;

| Input                 | Output                                                              |
| --------------------- | ------------------------------------------------------------------- |
| `4242 4242 4242 4242` | <mark style="color:blue;">`AAABcH0Bq92s3kgAESIAAbGj5NIsAHWC`</mark> |

* Possible characters: `A-Z`, `a-z`, `0-9`, `-`, `_`
* Length: `32`
* Supported features:
  * [Network Tokenisation ](../advanced-features/network-tokenization/)
  * [Manage API](../store/manage/)
  * Fingerprint

## Alias 2.0 - Length preserving&#x20;

The Alias 2.0 - Length preserving format inherits all features and functionalities of the original Alias 2.0 format with the difference that the length of the alias equals the length of the original card number.&#x20;

| Input                 | Output                                              |
| --------------------- | --------------------------------------------------- |
| `4242 4242 4242 4242` | <mark style="color:blue;">`AEcyq81HSCWWGihU`</mark> |

* Possible characters: `A-Z`, `a-z`, `0-9`, `-`, `_`
* Length: `[12, 19]`, based on underlying card length
* Supported features:
  * [Network Tokenisation ](../advanced-features/network-tokenization/)
  * [Manage API](../store/manage/)
  * Fingerprint

## CVV/CVC Alias

All the tokens are unique. All payment methods share a common token format:

* Sensitive Authentication Data (CVV/CVC)
* Personal Data

| Input                         | Output                                                      |
| ----------------------------- | ----------------------------------------------------------- |
| `123`                         | <mark style="color:blue;">`Glb62cRnQV0jJxI0Iaeq9Wme`</mark> |

* Possible characters: `A-Z`, `a-z`, `0-9`, `-`, `_`
* Length: `24`

## Masked Alias

This format consists of the first 6 digits of the real credit card number, the actual BIN Range (Bank Identification Number), followed by the token in form of 6 upper-case letters. The Masked Credit Card alias ends with the last 3-4 digits of the actual credit card number. Based on the card brand the length of the token varies.

| Input                                         | Output                                              |
| --------------------------------------------- | --------------------------------------------------- |
| `4242 4242 4242 4242`                         | <mark style="color:blue;">`424242ABCDEF4242`</mark> |

* Possible characters: `A-Z`, `0-9`,&#x20;
* Length: `length preserving`

## Full Substitution

This format consists digits only

| Input                                         | Output                                                 |
| --------------------------------------------- | ------------------------------------------------------ |
| `4242 4242 4242 4242`                         | <mark style="color:blue;">`1198182968382186732`</mark> |

* Possible characters: `0-9`
* Length: `20`

