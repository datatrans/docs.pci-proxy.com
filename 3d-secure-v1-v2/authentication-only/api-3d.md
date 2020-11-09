---
description: >-
  Use server-to-server based Authentication only integration to receive 3D
  authentication data.
---

# API 3D

## Before you start

1. \*\*\*\*[**Sign up**](https://dashboard.pci-proxy.com/signup) for a free PCI Proxy sandbox account.

{% hint style="info" %}
* This service requires basic authentication. Please refer to [Authentication](../../guides/pci-proxy-dashboard/api-authentication-data.md#basic-authentication) to retrieve required crendetials. 
* Make sure to use our 3D Secure enabled test credit cards [here](../testing-3d-secure.md).
{% endhint %}

{% hint style="warning" %}
**3D Secure Enrollment Requirements**

Secure Fields 3D requires a 3D Secure enrolled acquiring contract. Either deposited on your merchantID or sent dynamically in the initial request to `/v1/transactions`
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
Transaction in the currency's smallest unit. For example use 1000 for EUR 10.00
{% endapi-method-parameter %}

{% api-method-parameter name="currency" type="string" required=true %}
3 letter ISO-4217 character code. For example `EUR` or `USD`
{% endapi-method-parameter %}

{% api-method-parameter name="refno" type="string" required=true %}
\[1..20\] characters  
It should be unique each transaction
{% endapi-method-parameter %}

{% api-method-parameter name="paymentMethods" type="array" required=true %}
An array with one element: payment method shortname  
`"AMX"` `"CUP"` `"ECA"` `"DIN"` `"DIS"` `"JCB"` `"VIS"`
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
Url where cardholder will be redirected in case of  canceled 3D process
{% endapi-method-parameter %}

{% api-method-parameter name="errorUrl" type="string" required=true %}
Url where cardholder will be redirected in case of an error in 3D process
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=201 %}
{% api-method-response-example-description %}
Returns the transactionId and wheter the card is enrolled for 3D or not. 
{% endapi-method-response-example-description %}

```javascript
{
    "transactionId": "190527154549809618",
    "3D": {
        "enrolled": true
    }
},
{
  "transactionId": "190911134600593525",
  "3D": {
    "enrolled": false
  }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Invalid Request: Returns error object with an error code and an error message.
{% endapi-method-response-example-description %}

```javascript
{
  "error": {
    "code": "INVALID_PROPERTY",
    "message": "init.refno must not be null"
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

{% tabs %}
{% tab title="Request with masked token" %}
```javascript
curl -X POST \
  https://api.sandbox.datatrans.com/v1/transactions \
  -H 'Authorization: Basic MTEwMDAxNzY3NTpTejdodE5uSjdNM05YQ0lT,Basic MTEwMDAxNzY3NTpTejdodE5uSjdNM05YQ0lT' \
  -d '{
    "amount": 1000,
    "currency": "EUR",
    "refno": "NIJ3OSelzyqp",
    "paymentMethods": ["ECA"],
    "card": {
        "alias": "AAABcHxr-sDssdexyrAAAfyXWIgaAF40", 
        "expiryMonth": "12",
        "expiryYear": "21",
         "3D": {
            "acquirer": {
                "acquirerMerchantId": "1354656",
                "acquirerBin": "9854128"
            },
            "merchant": {
                "mcc": "4722",
                "merchantName": "Example Travel Ltd."
            }
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
{% endtab %}

{% tab title="Request with plain text cardnumber" %}
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
            "acquirer": {
            		"acquirerMerchantId": "1234567",
            		"acquirerBin": "9876543"
            	},
            "merchant": {
            		"mcc": "4722",
            		"merchantName": "Example Travel Ltd."
            	}
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
{% endtab %}

{% tab title="Response" %}
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
{% endtab %}
{% endtabs %}

#### 3D-Secure Acquirer related data

To use the Authentication only API you need to get the following information from your acquirer as they are part of the 3D Secure 2 enrolment process between your acquirer and card schemes.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>acquirerMerchantId</code>
      </td>
      <td style="text-align:left">
        <p>Acquirer Merchant ID</p>
        <p>Acquirer-assigned Merchant identifier</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>acquirerBin</code>
      </td>
      <td style="text-align:left">
        <p>Acquirer BIN</p>
        <p>Acquiring institution identification code</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>mcc</code>
      </td>
      <td style="text-align:left">
        <p>Merchant Category Code</p>
        <p>Describes the Merchant&#x2019;s type of business, product or service.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>merchantName</code>
      </td>
      <td style="text-align:left">
        <p>Merchant Name</p>
        <p>Name which will be displayed on the ACS page.</p>
      </td>
    </tr>
  </tbody>
</table>

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

{% tabs %}
{% tab title="Request" %}
```java
curl -X GET \
  https://api.sandbox.datatrans.com/v1/transactions/190906151210861442 \
  -H 'Authorization: Basic MTEwMDAxNzY3NTpTejdodE5uSjdNM05YQ0lT' \

```
{% endtab %}

{% tab title="Response" %}
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
{% endtab %}
{% endtabs %}

#### 3-object field name mapping  

<table>
  <thead>
    <tr>
      <th style="text-align:left">Datatrans</th>
      <th style="text-align:left">EMVCo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>eci</code>
      </td>
      <td style="text-align:left"><code>eci</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>xid</code>
      </td>
      <td style="text-align:left">
        <p><code>dsTransId</code> (3Dv2)</p>
        <p><code>xid</code> (3Dv1)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>cavvAlgorithm</code>
      </td>
      <td style="text-align:left">Only required for 3D Secure 1</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>cavv</code>
      </td>
      <td style="text-align:left"><code>authenticationValue</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>threeDSVersion</code>
      </td>
      <td style="text-align:left"><code>messageVersion</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>directoryResponse</code>
      </td>
      <td style="text-align:left"><code>transStatus </code>(after ARes)</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>authenticationResponse</code>
      </td>
      <td style="text-align:left"><code>transStatus </code>(after RReq)</td>
    </tr>
  </tbody>
</table>

#### Directory Response \(Transaction status after `ARes`\)

| Value | 3Dv1 | 3Dv2 |
| :--- | :--- | :--- |
| Y | enrolled | authenticated |
| N | not enrolled | authentication failed |
| U | not available | not available |
| C |  | challenge needed |
| R |  | rejected |

#### Authentication Response \(Transaction status after `RReq` \(Challenge flow\)\)

| Value  | 3Dv1 | 3Dv2 |
| :--- | :--- | :--- |
| Y | authenticated | authenticated |
| N | authentication failed | authentication failed |
| U | not available | not available |
| A | authentication attempt | authentication attempt |
| C | process incomplete | process incomplete |
| D | not enrolled |  |

## Step 4: Forward 3D data

The received `"3D"` object contains parameters with the result of the 3D-Secure process and can be forwarded to 3rd party payment gateways. If you decide to use Datatrans payment gateway please continue with our [Authorize](../authorize-1/authorize.md) API.

