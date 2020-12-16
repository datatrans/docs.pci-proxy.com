---
description: >-
  Submit a payment authorization with PCI Proxy, using authentication data from
  a third-party 3D Secure 2 provider.
---

# Authorize with 3rd party authenticated data

Using this API allows you to simply send a json request with a token to just **reserve** \(authorize\) or **charge** \(settle\) an amount. 

{% tabs %}
{% tab title="Reserve an amount" %}
When you [**reserve an amount**](../../use-stored-cards/authorize-settle/#examples) on a stored card, the monthly allowance of the cardholder is reduced by the authorised amount, no matter whether the transaction will be settled later or not. The authorised amount is reserved for the merchant and should be settled within the period agreed with the acquirer. The issuer returns an authorisation code which serves as the reference of the authorisation. Once a transaction has been successfully authorised it can be settled.

**Important:** the cardholder will not be charged without settlement. Authorisation and settlement can also be processed in one single step. Please continue [here ](../../use-stored-cards/authorize-settle/defered-settlement.md)with deferred settlement API if you just authorized the transaction.
{% endtab %}

{% tab title="Charge cardholder" %}
When you [**charge a stored card**](../../use-stored-cards/authorize-settle/#examples), the authorization and settlement will be processed in one single step. The settlement is often also referred to as “capture” or “clearing”. Once you sent a charge request, the authorized amount is reduced from the monthly allowance of the cardholder and will be automatically settled, which means that the cardholder will be actually charged.
{% endtab %}
{% endtabs %}

{% hint style="success" %}
Stored cards can be used multiple times for **recurring transactions** or **One-Click payments**. 
{% endhint %}

## 1. Get authentication data

To authorize a 3D Secure 1 authenticated payment, you need the following data:

* `authenticationResponse`:  Transaction status after `paResponse`\(Challenge flow\) received from your 3D provider
* `directoryResponse`:  Transaction status after `VERes` received from your 3D provider
* `cavv`: The authentication value for the 3D Secure authentication session. The returned value is a base64-encoded 20-byte array.
* `threeDSVersion`3D-Secure version
* `xid`: The transaction identifier assigned by the Directory Server \(base64 encoded, 20 bytes in a decoded form\).
* `eci`: The electronic commerce indicator.

**For 3D Secure 2 following data are required**

* `cavv`: The `authenticationValue` from your 3D Secure 2 provider.
* `dsTransID`: The unique transaction identifier assigned by the DS to identify a single transaction.
* `eci`: The electronic commerce indicator.

## 2. Authorize a stored card

{% hint style="warning" %}
The service requires HTTP basic authentication. The required credentials can be found in our dashboard. Please refer to [API authentication data](../../guides/pci-proxy-dashboard/api-authentication-data.md#basic-authentication) for more information. 
{% endhint %}

{% api-method method="post" host="https://api.sandbox.datatrans.com" path="/v1/transactions/authorize" %}
{% api-method-summary %}
AUTH method
{% endapi-method-summary %}

{% api-method-description %}
Send a POST to /authorize including 3D data
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authentication" type="string" required=true %}
Basic MTEwMDAwNzAwNjpLNnFYMXUkIQ==  
see Setup
{% endapi-method-parameter %}

{% api-method-parameter name="Content-Type" type="string" required=true %}
application/json; charset=UTF-8
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="currency" type="string" required=true %}
3 letter ISO-4217 character code. E.g. `EUR` or `USD`
{% endapi-method-parameter %}

{% api-method-parameter name="refno" type="string" required=true %}
Your unique reference number \(AN 1..20\)
{% endapi-method-parameter %}

{% api-method-parameter name="amount" type="integer" required=true %}
The amount of the transaction in the currency's smallest unit. For example use 1000 for EUR 10.00. 
{% endapi-method-parameter %}

{% api-method-parameter name="autoSettle" type="boolean" required=false %}
Wheter to automatically settle the transaction after an authorization or not. Default is `false`. 
{% endapi-method-parameter %}

{% api-method-parameter name="card" type="object" required=true %}
Card object must contain following parameters below
{% endapi-method-parameter %}

{% api-method-parameter name="alias" type="string" required=true %}
Token received from a previous PCI Proxy integration
{% endapi-method-parameter %}

{% api-method-parameter name="expiryMonth" type="string" required=true %}
The expiry month of the token \(2 characters\)
{% endapi-method-parameter %}

{% api-method-parameter name="expiryYear" type="string" required=true %}
The expiry year of the token \(2 characters\)
{% endapi-method-parameter %}

{% api-method-parameter name="3D" type="object" required=true %}
3D data reiceved from a previous authentication request.  
See example below for details. 
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Successful authorization response
{% endapi-method-response-example-description %}

```javascript
{
  "transactionId": "191023102544373504",
  "acquirerAuthorizationCode": "102544",
  "card": {
    "masked": "424242xxxxxx4242"
  }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
 Failed authorization response  
{% endapi-method-response-example-description %}

```bash
{
  "error": {
    "code": "see table below for detailed error messages",
    "message": "see table below for detailed error messages"
  },
  "transactionId": "191023112022175523"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="warning" %}
In test mode, only [test credit cards](../../test-card-data.md) are allowed.
{% endhint %}

### Examples \(3D v1\)

{% tabs %}
{% tab title="Authorize amount \(authorize & settle\)" %}
{% code title="Request" %}
```javascript
curl -L -X POST 'https://api.sandbox.datatrans.com/v1/transactions/authorize' \
-H 'Content-Type: application/json; charset=UTF-8' \
-H 'Authorization: Basic MTEwMDAxNzc4OTpNQUd6UUVEbkVxd001d0Vr' \
-H 'Content-Type: text/plain' \
-d'{
    "currency": "EUR",
    "refno": "3Dv2-Test",
    "amount": 1000,
    "card": {
        "alias": "AAABchiPFXnssdexyrAAAYStQsjpANlH",
        "expiryMonth": "12",
        "expiryYear": "21",
    	  "3D": {
    		    "eci": "02",
    		    "xid": "MDAyMDA1MTgxMDA4NDE2OTExMjI=",
    		    "cavv": "OTkyMDA1MTgxMDA4NTY1NjExMzg=",
    		    "threeDSVersion": "1.0.2",
    		    "cavvAlgorithm": "1",
    		    "directoryResponse": "Y",
    		    "authenticationResponse": "Y"
    		    }
    	}
}'
```
{% endcode %}

{% code title="Response \(successful\)" %}
```javascript
{
  "transactionId": "200518101037811359",
  "acquirerAuthorizationCode": "101037",
  "card": {
    "masked": "510000xxxxxx0022"
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Error table

If the authorisation failed, you receive one of the of the following error codes. 

> `"UNKNOWN_ERROR"`, `"UNRECOGNIZED_PROPERTY"`, `"INVALID_PROPERTY"`, `"INVALID_TRANSACTION_STATUS"`, `"TRANSACTION_NOT_FOUND"`, `"INVALID_JSON_PAYLOAD"`, `"UNAUTHORIZED"`, `"EXPIRED_CARD"`, `"INVALID_CARD"`, `"UNSUPPORTED_CARD"`, `"DUPLICATED_REFNO"`, `"DECLINED"`, `"BLOCKED_BY_VELOCITY_CHECKER"`, `"CLIENT_ERROR"` , `"SERVER_ERROR"`

