---
description: >-
  Use the Patch transaction API to update the amount or currency for an already
  initialized transaction.
---

# Update a transaction

{% hint style="info" %}
Call the Patch transaction API endpoint after calling `secureFields.init()` and before calling `secureFields.submit()`.
{% endhint %}

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/transactions/secureFields/{transactionId}" method="patch" summary="Transaction" %}
{% swagger-description %}
Update the amount or currency of an already initialized transaction. 
{% endswagger-description %}

{% swagger-parameter in="path" name="transactionId" type="string" %}
The transactionId obtained via initial 

`/v1/transactions/secureFields`

 call
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Basic MTEwMDAyNjUyfDrtSwty5fdstEtodDZpQU1O
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-type" type="string" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="integer" %}
The new amount in the currency's smallest unit. For example use 1000 for EUR 10.00
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="integer" %}
Three letter ISO-4217 character code. For example 

`GBP`
{% endswagger-parameter %}

{% swagger-response status="204" description="Amount or currency successfully updated" %}
```
```
{% endswagger-response %}

{% swagger-response status="400" description="Invalid property" %}
```javascript
{
    "error": {
        "code": "INVALID_PROPERTY",
        "message": "update at least one property (e.g. amount or currency)"
    }
}
```
{% endswagger-response %}

{% swagger-response status="404" description="Transaction not found" %}
```
{
    "error": {
        "code": "TRANSACTION_NOT_FOUND"
    }
}
```
{% endswagger-response %}
{% endswagger %}

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

