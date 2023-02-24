---
description: >-
  Request detailed information about an alias such as creation date, fingerprint
  or card meta data.
---

# Status

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/aliases/{alias}" method="get" summary="STATUS" %}
{% swagger-description %}
The parameters marked with * are mandatory.
{% endswagger-description %}

{% swagger-parameter in="path" name="alias" type="string" required="true" %}
Alias 2.0 format received from a previous inbound channel
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-response status="200" description="Status successfully returned" %}
```javascript
{
    "alias": "AAABeM8amw3ssdexyrAAAYwp9fXrAIkp",
    "fingerprint": "F-dV5V8dE0SZLoTurWbq2HZp",
    "type": "CARD",
    "masked": "424242xxxxxx4242",
    "dateCreated": "2021-01-14T06:38:50.637+00:00",
    "card": {
        "expiryMonth": "12",
        "expiryYear": "21",
        "cardInfo": {
            "brand": "VISA CREDIT",
            "type": "credit",
            "usage": "consumer",
            "country": "GB",
            "issuer": "DATATRANS"
        }
    }
}
```
{% endswagger-response %}

{% swagger-response status="400" description="Invalid request" %}
```javascript
{
  "error": {
    "code": "ALIAS_NOT_FOUND"
  }

```
{% endswagger-response %}
{% endswagger %}

#### Examples

{% tabs %}
{% tab title="Request" %}
```javascript
curl -L -X GET 'https://api.sandbox.datatrans.com/v1/aliases/AAABeM8amw3ssdexyrAAAYwp9fXrAIkp' \
-H 'Authorization: Basic MTEwMDAxNzc4OTpNQUd6UUVEbkVxd001d0Vr'
```
{% endtab %}

{% tab title="Response" %}
```javascript
{
    "alias": "AAABeM8amw3ssdexyrAAAYwp9fXrAIkp",
    "fingerprint": "F-dV5V8dE0SZLoTurWbq2HZp",
    "type": "CARD",
    "masked": "424242xxxxxx4242",
    "dateCreated": "2021-01-14T06:38:50.637+00:00",
    "card": {
        "expiryMonth": "12",
        "expiryYear": "21",
        "cardInfo": {
            "brand": "VISA CREDIT",
            "type": "credit",
            "usage": "consumer",
            "country": "GB",
            "issuer": "DATATRANS"
        }
    }
}
```
{% endtab %}
{% endtabs %}

{% hint style="danger" %}
Please note that the Status API is only working with the two latest [Alias 2.0 format](../../resources/token-formats.md#alias-2.0). \
Reach out to your PCI Proxy contact if you are not sure which alias format you are using.
{% endhint %}

