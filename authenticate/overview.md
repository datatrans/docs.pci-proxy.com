# Overview

Protect yourself against fraudulent transactions using our unique vendor-independent <mark style="color:blue;">**3D Secure Authentication-Only**</mark> approach. Perform only the 3D Secure authentication with PCI Proxy and share 3DS authentication data with partners and payment gateways for payment authorization at a later stage.



PCI Proxy complies with the latest 3D Secure 2 standard from [EMVCo](https://www.linkedin.com/company/emvco/):

| Brand                                                                                                                    | Code  | Version        |
| ------------------------------------------------------------------------------------------------------------------------ | ----- | -------------- |
| <img src="../.gitbook/assets/mastercard.svg" alt="" data-size="line">Mastercard                                          | `ECA` | 3-D Secure 2.2 |
| <img src="../.gitbook/assets/visa.svg" alt="" data-size="line">Visa                                                      | `VIS` | 3-D Secure 2.2 |
| <img src="../.gitbook/assets/card_amex-old.svg" alt="" data-size="line"> American Express                                | `AMX` | 3-D Secure 2.2 |
| <img src="../.gitbook/assets/diners.svg" alt="" data-size="line">Diners Club                                             | `DIN` | 3-D Secure 2.1 |
| <img src="../.gitbook/assets/discover.svg" alt="" data-size="line">Discover                                              | `DIS` | 3-D Secure 2.1 |
| <img src="../.gitbook/assets/1200px-China-UnionPay-Logo.svg.png" alt="" data-size="line"> Union Pay                      | `CUP` | 3-D Secure 2.2 |
| <img src="../.gitbook/assets/Maestro_2016.svg.png" alt="" data-size="line">  Maestro                                     | MAU   | 3-D Secure 2.2 |
| <img src="../.gitbook/assets/Dankort.png" alt="" data-size="line">Dankort                                                | `DNK` | 3-D Secure 2.1 |
| <img src="../.gitbook/assets/logo_jcb.png" alt="" data-size="line"> JCB                                                  | `JCB` | 3-D Secure 2.2 |
| <img src="../.gitbook/assets/webimage-0D45FA73-E241-49FC-9F4CCF6FD9747B83.jpg" alt="" data-size="line"> Cartes Bancaires | `CBL` | 3-D Secure 2.2 |

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

Our product <mark style="color:blue;">**Dynamic 3D Secure**</mark> takes care of applying 3D Secure authentication only if your client's card issuer is from an EEA country. Based on the card number, we are able to identify if this is the case or not. While this product may reduce friction during checkouts, especially for countries where 3D Secure is not as dominant as it is in EEA countries, the liability shift protection will be completely missing for such transactions. We do recommend to enforce 3D Secure whenever possible. To activate Dynamic 3D Secure, please get in touch with your account manager at Datatrans or send us a [message](../help/contact.md).



## New to 3D Secure?&#x20;

Simply [drop us a message](../help/contact.md) if you're interested in taking advantage of <mark style="color:blue;">**Authentication-Only**</mark> and our experts will reach out and find the best way how to proceed together with you. Please also check the following terminology page for&#x20;
