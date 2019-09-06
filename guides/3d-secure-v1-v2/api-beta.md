---
description: >-
  Use server-to-server based Authentication only integration to receive 3D
  authentication data.
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

Secure Fields 3D requires a 3D Secure enrolled acquiring contract that needs to be activated on your account \(`merchantId`\). 
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
Transaction in the currency's smallets unit. For example use 1000 for EUR 10.00
{% endapi-method-parameter %}

{% api-method-parameter name="currency" type="string" required=true %}
3 letter ISO-4217 character code. For example `EUR` or `USD`
{% endapi-method-parameter %}

{% api-method-parameter name="refno" type="string" required=true %}
\[1..20\] characters  
It should be unique each transaction
{% endapi-method-parameter %}

{% api-method-parameter name="paymentMethods" type="array" required=true %}
An array of payment method shortnames  
Items Enum: `"AMX"` `"DIN"` `"ECA"` `"INT"` `"KLN"` `"MPW"` `"MYO"` `"VIS"`
{% endapi-method-parameter %}

{% api-method-parameter name="card" type="object" required=true %}
card object must contain following parameters below
{% endapi-method-parameter %}

{% api-method-parameter name="number" type="string" required=true %}
Plain text card number or PCI Proxy token
{% endapi-method-parameter %}

{% api-method-parameter name="expiryMonth" type="string" required=true %}
Expiry month of card \(2 characters\)
{% endapi-method-parameter %}

{% api-method-parameter name="expiryYear" type="string" required=true %}
Expiry year of card \(2 characters\)
{% endapi-method-parameter %}

{% api-method-parameter name="3D" type="object" required=false %}
3D object for optional 3D v2 parameters  
See hint box below for additional information.
{% endapi-method-parameter %}

{% api-method-parameter name="option" type="string" required=true %}
option object must contain following parameters below
{% endapi-method-parameter %}

{% api-method-parameter name="authenticationOnly" type="boolean" required=true %}
true
{% endapi-method-parameter %}

{% api-method-parameter name="redirect" type="object" required=true %}
redirect object must contain following parameters below
{% endapi-method-parameter %}

{% api-method-parameter name="successUrl" type="string" required=true %}
Url where cardholder will be redirect in case of successful 3D process
{% endapi-method-parameter %}

{% api-method-parameter name="cancelUrl" type="string" required=true %}
Url where cardholder will be redirected in case cancled 3D process
{% endapi-method-parameter %}

