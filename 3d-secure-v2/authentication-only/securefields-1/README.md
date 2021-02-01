---
description: >-
  Use Secure Fields integration for Tokenisation and Authentication only in your
  frontend.
---

# SecureFields 3D

## Before you start

1. \*\*\*\*[**Sign up** ](https://dashboard.pci-proxy.com/signup)for a free PCI Proxy sandbox account.

{% hint style="info" %}
* This service requires basic authentication. Please refer to [Authentication](../../../guides/pci-proxy-dashboard/api-authentication-data.md#basic-authentication) to retrieve required credentials. 
* Make sure to use our 3D Secure enabled test credit cards [here](../../testing-3d-secure.md).
{% endhint %}

{% hint style="warning" %}
**3D Secure Enrollment Requirements**

Secure Fields 3D requires a 3D Secure enrolled acquiring contract for each card brand. Those 3D acquiring data needs to be sent in the initial call to `/v1/transactions/secureFields` 
{% endhint %}

## Step 1: Initial Server-to-Server call

{% api-method method="post" host="https://api.sandbox.datatrans.com" path="/v1/transactions/secureFields" %}
{% api-method-summary %}
Init call
{% endapi-method-summary %}

{% api-method-description %}
Initial Server-to-Server call to retrieve the transactionId and submit the optional 3D parameters. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==  
see API Authentication data
{% endapi-method-parameter %}

{% api-method-parameter name="Content-Type" type="string" required=true %}
API consumes application/json; charset=UTF-8
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="amount" type="integer" required=true %}
Transaction amount in the currency's smallest unit. For example use 1000 for EU 10.00
{% endapi-method-parameter %}

{% api-method-parameter name="currency" type="string" required=true %}
3 letter ISO-4217 character. For example EUR or USD
{% endapi-method-parameter %}

{% api-method-parameter name="returnUrl" type="string" required=true %}
Your 3D process return URL
{% endapi-method-parameter %}

{% api-method-parameter name="AMX" type="object" required=true %}
Object used for AMEX 3D acquiring data
{% endapi-method-parameter %}

{% api-method-parameter name="VIS" type="object" required=true %}
Object used for VISA 3D acquiring data
{% endapi-method-parameter %}

{% api-method-parameter name="ECA" type="object" required=true %}
Object used for Mastercard 3D acquiring data
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=201 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```java
{
    "transactionId": "190520110934541218",
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Amount must be at least in the currency's smallest unit. 
{% endapi-method-response-example-description %}

```java
{
    "error": {
        "code": "INVALID_PROPERTY",
        "message": "init.amount must be > 0"
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
3D Secure 2 allows you send additional, optional data to ensure increased acceptance and frictionless rate at the issuer. Please refer to the official EMVCo 3D specification 2.1.0 for parameter requirements sent in the card brands object. [https://www.emvco.com/emv-technologies/3d-secure/](https://www.emvco.com/emv-technologies/3d-secure/) or contact us for more information. 
{% endhint %}

#### Example

{% tabs %}
{% tab title="Request" %}
```java
curl -L -X POST 'https://api.sandbox.datatrans.com/v1/transactions/secureFields' \
-H 'Authorization: Basic MTEwMDAxNzc4OTpNQUd6UUVEbkVxd001d0Vr' \
-H 'Content-Type: application/json' \
    -d '{
    "amount" : 1000,
    "currency" : "EUR",
    "returnUrl": "https://pay.sandbox.datatrans.com/upp/merchant/successPage.jsp",
    "VIS": {
        "3D": {          
            "acquirer": {
                "acquirerBin": "658942",
                "acquirerMerchantId": "XCGHPB1U0ZIK459"
            },
            "merchant": {
                "mcc": "4722",
                "merchantName": "Test-OTA"
            }
        }
    },
    "ECA": {
        "3D": {         
            "acquirer": {
                "acquirerBin": "357941",
                "acquirerMerchantId": "XLKDPB1U0ZIK658"
            },
            "merchant": {
                "mcc": "4722",
                "merchantName": "Test-OTA"
            }
        }
    }.
   "AMX": {
        "3D": {         
            "acquirer": {
                "acquirerBin": "",
                "acquirerMerchantId": "9999999999"
            },
            "merchant": {
                "mcc": "4722",
                "merchantName": "Test-OTA"
            }
        }
    }
 }' 
```
{% endtab %}

{% tab title="Response" %}
```java
{
  "transactionId" : "190510170631533875"
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If the initial server to server call failed, you will receive one of these [error codes](../../initialization-errors.md).
{% endhint %}

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
        <p>Acquirer Merchant ID - Acquirer-assigned Merchant identifier.</p>
        <p>This may be the same value that is used in authorisation requests sent
          on behalf of the 3DS Requestor and is represented in ISO 8583 formatting
          requirements.</p>
        <p>Length: Variable, maximum 35 characters</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>acquirerBin</code>
      </td>
      <td style="text-align:left">
        <p>Acquirer BIN - Acquiring institution identification code as assigned by
          the DS receiving the AReq message.</p>
        <p>Length: Variable, maximum 11 characters.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>mcc</code>
      </td>
      <td style="text-align:left">
        <p>Merchant Category Code - DS-specific code describing the Merchant&#x2019;s
          type of business, product or service. The four-digit MCC registered with
          the schemes for the same <code>acquirerMerchantID</code> sent in the request.</p>
        <p>Length: 4 characters</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>merchantName</code>
      </td>
      <td style="text-align:left">
        <p>Merchant Name - Merchant name assigned by the Acquirer or Payment System;
          it is the merchant name that the issuer presents to the cardholder if they
          get a challenge.</p>
        <p>Length: Variable, maximum 40 characters</p>
      </td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
Above mentioned data are only required for Visa and Mastercard. If you need to authenticate AMEX as well please contact us. 
{% endhint %}

## Step 2: Setup SecureFields

To get started include the following script on your page.

{% tabs %}
{% tab title="SecureFields Script" %}
```markup
<script src="https://pay.sandbox.datatrans.com/upp/payment/js/secure-fields-2.0.0.js"></script>
```
{% endtab %}

{% tab title="Minified version" %}
```markup
<script src="https://pay.sandbox.datatrans.com/upp/payment/js/secure-fields-2.0.0.min.js"></script>
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Please make sure to always load it directly from [https://pay.sandbox.datatrans.com](https://pay.sandbox.datatrans.com)
{% endhint %}

## Step 3: Create payment form 

In order for Secure Fields to insert the card number and CVV iframes at the right place, create empty DOM elements and assign them unique IDs. In the example below those are:

* `card-number-placeholder`
* `cvv-placeholder`

```java
<form>
    <div>
        <div>
            <label for="card-number-placeholder">Card Number</label>
            <!-- card number container -->
            <div id="card-number-placeholder" style="width: 250px;"></div>
        </div>
        <div>
            <label for="cvv-placeholder">Cvv</label>
            <!-- cvv container -->
            <div id="cvv-placeholder" style="width: 90px;"></div>
        </div>

        <button type="button" id="go">Get Token!</button>
    </div>
</form>
```

## Step 4: Initialize Secure Fields with the transactionId

Start with creating a new Secure Fields instance: 

```java
var secureFields = new SecureFields();

// Multiple instances might be created and used independently:
// e.g. var secureFields2 = new SecureFields();
```

Initialize it with your `transactionId` and specify which DOM element containers should be used to inject the iframes:

```java
    secureFields.init(
      '190520110934541218',
      {
        cardNumber: {
           placeholderElementId: 'card-number-placeholder',
           inputType: 'tel'
        },
        cvv:  {
           placeholderElementId: 'cvv-placeholder',
           inputType: 'tel'
        }
      },
      {
        debug: true
      }
    );
```

Afterwards add parameter `expm` and `expy` , submit the form and listen for the success event:

```java
$(function() {
  $("#go").click( function() {
      secureFields.submit({ // submit the "form"
        expm: 12,
        expy: 21
      });
   });
});

secureFields.on("success", function(data) {
  if(data.transactionId) {
    // transmit data.transactionId and the rest
    // of the form to your server.
    // redirect the customers browser to the URL
    // within data.redirect. See Step 5. 
  }
});
```

## Step 5: Display a 3D secure challenge

The `success` event returns a `redirect` attribute which contains the 3D URL if a challenge is required. Redirect the card holder to this URL to trigger the 3D authentication process. 

It is recommended to do the redirect to the 3D URL in the `_top` window. It is not guaranteed that the various 3D ACS pages allow being iFramed or are displayed properly in an iFrame.

Once the card holder completed the 3D process, the browser will be redirected to the `returnUrl` passed to the `/v1/transactions/secureFields` API, with a POST request containing the variables `upptransactionId` and `status_3d` .

## Step 6: Obtain 3D parameters and tokens

{% api-method method="get" host="https://api.sandbox.datatrans.com" path="/v1/transactions/{transactionId}" %}
{% api-method-summary %}
Status API
{% endapi-method-summary %}

{% api-method-description %}
Obtain the 3D parameters, credit card and cvv tokens by executing a server to server call with the `transactionId` received in step 1.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Basic MTEwMDAwNzAwNjpLNnFYMXUklq==  
see Setup
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="transactionId" type="string" required=true %}
The `transactionId` obtained via initial`/v1/transactions/secureFields` call
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Returns the credit card and CVV code tokens as well as the "3D" object
{% endapi-method-response-example-description %}

{% code title="Example response" %}
```java
{
    "transactionId": "190520111958152753",
    "type": "payment",
    "status": "authenticated",
    "currency": "CHF",
    "refno": "N/A",
    "paymentMethod": "ECA",
    "detail": {
        "authorize": {
            "amount": 10
        }
    },
    "card": {
        "alias": "AAABcHxr-sDssdexyrAAAfyXWIgaAF40",
        "masked": "520000xxxxxx0080",
        "aliasCVV": "WWguOT-vQKybTMo1CALTjjwZ",
        "expiryMonth": "12",
        "expiryYear": "21",
        "info": {
            "brand": "MASTERCARD",
            "type": "credit",
            "usage": "consumer",
            "country": "RO",
            "issuer": "DATATRANS"
        },
        "3D": {
            "eci": "02",
            "xid": "1f88043a-7d5c-431b-be5d-bfebd6088992",
            "cavv": "OTkxOTA1MjAxMTIxMDU2MTI4NzM=",
            "threeDSVersion": "2.1.0",
            "directoryResponse": "Y",
            "authenticationResponse": "Y",
            "cardHolderInfo": "Detailed issuer notification if available",
            "threeDSTransactionId": "8558c931-277b-4240-adfc-443cbd61a2c0"
        }
    }
}
```
{% endcode %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

#### Examples

{% tabs %}
{% tab title="Request" %}
```java
curl -u 1100018081:2fgVhQOYZK0io9ct  https://api.sandbox.datatrans.com/v1/transactions/190510164649321735
```
{% endtab %}

{% tab title="Response" %}
```java
{
    "transactionId": "190520111958152753",
    "type": "payment",
    "status": "authenticated",
    "currency": "EUR",
    "refno": "N/A",
    "paymentMethod": "ECA",
    "detail": {
        "authorize": {
            "amount": 1000
        }
    },
    "card": {
        "alias": "AAABcHxr-sDssdexyrAAAfyXWIgaAF40",
        "masked": "520000xxxxxx0080",
        "aliasCVV":"WWguOT-vQKybTMo1CALTjjwZ",
        "expiryMonth": "12",
        "expiryYear": "21",
        "info": {
            "brand": "MASTERCARD",
            "type": "credit",
            "usage": "consumer",
            "country": "RO",
            "issuer": "DATATRANS"
        },
        "3D": {
          "eci": "02",
          "xid": "1f88043a-7d5c-431b-be5d-bfebd6088992",
          "cavv": "OTkxOTA4MDkxNjMzMTYwNTUwMzY=",
          "threeDSVersion": "2.1.0",          
          "directoryResponse": "Y",
          "authenticationResponse": "Y",
          "cardHolderInfo": "Detailed issuer notification if available",
          "threeDSTransactionId": "8558c931-277b-4240-adfc-443cbd61a2c0"
        }
    }
}
```
{% endtab %}
{% endtabs %}

#### 3D object field name mapping  

<table>
  <thead>
    <tr>
      <th style="text-align:left">Datatrans</th>
      <th style="text-align:left">EMVCo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p><code>eci - string, 2 characters</code>
        </p>
        <p>The Electronic Commerce Indicator</p>
      </td>
      <td style="text-align:left"><code>eci</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>xid - string</code>
        </p>
        <p>The transaction ID returned by the directory server</p>
      </td>
      <td style="text-align:left">
        <p><code>dsTransId</code> (3Dv2)</p>
        <p><code>xid</code> (3Dv1)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>cavvAlgorithm - string</code>
        </p>
        <p>The 3D algorithm</p>
      </td>
      <td style="text-align:left">Only required for 3D Secure 1</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>cavv - string</code>
        </p>
        <p>The Cardholder Authentication Verification Value</p>
      </td>
      <td style="text-align:left"><code>authenticationValue</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>threeDSVersion - string</code>
        </p>
        <p>The 3D version</p>
      </td>
      <td style="text-align:left"><code>messageVersion</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>directoryResponse - string, 1 character</code> 
        </p>
        <p>Transaction status after <code>ARes </code>
        </p>
      </td>
      <td style="text-align:left">
        <p><code>transStatus </code>
        </p>
        <p>(after ARes)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>authenticationResponse - string, 1 character</code> 
        </p>
        <p>Transaction status after <code>RReq</code> 
        </p>
      </td>
      <td style="text-align:left">
        <p><code>transStatus </code>
        </p>
        <p>(after RReq)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>threeDSTransactionId - string</code>
        </p>
        <p>Universally unique transaction identifier assigned by the 3DS Server to
          identify a single transaction.</p>
      </td>
      <td style="text-align:left">threeDSServerTransID</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>cardHolderInfo - string</code>
        </p>
        <p>Text provided by the ACS/Issuer to Cardholder during a Frictionless transaction
          that was not authenticated by the ACS. The Issuer can optionally provide
          information to Cardholder. For example, &#x201C;<em>Additional authentication is needed for this transaction, please contact (Issuer Name) at xxx-xxx-xxxx.</em>&#x201D;</p>
      </td>
      <td style="text-align:left"><code>cardholderInfo</code>
      </td>
    </tr>
  </tbody>
</table>

#### Directory Response \(Transaction status after `ARes`\)

| Value | 3Dv2 |
| :--- | :--- |
| Y | authenticated |
| N | authentication failed |
| U | not available |
| C | challenge needed |
| R | rejected |
| A | authentication attempt |

#### Authentication Response \(Transaction status after `RReq` \(Challenge flow\)\)

| Value  | 3Dv2 |
| :--- | :--- |
| Y | authenticated |
| N | authentication failed |
| U | not available |
| A | authentication attempt |
| C | process incomplete |

## Step 7: Forward 3D data

Received `"3D"` object contains parameters with the result of the 3D-Secure process and can be forwarded to 3rd party payment gateway. If you decide to use Datatrans payment gateway please continue with our [Authorize](../../authorize-1/authorize.md) API.

## Examples

Find a working sample here \(change the transactionId all the time\):   
[https://github.com/datatrans/secure-fields-sample/blob/secure-fields-init-with-transactionId/index.html](https://github.com/datatrans/secure-fields-sample/blob/secure-fields-init-with-transactionId/index.html)

