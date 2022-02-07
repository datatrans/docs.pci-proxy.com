# Overview

Protect yourself against fraudulent transactions using our unique vendor-independent **3D Secure Authentication-Only** approach. Perform only the 3D Secure authentication with PCI Proxy and share 3DS authentication data with partners and payment gateways for payment authorization at a later stage.



PCI Proxy complies with the latest 3D Secure 2 standard from [EMVCo](https://www.linkedin.com/company/emvco/):

| Brand                                                       | Code  | Version         |
| ----------------------------------------------------------- | ----- | --------------- |
| ![](../.gitbook/assets/mastercard.svg)Mastercard            | `ECA` | >3-D Secure 2.0 |
| ![](../.gitbook/assets/visa.svg)Visa                        | `VIS` | >3-D Secure 2.0 |
| ![](../.gitbook/assets/card\_amex-old.svg) American Express | `AMX` | >3-D Secure 2.0 |
| ![](../.gitbook/assets/diners.svg)Diners Club               | `DIN` | >3-D Secure 2.0 |
| ![](../.gitbook/assets/discover.svg)Discover                | `DIS` | >3-D Secure 2.0 |
| ![](../.gitbook/assets/Dankort.png)Dankort                  | `DNK` | >3-D Secure 2.0 |

## Integration

Learn about PCI Proxy's integration choices for authenticating transactions:

{% content-ref url="3d-secure-fields-js/" %}
[3d-secure-fields-js](3d-secure-fields-js/)
{% endcontent-ref %}

{% content-ref url="3d-secure-mobile-sdks.md" %}
[3d-secure-mobile-sdks.md](3d-secure-mobile-sdks.md)
{% endcontent-ref %}

{% content-ref url="3d-secure-api.md" %}
[3d-secure-api.md](3d-secure-api.md)
{% endcontent-ref %}

## Dynamic 3D Secure

Our product **Dynamic 3D Secure** takes care of applying 3D Secure authentication only if your client's card issuer is from an EEA country. Based on the card number, we are able to identify if this is the case or not. While this product may reduce friction during checkouts, especially for countries where 3D Secure is not as dominant as it is in EEA countries, the liability shift protection will be completely missing for such transactions. We do recommend to enforce 3D Secure whenever possible. To activate Dynamic 3D Secure, please get in touch with your account manager at Datatrans or send us a [message](../help/contact.md).



## New to 3D Secure?&#x20;

Simply [drop us a message](https://www.pci-proxy.com/pci-proxy/contact/) if you're interested in taking advantage of **Authentication-Only** and our experts will reach out and find the best way how to proceed together with you. Please also check the following terminology page for&#x20;