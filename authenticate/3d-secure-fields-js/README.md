# 3D Secure Fields (JS)

**3D Secure Fields (JS)** allow you to securely collect and tokenize sensitive card data by injecting iframes to your DOM and perform an Authentication Only call to authenticate a cardholder via 3D Secure Fields.

## Before you start

{% hint style="info" %}
Make sure to use our 3D Secure enabled test credit cards [here](../../resources/test-credentials.md).
{% endhint %}

**3D Secure Enrolment Requirements**

{% hint style="warning" %}
Secure Fields 3D requires a 3D Secure enrolled acquiring contract for each card brand. Those 3-D acquiring data needs to be sent in the initial call to `/v1/transactions/secureFields`&#x20;
{% endhint %}

## Step 1: Initial Server-to-Server call

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/transactions/secureFields" method="post" summary="Init call" %}
{% swagger-description %}
Initial Server-to-Server call to retrieve the transactionId and submit the optional 3D parameters.&#x20;

The parameters marked with \* are mandatory.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==

\


see API Authentication data
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
API consumes application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="integer" %}
Transaction amount in the currency's smallest unit. For example use 1000 for EUR 10.00
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="string" required="true" %}
3 letter ISO-4217 character. For example EUR or USD
{% endswagger-parameter %}

{% swagger-parameter in="body" name="returnUrl" type="string" required="true" %}
Your 3D process return URL
{% endswagger-parameter %}

{% swagger-parameter in="body" name="AMX" type="object" %}
Object used for AMEX 3D acquiring data
{% endswagger-parameter %}

{% swagger-parameter in="body" name="VIS" type="object" %}
Object used for VISA 3D acquiring data
{% endswagger-parameter %}

{% swagger-parameter in="body" name="ECA" type="object" %}
Object used for Mastercard 3D acquiring data
{% endswagger-parameter %}

{% swagger-response status="201" description="" %}
```java
{
    "transactionId": "190520110934541218",
}
```
{% endswagger-response %}

