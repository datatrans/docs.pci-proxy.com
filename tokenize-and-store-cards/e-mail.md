---
description: Securely collect carda data directly via email.
---

# E-Mail

Let us assume you have an offer for your customers and you want to collect the card data directly via email. Just generate a payment link and copy it into your email. Your customers can click on the link and our payment page is opened. They can choose their favorite payment method and pay directly.

Our PayByEmailService allows you to generate Pay-by-Email payment links.

## Generate payment links

{% api-method method="post" host="" path="" %}
{% api-method-summary %}
XML\_PayByEmail
{% endapi-method-summary %}

{% api-method-description %}
PayByEmailService allows you to generate Pay-by-Email payment links.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="merchantId" type="number" required=true %}
Unique merchant identifier \(allocated at signup\)
{% endapi-method-parameter %}

{% api-method-parameter name="language" type="string" required=false %}
Define language in which payment page will be opened
{% endapi-method-parameter %}

{% api-method-parameter name="" type="string" required=false %}
kjhkh
{% endapi-method-parameter %}

{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="duedate" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter type="number" name="merchantId" %}
Unique Merchant Identifier \(allocated by Datatrans at merchant registration process\)
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

| **PayByEmailService Endpoint:** |
| --- |
| [https://pay.sandbox.datatrans.com/upp/jsp/XML\_PayByEmail](https://pay.sandbox.datatrans.com/upp/jsp/XML_PayByEmail) |

**Just send the following payload to our PayByEmailService Endpoint:**

```markup
<?xml version="1.0" encoding="UTF-8" ?>
  <payByEmailService version="1">
    <body merchantId="1000011011">
      <language>en</language>
      <currency>eur</currency>
      <amount>400</amount>
      <refno>XML test</refno>
      <duedate>20151231</duedate>
    </body>
  </payByEmailService>
```

_Duedate should be in the yyyymmdd format._

**As a response you receive the payment link:**

```markup
<?xml version="1.0" encoding="UTF-8"?>
  <payByEmailService version="1">
    <body merchantId="1000011011">
      <payByEmailURL>https://pay.sandbox.datatrans.com/upp/jsp/upStartFromTemplate?paymentTemplateId=021935b9-
54fb-f8f8-0000-015191015e03</payByEmailURL>
    </body>
  </payByEmailService>
```

_Note: In test mode, only test credit cards are allowed!_

> ## Congrats, Level 2 completed: Your server is out of PCI scope!
>
> You have securely captured sensitive card data through email without sensitive data touching your servers. **Your systems never record, transmit or store real credit card data, only the token.** **Thus, you are out of PCI scope.** Move on and learn how you can use stored card data. Please continue to [**Step 3**](../use-stored-cards/).
>
> ### Questions?
>
> Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.
>
> Phone: +41 44 256 81 91  
> Email: [support@pci-proxy.com](mailto:support@pci-proxy.com)

