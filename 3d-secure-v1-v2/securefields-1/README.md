---
description: >-
  Use Secure Fields integration for Tokenisation and Authentication only in your
  frontend.
---

# SecureFields 3D \(beta\)

## Before you start

1. \*\*\*\*[**Sign up** ](https://dashboard.pci-proxy.com/signup)for a free PCI Proxy sandbox account.

{% hint style="info" %}
* This service requires basic authentication. Please refer to [Authentification](../../guides/pci-proxy-dashboard/api-authentication-data.md) to retrieve required crendetials. 
* Make sure to use our 3D Secure enabled test credit cards [here](../testing-3d-secure.md).
{% endhint %}

{% hint style="warning" %}
**3D Secure Enrollment Requirements**

Secure Fields 3D requires a 3D Secure enrolled acquiring contract that needs to be activated on your account \(`merchantId`\). 
{% endhint %}

## Step 1: Initial Server-to-Server call

{% api-method method="post" host="https://api.sandbox.datatrans.com" path="/v1/transactions/secureFields" %}
{% api-method-summary %}
Init call
{% endapi-method-summary %}

{% api-method-description %}
Initial Server-to-Server call to retrieve transactionId and submit 3D v1/v2 parameters. 
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
Transaction amount in the currency's smalles unit. For example use 1000 for EU 10.00
{% endapi-method-parameter %}

{% api-method-parameter name="currency" type="string" required=true %}
3 letter ISO-4217 character. For example CHF or USD
{% endapi-method-parameter %}

{% api-method-parameter name="returnUrl" type="string" required=true %}
Your 3D process return URL
{% endapi-method-parameter %}

{% api-method-parameter name="card" type="object" required=false %}
Object used for additional 3D v2 parameters
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
 Refer to the official EMVCo 3D specification 2.1.0 for parameter requirements sent in the `card` object. [https://www.emvco.com/emv-technologies/3d-secure/](https://www.emvco.com/emv-technologies/3d-secure/)
{% endhint %}

#### The transactionId returned in the response of the init call

```java
{
    "transactionId": "190520110934541218",
}
```

#### Examples

{% tabs %}
{% tab title="Request" %}
```java
curl -v -u 1100018081:2fgVhQOYZK0io9ct 'https://api.sandbox.datatrans.com/v1/transactions/secureFields' \
    -H 'Content-Type: application/json; charset=UTF-8' \
    -d '{
    "amount" : 1000,
    "currency" : "EUR",
    "returnUrl": "https://pay.sandbox.datatrans.com/upp/merchant/successPage.jsp",
    "card": {
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

In order for Secure Fields to insert card number and CVV iframes at the right place, create empty DOM elements and assign them unique IDs. In the example below those are:

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

The `success` event returns a `redirect` attribute which contains the 3D URL. To present a challenge flow, redirect the card holder to this URL to trigger 3D authentication process. Once the card holder completed the 3D process, he will be redirected to the `returnUrl` passed to the `/v1/transactions/secureFields` API. 

## Step 6: Obtain 3D parameters and tokens

{% api-method method="get" host="https://api.sandbox.datatrans.com" path="/v1/transactions/{transactionId}" %}
{% api-method-summary %}
Status API
{% endapi-method-summary %}

{% api-method-description %}
Obtain 3D parameters, credit card and cvv token by executing a server to server call with the `transactionId` received in step 1 
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
Returns Creditcard and CVV code tokens as well as the "3D" object
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
        "alias": "520000RIVWAS0080",
        "masked": "520000xxxxxx0080",
        "aliasCVV":"WWguOT-vQKybTMo1CALTjjwZ",
        "expiryMonth": "12",
        "expiryYear": "21",
        "3D": {
            "eci": "02",
            "xid": "MDAxOTA1MjAxMTE5NTgxNTI3NTM=",
            "cavv": "OTkxOTA1MjAxMTIxMDU2MTI4NzM=",
            "threeDSVersion": "1.0.2",
            "directoryResponse": "Y",
            "authenticationResponse": "A"
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
        "3D": {
          "eci": "02",
          "xid": "MDAxOTA4MDkxNjMzMDkzNTUwMDQ=",
          "cavv": "OTkxOTA4MDkxNjMzMTYwNTUwMzY=",
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
</table>## Step 7: Forward 3D data

Received `"3D"` object contains parameters with the result of the 3D-Secure process and can be forwarded to 3rd party payment gateway. If you decide to use Datatrans payment gateway please continue with our [Authorize](../authorize.md) API.

## Examples

Find a working sample here \(change transactionId all the time\):   
[https://github.com/datatrans/secure-fields-sample/blob/secure-fields-init-with-transactionId/index.html](https://github.com/datatrans/secure-fields-sample/blob/secure-fields-init-with-transactionId/index.html)

