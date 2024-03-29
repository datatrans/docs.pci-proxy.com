---
description: >-
  Using the Credit Card Check API provides you with a simple and effective way
  against fraud
---

# Check

We run a zero amount authorization request against the Visa, Mastercard, and American Express network to check if the card is still valid, not stolen, or expired. The authorization request does not appear on the customer statement but still gives you the ability to test the validity of a stored credit card.

{% hint style="warning" %}
The service requires HTTP basic authentication. The required credentials can be found in our dashboard. Please refer to [API authentication data](broken-reference) for more information.&#x20;
{% endhint %}

## 1. Activate Credit Card Check

Please contact the PCI Proxy team to activate the credit card check feature on your PCI Proxy account.&#x20;

## 2. Call the validate API&#x20;

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/transactions/validate" method="post" summary="Validate" %}
{% swagger-description %}
The parameters marked with * are mandatory.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Basic MTEwMDAwNzAwNjpLNnFYMXUklQ==
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="string" required="true" %}
3 letter ISO-4217 character code. For 

**VISA**

 and 

**MC**

 cards use 

`CHF`

, 

`USD`

 or 

`EUR`

 and for 

**AMEX**

 cards use 

`EUR`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="refno" type="string" required="true" %}
Your unique reference number (AN 1..20)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="card" type="object" required="true" %}
Card object must contain following parameters below
{% endswagger-parameter %}

{% swagger-parameter in="body" name="alias" type="string" required="true" %}
Credit card token received from initial tokenisation
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiryMonth" type="string" required="true" %}
The expiry month of the credit card token (AN2)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiryYear" type="string" required="true" %}
The expiry year of the credit card token (AN2)
{% endswagger-parameter %}

{% swagger-response status="200" description="Credit Card successfully validated" %}
```javascript
{
"transactionId": "190828124101219812",
"acquirerAuthorizationCode": "124101"
}
```
{% endswagger-response %}

{% swagger-response status="400" description="Credit Card Expired" %}
```javascript
{
  "error": {
    "code": "EXPIRED_CARD",
    "message": "expired card"
  },
  "transactionId": "191016104534077141",
  "card": {}
}
```
{% endswagger-response %}
{% endswagger %}

{% hint style="warning" %}
In test mode, only [test credit cards](broken-reference) are allowed.
{% endhint %}

### Examples

{% tabs %}
{% tab title="Request" %}
```javascript
curl -X POST \
  https://api.sandbox.datatrans.com/v1/transactions/validate \
  -H 'Authorization: Basic MTAwMDAwMTExMTpwWUU4bFE2TlBiM2thRXpR' \
  -H 'Content-Type: application/json; charset=UTF-8' \
  -d '{
    "currency": "EUR",
    "refno": "vptJ07xyr",
    "card": {
        "alias": "AAABcHxr-sDssdexyrAAAfyXWIgaAF40",
        "expiryMonth": "06",
        "expiryYear": "25"
    }
}'
```
{% endtab %}

{% tab title="Response Success" %}
```javascript
{
  "transactionId": "191016104224286267",
  "acquirerAuthorizationCode": "104224",
  "card": {
    "masked": "424242xxxxxx4242"
  }
}
```
{% endtab %}

{% tab title="Response error " %}
```javascript
{
  "error": {
    "code": "EXPIRED_CARD",
    "message": "expired card"
  },
  "transactionId": "191016104534077141",
}
```
{% endtab %}
{% endtabs %}

### Errors

> `UNKNOWN_ERROR` `UNAUTHORIZED` `INVALID_JSON_PAYLOAD` `UNRECOGNIZED_PROPERTY` `INVALID_PROPERTY` `CLIENT_ERROR` `SERVER_ERROR` `INVALID_TRANSACTION_STATUS` `TRANSACTION_NOT_FOUND` `EXPIRED_CARD` `INVALID_CARD` `BLOCKED_CARD` `UNSUPPORTED_CARD` `INVALID_ALIAS` `INVALID_CVV` `DUPLICATE_REFNO` `DECLINED` `SOFT_DECLINED` `INVALID_SIGN` `BLOCKED_BY_VELOCITY_CHECKER` `THIRD_PARTY_ERROR` `REFERRAL` `INVALID_SETUP`