{% swagger-response status="400" description="the amount must be at least in the currency's smallest unit. " %}
```java
{
    "error": {
        "code": "INVALID_PROPERTY",
        "message": "init.amount must be > 0"
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% hint style="info" %}
3D Secure 2 allows you to send additional, optional data to ensure increased acceptance and frictionless rate at the issuer. Please refer to the official EMVCo 3D specification 2.1.0 for parameter requirements sent in the card brands object. [https://www.emvco.com/emv-technologies/3d-secure/](https://www.emvco.com/emv-technologies/3d-secure/) or contact us for more information.&#x20;
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
    },
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

If the initial server to server call failed, you will receive one of these error codes:&#x20;

> "`UNKNOWN_ERROR`", "`UNAUTHORIZED`", "`INVALID_JSON_PAYLOAD`", "`UNRECOGNIZED_PROPERTY`", "`INVALID_PROPERTY`", "`CLIENT_ERROR`", "`SERVER_ERROR`", "`INVALID_TRANSACTION_STATUS`", "`TRANSACTION_NOT_FOUND`", "`EXPIRED_CARD`", "`INVALID_CARD`", "`BLOCKED_CARD`", "`UNSUPPORTED_CARD`", "`INVALID_ALIAS`", "`INVALID_CVV`", "`DUPLICATE_REFNO`", "`DECLINED`", "`SOFT_DECLINED`", "`INVALID_SIGN`", "`BLOCKED_BY_VELOCITY_CHECKER`", "`THIRD_PARTY_ERROR`", "`REFERRAL`", "`INVALID_SETUP`".

#### 3D Secure Acquirer related data

To use the Authentication only API you need to get the following information from your acquirer as they are part of the 3-D Secure 2 enrolment process between your acquirer and the card schemes.

| Name                 | Description                                                                                                                                                                                                                                                                              |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `acquirerMerchantId` | <p>Acquirer Merchant ID - Acquirer-assigned Merchant identifier. </p><p>This may be the same value that is used in authorisation requests sent on behalf of the 3DS Requestor and is represented in ISO 8583 formatting requirements. </p><p>Length: Variable, maximum 35 characters</p> |
| `acquirerBin`        | <p>Acquirer BIN - Acquiring institution identification code as assigned by the DS receiving the AReq message. </p><p>Length: Variable, maximum 11 characters.</p>                                                                                                                        |
| `mcc`                | <p>Merchant Category Code - DS-specific code describing the Merchant’s type of business, product or service.  The four-digit MCC registered with the schemes for the same <code>acquirerMerchantID</code> sent in the request.</p><p>Length: 4 characters</p>                            |
| `merchantName`       | <p>Merchant Name - Merchant name assigned by the Acquirer or Payment System; it is the merchant name that the issuer presents to the cardholder if they get a challenge. </p><p>Length: Variable, maximum 40 characters</p>                                                              |

{% hint style="warning" %}
Above mentioned data are only required for Visa and Mastercard. If you need to authenticate AMEX as well please contact us.&#x20;
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
Please make sure to always load it directly from [https://pay.sandbox.datatrans.com](https://pay.sandbox.datatrans.com/upp/payment/js/secure-fields-2.0.0.js)
{% endhint %}

## Step 3: Create the payment form&#x20;

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

Start with creating a new Secure Fields instance:&#x20;

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

Afterwards add the parameters `expm` and `expy` , submit the form and listen for the success event:

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

The `success` event returns a `redirect` attribute which contains the 3D URL if a challenge is required. Redirect the cardholder to this URL to trigger the 3D authentication process.&#x20;

Once the cardholder completed the 3D process, the browser will be redirected to the `returnUrl` passed to the `/v1/transactions/secureFields` API, with a POST request containing the variables `uppTransactionId` and `status_3d` .

## Step 6: Obtain 3D parameters and tokens

Obtain the D parameters, the credit card and cvv tokens by executing a server to server call with the `transactionId` received in step 1.

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/transactions/{transactionId}" method="get" summary="Status API" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Basic MTEwMDAwNzAwNjpLNnFYMXUklq==

\


see Setup
{% endswagger-parameter %}

{% swagger-parameter in="query" name="transactionId" type="string" required="true" %}
The 

`transactionId`

 obtained via initial

`/v1/transactions/secureFields`

 call
{% endswagger-parameter %}

{% swagger-response status="200" description="Returns the credit card and CVV code tokens as well as the "3D" object" %}
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
{% endswagger-response %}
{% endswagger %}

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
        "fingerprint": "F-dV5V8dE0SZLoTurWbq2HZp",
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
          "transStatusReason": "01",
          "cardHolderInfo": "Detailed issuer notification if available",
          "threeDSTransactionId": "8558c931-277b-4240-adfc-443cbd61a2c0"
        }
    }
}
```
{% endtab %}
{% endtabs %}

#### 3D object field name mapping &#x20;