{% api-method-parameter name="errorUrl" type="string" required=true %}
Url where cardholder will be redirected in case of an error in 3D process
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=201 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```java
{
    "transactionId": "190527154549809618",
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
{% code-tabs-item title="Request with plain text cardnumber" %}
```java
curl -X POST \
  https://api.sandbox.datatrans.com/v1/transactions \
  -H 'Authorization: Basic MTEwMDAxNzY3NTpTejdodE5uSjdNM05YQ0lT,Basic MTEwMDAxNzY3NTpTejdodE5uSjdNM05YQ0lT' \
  -d '{
    "amount": 1000,
    "currency": "EUR",
    "refno": "NIJ3OSelzyqp",
    "paymentMethods": ["ECA"],
    "card": {
        "number": "5200000000000080",
        "cvv": "123", 
        "expiryMonth": "12",
        "expiryYear": "21",
        "3D": {
            "deviceChannel": "02",
            "messageCategory": "01",
            "threeDSCompInd": "Y",
            "threeDSRequestor": {},
            "threeDSServerTransID": "df4b3490-db44-4a88-9619-ab173ff76fbe",
            "cardholderAccount": {},
            "cardholder": {},
            "relaxRegionalValidationRules": false,
            "purchase": {},
            "acquirer": {},
            "merchant": {},
            "broadInfo": {},
            "deviceRenderOptions": {},
            "messageExtension": [],
            "browserInformation": {},
            "threeRIInd": "02",
            "sdkInformation": {}
            }
    },
    "option": {
        "authenticationOnly": true
    },
    "redirect": {
    	"successUrl": "https://pay.sandbox.datatrans.com/upp/merchant/successPage.jsp",
        "cancelUrl": "https://pay.sandbox.datatrans.com/upp/merchant/cancelPage.jsp",
        "errorUrl": "https://pay.sandbox.datatrans.com/upp/merchant/errorPage.jsp"
    }
}'
```
{% endcode-tabs-item %}

{% code-tabs-item title="Request with masked token" %}
```java
curl -X POST \
  https://api.sandbox.datatrans.com/v1/transactions \
  -H 'Authorization: Basic MTEwMDAxNzY3NTpTejdodE5uSjdNM05YQ0lT,Basic MTEwMDAxNzY3NTpTejdodE5uSjdNM05YQ0lT' \
  -d '{
    "amount": 1000,
    "currency": "EUR",
    "refno": "NIJ3OSelzyqp",
    "paymentMethods": ["ECA"],
    "card": {
        "alias": "520000RIVWAS0080", 
        "aliasCVV": "YahfrXdEQT67X1u7Og49rg2e",
        "expiryMonth": "12",
        "expiryYear": "21",
        "3D": {
            "deviceChannel": "02",
            "messageCategory": "01",
            "threeDSCompInd": "Y",
            "threeDSRequestor": {},
            "threeDSServerTransID": "df4b3490-db44-4a88-9619-ab173ff76fbe",
            "cardholderAccount": {},
            "cardholder": {},
            "relaxRegionalValidationRules": false,
            "purchase": {},
            "acquirer": {},
            "merchant": {},
            "broadInfo": {},
            "deviceRenderOptions": {},
            "messageExtension": [],
            "browserInformation": {},
            "threeRIInd": "02",
            "sdkInformation": {}
            }
    },
    "option": {
        "authenticationOnly": true
    },
    "redirect": {
    	"successUrl": "https://pay.sandbox.datatrans.com/upp/merchant/successPage.jsp",
        "cancelUrl": "https://pay.sandbox.datatrans.com/upp/merchant/cancelPage.jsp",
        "errorUrl": "https://pay.sandbox.datatrans.com/upp/merchant/errorPage.jsp"
    }
}'
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response" %}
```java
Response headers:
Location: https://pay.sandbox.datatrans.com/v1/start/190906151210861442

Response body:
{
  "transactionId" : "190906151210861442",
  "3D" : {
    "enrolled" : true
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Step 2: Display a 3D secure challenge

In the body of the response you receive the `transactionID` and in the location header the `3D-redirect`URL. Redirect the cardholder to this URL to trigger the 3D-Secure process. Once the card holder completed the 3D-Secure process, he will be redirected to the `successUrl` passed to the `v1/transactions` API. 

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
    "currency": "EUR",
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
  https://api.sandbox.datatrans.com/v1/transactions/190906151210861442 \
  -H 'Authorization: Basic MTEwMDAxNzY3NTpTejdodE5uSjdNM05YQ0lT' \

```
{% endcode-tabs-item %}

{% code-tabs-item title="Response" %}
```java
{
  "transactionId": "190906151210861442",
  "type": "payment",
  "status": "authenticated",
  "currency": "EUR",
  "refno": "EVO-1564475113071",
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
      "date": "2019-09-06T13:12:11.915+00:00",
      "success": true,
      "ip": "77.109.165.195"
    },
    {
      "action": "authenticate",
      "amount": 1000,
      "source": "web",
      "date": "2019-09-06T13:12:21.915+00:00",
      "success": true,
      "ip": "77.109.165.195"
    }
  ],
  "card": {
    "masked": "520000xxxxxx0080",
    "expiryMonth": "12",
    "expiryYear": "21",
    "info": {
      "brand": "MCI CREDIT",
      "type": "credit",
      "usage": "consumer",
      "country": "MY",
      "issuer": "DATATRANS"
    },
    "3D": {
      "eci": "02",
      "xid": "MDAxOTA5MDYxNTEyMTA4NjE0NDI=",
      "cavv": "OTkxOTA5MDYxNTEyMjE3NTE0NjA=",
      "threeDSVersion": "1.0.2",
      "cavvAlgorithm": "1",
      "directoryResponse": "Y",
      "authenticationResponse": "Y"
    }
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### 3-object field name mapping  

| Datatrans  | EMVCo |
| :--- | :--- |
| `eci` | `eci` |
| `xid` | `dsTransId` |
| `cavvAlgorithm` | Only required for 3D Secure 1 |
| `cavv` | `authenticationValue` |
| `threeDSVersion` | `messageVersion` |
| `directoryResponse` | `transStatus` \(after ARes\) |
| `authenticationResponse` | `transStatus` \(after RReq\) |

## Step 4: Forward 3D data

The received `"3D"` object contains parameters with the result of the 3D-Secure process and can be forwarded to 3rd party payment gateways. If you decide to use Datatrans payment gateway please continue with our [Authorize](authorize.md) API.

