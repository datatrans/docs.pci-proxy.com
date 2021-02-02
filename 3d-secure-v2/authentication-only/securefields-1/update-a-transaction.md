---
description: >-
  Use the Patch transaction API to update the amount or currency for an already
  initialized transaction.
---

# Update a transaction

{% hint style="info" %}
Call the Patch transaction API endpoint after calling `secureFields.init()` and before calling `secureFields.submit()`.
{% endhint %}

{% api-method method="patch" host="https://api.sandbox.datatrans.com" path="/v1/transactions/secureFields/{transactionId}" %}
{% api-method-summary %}
Transaction
{% endapi-method-summary %}

{% api-method-description %}
Update the amount or currency of an already initialized transaction. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="transactionId" type="string" required=true %}
The transactionId obtained via initial `/v1/transactions/secureFields` call
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Basic MTEwMDAyNjUyfDrtSwty5fdstEtodDZpQU1O
{% endapi-method-parameter %}

{% api-method-parameter name="Content-type" type="string" required=true %}
application/json; charset=UTF-8
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="amount" type="integer" required=false %}
The new amount in the currency's smallest unit. For example use 1000 for EUR 10.00
{% endapi-method-parameter %}

{% api-method-parameter name="currency" type="integer" required=false %}
Three letter ISO-4217 character code. For example `GBP`
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Amount or currency successfully updated
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Invalid property
{% endapi-method-response-example-description %}

```javascript
{
    "error": {
        "code": "INVALID_PROPERTY",
        "message": "update at least one property (e.g. amount or currency)"
    }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Transaction not found
{% endapi-method-response-example-description %}

```
{
    "error": {
        "code": "TRANSACTION_NOT_FOUND"
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Example

{% tabs %}
{% tab title="Request" %}
```java
curl -L -X PATCH 'https://api.sandbox.datatrans.com/v1/transactions/secureFields/201110094904976728' \
-H 'merchantId:password' \
-H 'Content-Type: application/json; charset=UTF-8' \
--data-raw '{
    "amount": 5000,
    "currency": "GBP"
}'
```
{% endtab %}

{% tab title="Response" %}
```
204 No content
```
{% endtab %}
{% endtabs %}