| Datatrans                | EMVCo                                                                                                           | Description                                                     |
| ------------------------ | --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| `eci`                    | [eci](../3d-secure-terminology.md#eci-electronic-commerce-indicator)                                            | The Electronic Commerce Indicator                               |
| `xid`                    | <p><a href="../3d-secure-terminology.md#dstransid-ds-transaction-id">dsTransId</a> (3Dv2)</p><p>xid (3Dv1)</p>  | The transaction ID returned by the directory server             |
| `cavvAlgorithm`          | Only required for 3D Secure 1                                                                                   | The 3D algorithm                                                |
| `cavv`                   | [authenticationValue](../3d-secure-terminology.md#authenticationvalue-authentication-value)                     | The Cardholder Authentication Verification Value                |
| `threeDSVersion`         | [messageVersion](../3d-secure-terminology.md#messageversion-message-version-number)                             | The 3D version                                                  |
| `directoryResponse`      | <p><a href="../3d-secure-terminology.md#transstatus-transaction-status">transStatus</a> </p><p>(after ARes)</p> | Transaction status after `ARes`                                 |
| `authenticationResponse` | <p><a href="../3d-secure-terminology.md#transstatus-transaction-status">transStatus </a></p><p>(after RReq)</p> | Transaction status after `RReq`                                 |
| `threeDSTransactionId`   | [threeDSServerTransID](../3d-secure-terminology.md#threedsservertransid-3ds-server-transaction-id)              | Universally unique transaction identifier.                      |
| `cardHolderInfo`         | [cardholderInfo](../3d-secure-terminology.md#cardholderinfo-cardholder-information-text)                        | Optional message provided by the ACS/Issuer to the Cardholder   |
| `transStatusReason`      | [transStatusReason](../3d-secure-terminology.md#transstatusreason-transaction-status-reason)                    | Provides additional information on the failed 3D authentication |

### Directory response & authentication response

We return the directory response for any transaction where a 3D Secure verification can take place and the authentication response for any transaction where a 3D Secure challenge flow was completed. In other words: directoryResponse tells you if a card is enrolled or needs authentication and authenticationResponse returns the challenge flow response.

#### Directory Response (Transaction status after `ARes`)

<table><thead><tr><th width="150">Value</th><th width="215">3Dv2</th><th>Description</th></tr></thead><tbody><tr><td><code>Y</code></td><td>authenticated</td><td>The card or account was authenticated seamlessly with 3D Secure. No challenge flow will take place.</td></tr><tr><td><code>N</code></td><td>authentication failed</td><td>Not authenticated</td></tr><tr><td><code>U</code></td><td>not available</td><td>The authentication or account verification could not be performed. This is usually linked to technical problems.</td></tr><tr><td><code>C</code></td><td>challenge needed</td><td>Further cardholder interaction is required to complete the authentication.</td></tr><tr><td><code>R</code></td><td>rejected</td><td>Not authenticated because the issuer is rejecting authentication.</td></tr><tr><td><code>A</code></td><td>authentication attempt</td><td>A proof of authentication attempt was generated. One or more 3D Secure authentication attempts were performed but no authentication or account verification was completed successfully. This serves as a proof that 3D Secure authentication was attempted and may also be returned if a cardholder skips the 3D Secure registration.</td></tr></tbody></table>

#### Authentication Response (Transaction status after `RReq`(Challenge flow))

<table><thead><tr><th width="150">Value </th><th>3Dv2</th><th>Description</th></tr></thead><tbody><tr><td><code>Y</code></td><td>authenticated</td><td>The authentication was successful.</td></tr><tr><td><code>N</code></td><td>authentication failed</td><td>The authentication or account could not be verified. This will be returned when the authentication fails.</td></tr><tr><td><code>U</code></td><td>not available</td><td>The authentication or account verification could not be performed. This is usually linked to technical problems.</td></tr><tr><td><code>A</code></td><td>authentication attempt</td><td>A proof of authentication attempt was generated. One or more 3D Secure authentication attempts were performed but no authentication or account verification was completed successfully. This serves as a proof that 3D Secure authentication was attempted and may also be returned if a cardholder skips the 3D Secure registration.</td></tr><tr><td><code>C</code></td><td>process incomplete</td><td>Further cardholder interaction is required to complete the authentication.</td></tr></tbody></table>

## Step 7: Forward 3D Secure data

The received `"3D"` object contains parameters with the result of the 3D Secure process and can be forwarded to 3rd party payment gateway. If you decide to use Datatrans payment gateway please continue with our [Authorize API](https://api-reference.datatrans.ch/#operation/authorize).

## Examples

Find a working sample here (change the transactionId all the time): \
[https://github.com/datatrans/secure-fields-sample/blob/secure-fields-init-with-transactionId/index.html](https://github.com/datatrans/secure-fields-sample/blob/secure-fields-init-with-transactionId/index.html)
