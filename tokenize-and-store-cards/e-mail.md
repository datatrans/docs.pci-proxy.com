---
description: Securely collect card data via a temporary payment link.
---

# Capture \(email\)

PayByEmail allows you to capture credit card data directly through a payment link that is sent via email. Just generate a temporary payment link and copy it into your email. Your customers can click on the link and our payment page is opened. They can choose their preferred payment method and pay directly.

{% api-method method="post" host="https://pay.sandbox.datatrans.com" path="/upp/jsp/XML\_PayByEmail" %}
{% api-method-summary %}
PayByEmail
{% endapi-method-summary %}

{% api-method-description %}
Th PayByEmail service generates a temporary payment link.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Content-Type" type="string" required=false %}
API consumes application/xml
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="merchantId" type="string" required=false %}
Your unique account id at PCI Proxy \(e.g. 1000011011\)
{% endapi-method-parameter %}

{% api-method-parameter name="language" type="string" required=false %}
Language in which payment page is shown \(e.g. en\)
{% endapi-method-parameter %}

{% api-method-parameter name="currrency" type="string" required=false %}
Currency in which amount is shown \(e.g. eur\)
{% endapi-method-parameter %}

{% api-method-parameter name="amount" type="string" required=false %}
Transaction amount in cents \(e.g. 123.50 = 12350\)
{% endapi-method-parameter %}

{% api-method-parameter name="refno" type="string" required=false %}
Your reference number \(defined by you - AN18\)
{% endapi-method-parameter %}

{% api-method-parameter name="duedate" type="string" required=false %}
Duration payment link is active \(format: YYYYMMDD\)
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
You receive a temporary payment link
{% endapi-method-response-example-description %}

```javascript
<?xml version="1.0" encoding="UTF-8"?>
  <payByEmailService version="1">
    <body merchantId="1000011011">
      <payByEmailURL>https://pay.sandbox.datatrans.com/upp/jsp/upStartFromTemplate?paymentTemplateId=021935b9-
54fb-f8f8-0000-015191015e03</payByEmailURL>
    </body>
  </payByEmailService>
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Examples

{% code-tabs %}
{% code-tabs-item title="Example Request" %}
```bash
curl "https://api.sandbox.datatrans.com/upp/jsp/XML_PayByEmail" \
  -H "Content-Type: text/xml" \
  -d '<?xml version="1.0" encoding="UTF-8"?>
        <payByEmailService version="1">
          <body merchantId="1000011011">
            <language>en</language>
            <currency>eur</currency>
            <amount>400</amount>
            <refno>XML test</refno>
            <duedate>20151231</duedate>
          </body>
        </payByEmailService>'
```
{% endcode-tabs-item %}

{% code-tabs-item title="Example Response" %}
```markup
<?xml version="1.0" encoding="UTF-8"?>
  <payByEmailService version="1">
    <body merchantId="1000011011">
      <payByEmailURL>https://pay.sandbox.datatrans.com/upp/jsp/upStartFromTemplate?paymentTemplateId=021935b9-
54fb-f8f8-0000-015191015e03</payByEmailURL>
    </body>
  </payByEmailService>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="warning" %}
In test mode, only [test credit cards](../setup/sandbox-account.md) are allowed.
{% endhint %}

## Next up

{% page-ref page="../use-stored-cards/" %}



