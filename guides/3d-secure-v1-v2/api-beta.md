---
description: >-
  Use server-to-server based authenticate only integration to receive 3D
  authentification data.
---

# API 3D \(beta\)

## Before you start

1. [**Sign up**](https://www.pci-proxy.com/pci-proxy/contact/) for a free PCI Proxy sandbox account.

{% hint style="info" %}
* This service requires basic authentication. The password can be found in the [Web Admin Tool](https://admin.sandbox.datatrans.com/) under _UPP Administration &gt; Security &gt; Server-to-Server services security_.
* Make sure to use our 3D Secure enabled test credit cards [here](../testing-3d-secure.md).
{% endhint %}

{% hint style="warning" %}
**3D Secure Enrollment Requirements**

Secure Fields 3D requires a 3D Secure enrolled acquiring contract that needs to be activated on your account \(`merchantId`\). If you don't have your own acquiring contract, please contact us to use our generic 3D Secure contract \(currently VISA and Mastercard only\).
{% endhint %}

## Step 1: Initial Server-to-Server call

{% api-method method="post" host="https://api.sandbox.datatrans.com" path="/v1/transactions" %}
{% api-method-summary %}
Init call
{% endapi-method-summary %}

{% api-method-description %}
Initial Server-to-Server call to retrieve transactionId and submit 3D Secure v1 and v2 parameters. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==  
see Setup
{% endapi-method-parameter %}

{% api-method-parameter name="Content-Type" type="string" required=true %}
API consumes application/json; charset=UTF-8
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="amount" type="integer" required=true %}
1000
{% endapi-method-parameter %}

{% api-method-parameter name="currency" type="string" required=true %}
3 letter ISO-4217 character code. For example `CHF` or `EUR`
{% endapi-method-parameter %}

{% api-method-parameter name="refno" type="string" required=true %}
\[1..20\] characters  
It should be unique each transaction 
{% endapi-method-parameter %}

{% api-method-parameter name="card" type="object" required=true %}
card object must contain following parameters below
{% endapi-method-parameter %}

{% api-method-parameter name="alias" type="integer" required=true %}
Plain text cardnumber or masked PCI Proxy token
{% endapi-method-parameter %}

{% api-method-parameter name="expiryMonth" type="string" required=true %}
2 characters
{% endapi-method-parameter %}

{% api-method-parameter name="expiryYear" type="string" required=true %}
2 characters 
{% endapi-method-parameter %}

{% api-method-parameter name="3D" type="object" required=true %}
3D object for additional 3D v2 parameters
{% endapi-method-parameter %}

{% api-method-parameter name="option" type="object" required=true %}
option object must contain following paramter below
{% endapi-method-parameter %}

{% api-method-parameter name="authenticateOnly" type="boolean" required=true %}
true
{% endapi-method-parameter %}

{% api-method-parameter name="redirect" type="object" required=true %}
redirect object must contain following parameter below
{% endapi-method-parameter %}

{% api-method-parameter name="successUrl" type="string" required=true %}
Your 3D process return URL
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```java
{
    "transactionId": "190522135046172715",
    "3D": {
        "enrolled": true
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
Refer to the official EMVCo 3D specification 2.1.0 for parameter requirements sent in the `3D`object. [https://www.emvco.com/emv-technologies/3d-secure/](https://www.emvco.com/emv-technologies/3d-secure/)
{% endhint %}

#### Examples

{% code-tabs %}
{% code-tabs-item title="Request" %}
```java
curl -X POST \
  https://api.sandbox.datatrans.com/v1/transactions \
  -H 'Authorization: Basic MTEwMDAxNzY3NTpTejdodE5uSjdNM05YQ0lT,Basic MTEwMDAxNzY3NTpTejdodE5uSjdNM05YQ0lT' \
  -d '{
    "amount": 1000,
    "currency": "CHF",
    "refno": "NIJ3OSelzyqp",
    "card": {
        "alias": "5200000000000080", 
        "expiryMonth": "12",
        "expiryYear": "21"
        "3D": {...}
    },
    "option": {
        "authenticationOnly": true
    },
        "redirect": {
    	"successUrl": "https://pay.sandbox.datatrans.com/upp/merchant/successPage.jsp"
    }
}'
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response" %}
```java
{
    "transactionId": "190522135046172715",
    "3D": {
        "enrolled": true
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Step 2: Display a 3D secure challenge

In the body of the response you receive the `transactionID` and in the location header the `3D-redirect`URL. Redirect the cardholder to this URL to trigger 3D-Secure process. Once the card holder completed the 3D process, he will be redirected to the `successUrl` passed to the `v1/transactions` API. 

## Step 3: Obtain 3D parameters

{% api-method method="get" host="https://api.sandbox.datatrans.com" path="/v1/transactions/{transactionId}" %}
{% api-method-summary %}
Status API
{% endapi-method-summary %}

{% api-method-description %}
Obtain 3D parameters, credit card and cvv token by executing a server to server call with the `transactionId` received in step 1. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==  
see setup
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="transactionId" type="string" required=true %}
transactionId obtained via `/v1/transactions`
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```java
{
    "transactionId": "190522141403888597",
    "type": "payment",
    "status": "authenticated",
    "currency": "CHF",
    "refno": "NIJ3OSelzyqp",
    "paymentMethod": "ECA",
    "detail": {
        "authorize": {
            "amount": 1000
        }
    },
    "history": [
        {
            "action": "init",
            "amount": 1000,
            "source": "api",
            "date": "2019-05-22T12:14:04.385+00:00",
            "success": true,
            "ip": "77.109.165.195"
        }
    ],
    "card": {
        "masked": "520000xxxxxx0080",
        "3D": {
            "eci": "02",
            "xid": "MDAxOTA1MjIxNDE0MDM4ODg1OTc=",
            "cavv": "OTkxOTA1MjIxNDE0MjMwMjg2Mjc=",
            "threeDSVersion": "1.0.2",
            "directoryResponse": "Y",
            "authenticationResponse": "Y"
        }
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

#### Examples

{% code-tabs %}
{% code-tabs-item title="Request" %}
```java
curl -X GET \
  https://api.sandbox.datatrans.com/v1/transactions/190522141403888597 \
  -H 'Authorization: Basic MTEwMDAxNzY3NTpTejdodE5uSjdNM05YQ0lT' \

```
{% endcode-tabs-item %}

{% code-tabs-item title="Response" %}
```java
{
    "transactionId": "190522141403888597",
    "type": "payment",
    "status": "authenticated",
    "currency": "CHF",
    "refno": "NIJ3OSelzyqp",
    "paymentMethod": "ECA",
    "detail": {
        "authorize": {
            "amount": 1000
        }
    },
    "history": [
        {
            "action": "init",
            "amount": 1000,
            "source": "api",
            "date": "2019-05-22T12:14:04.385+00:00",
            "success": true,
            "ip": "77.109.165.195"
        }
    ],
    "card": {
        "masked": "520000xxxxxx0080",
        "3D": {
            "eci": "02",
            "xid": "MDAxOTA1MjIxNDE0MDM4ODg1OTc=",
            "cavv": "OTkxOTA1MjIxNDE0MjMwMjg2Mjc=",
            "threeDSVersion": "1.0.2",
            "directoryResponse": "Y",
            "authenticationResponse": "Y"
        }
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Step 4: Forward 3D data

Received `"3D"` object contains parameters with the result of the 3D-Secure process and can be fowarded to 3rd party payment gateway. If you decide to use Datatrans payment gateway please continue with our [Authorize](../../use-stored-cards/authorize.md) API.
