---
description: >-
  Use this API to validate an existing Token against the VISA, MasterCard and
  AMEX network at any time.
---

# Check

{% hint style="info" %}
Using the card check API provides you with a simple and effective way against fraud.   
Thereby we run a zero amount call against the Visa, MasterCard and AMEX network to check if the card is still valid, not stolen or expired. The authorization request does not appear on the customer statement but still gives you the ability to test the validity of a stored credit card. 
{% endhint %}

{% hint style="warning" %}
The service requires HTTP basic authentication. The required credentials can be found in our dashboard. Please refer to [API authentication data](../guides/pci-proxy-dashboard/api-authentication-data.md#basic-authentication) for more information. 
{% endhint %}

## 1. Activate credit card check feature

Please contact PCI Proxy team to activate the credit card check feature on your PCI Proxy account. 

## 2. Call the validate API 

{% api-method method="post" host="https://api.sandbox.datatrans.com" path="/v1/transactions/validate" %}
{% api-method-summary %}
Validate method
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Basic MTEwMDAwNzAwNjpLNnFYMXUklQ==
{% endapi-method-parameter %}

{% api-method-parameter name="Content-Type" type="string" required=true %}
application/json; charset=UTF-8
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="currency" type="string" required=true %}
3 letter ISO-4217 character code. For **VISA** and **MC** cards use `CHF`, `USD` or `EUR` and for **AMEX** cards use `EUR`
{% endapi-method-parameter %}

{% api-method-parameter name="refno" type="string" required=true %}
Your unique reference number \(AN 1..20\)
{% endapi-method-parameter %}

{% api-method-parameter name="card" type="object" required=true %}
Card object must contain following parameters below
{% endapi-method-parameter %}

{% api-method-parameter name="alias" type="string" required=true %}
Credit card token received from initial tokenisation
{% endapi-method-parameter %}

{% api-method-parameter name="expiryMonth" type="string" required=true %}
The expiry month of the credit card token \(AN2\)
{% endapi-method-parameter %}

{% api-method-parameter name="expiryYear" type="string" required=true %}
The expiry year of the credit card token \(AN2\)
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Credit Card successfully validated
{% endapi-method-response-example-description %}

```javascript
{
"transactionId": "190828124101219812",
"acquirerAuthorizationCode": "124101"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Credit Card Expired
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="warning" %}
In test mode, only [test credit cards](../test-card-data.md) are allowed.
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
        "expiryMonth": "12",
        "expiryYear": "21"
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

### Error table

> `"UNKNOWN_ERROR"`, `"UNRECOGNIZED_PROPERTY"`, `"INVALID_PROPERTY"`, `"INVALID_TRANSACTION_STATUS"`, `"TRANSACTION_NOT_FOUND"`, `"INVALID_JSON_PAYLOAD"`, `"UNAUTHORIZED"`, `"EXPIRED_CARD"`, `"INVALID_CARD"`, `"UNSUPPORTED_CARD"`, `"DUPLICATED_REFNO"`, `"DECLINED"`, `"BLOCKED_BY_VELOCITY_CHECKER"`, `"CLIENT_ERROR"` , `"SERVER_ERROR"`

