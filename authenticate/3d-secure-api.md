# 3D Secure API

<mark style="color:blue;">**3D Secure API**</mark> allows you to perform a standalone 3DS authentication. This makes sense if you're a PCI DSS level 1 merchant or service provider only using our 3DS services or if you want to decouple the card capturing from the authentication process.&#x20;

## Before you start

1. [**Sign up**](https://dashboard.pci-proxy.com/signup) for a free PCI Proxy sandbox account.

{% hint style="info" %}
* This service requires basic authentication. Please refer to [Authentication](../resources/pci-proxy-dashboard/api-authentication-data.md) to retrieve the required credentials.&#x20;
* Make sure to use our 3D Secure enabled test credit cards [here](../resources/test-credentials.md#test-3d-secure-cards).
{% endhint %}

{% hint style="warning" %}
**3D Secure Enrolment Requirements**

3D Secure API requires a 3-D Secure enrolled acquiring contract. Those 3D Secure acquiring data has to be sent dynamically in the initial request to `/v1/transactions`
{% endhint %}

## Step 1: Initial Server-to-Server call

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/transactions" method="post" summary="Init call" %}
{% swagger-description %}
Initial Server-to-Server call to retrieve transactionId and submit 3D Secure v2 parameters.&#x20;

The parameters marked with \* are mandatory.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==

\


see Setup
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
API consumes application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="integer" %}
Transaction in the currency's smallest unit. For example use 1000 for EUR 10.00
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="string" required="true" %}
3 letter ISO-4217 character code. For example 

`EUR`

 or 

`USD`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="refno" type="string" %}
\[1..20] characters

\


It should be unique each transaction
{% endswagger-parameter %}

{% swagger-parameter in="body" name="paymentMethods" type="array" required="true" %}
An array with one element: payment method shortname

\




`"AMX"`

 

`"CUP"`

 

`"ECA"`

 

`"DIN"`

 

`"DIS"`

 

`"JCB"`

 

`"VIS"`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="card" type="object" %}
card object must contain following parameters below
{% endswagger-parameter %}

{% swagger-parameter in="body" name="number" type="string" %}
Plain text card number or
{% endswagger-parameter %}

{% swagger-parameter in="body" name="alias" type="string" %}
PCI Proxy token
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiryMonth" type="string" %}
Expiry month of card (2 characters)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiryYear" type="string" %}
Expiry year of card (2 characters)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="3D" type="object" %}
3D object for the 3D v2 parameters

\


See the hint box below for additional information.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="option" type="string" %}
option object must contain the following parameters below
{% endswagger-parameter %}

{% swagger-parameter in="body" name="authenticationOnly" type="boolean" required="false" %}
true
{% endswagger-parameter %}

{% swagger-parameter in="body" name="redirect" type="object" %}
redirect object must contain following parameters below
{% endswagger-parameter %}

{% swagger-parameter in="body" name="successUrl" type="string" %}
URL where cardholder will be redirect in case of successful 3D process
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cancelUrl" type="string" %}
URL where cardholder will be redirected in case of  cancelled 3D process
{% endswagger-parameter %}

{% swagger-parameter in="body" name="errorUrl" type="string" %}
URL where cardholder will be redirected in case of an error in 3D process
{% endswagger-parameter %}

{% swagger-response status="201" description="Returns the transactionId and wheter the card is enrolled for 3D or not. " %}
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
{% endswagger-response %}

{% swagger-response status="400" description="Invalid Request: Returns error object with an error code and an error message." %}
```javascript
{
  "error": {
    "code": "INVALID_PROPERTY",
    "message": "init.refno must not be null"
  }
}
```
{% endswagger-response %}
{% endswagger %}

{% hint style="info" %}
Refer to the official EMVCo 3D specification 2.1.0 for parameter requirements sent in the `3D`object. [https://www.emvco.com/emv-technologies/3d-secure/](https://www.emvco.com/emv-technologies/3d-secure/)
{% endhint %}

#### Examples

{% tabs %}
{% tab title="Request with token" %}
```javascript
curl -X POST \
  https://api.sandbox.datatrans.com/v1/transactions \
  -H 'Authorization: Basic MTEwMDAxNzY3NTpTejdodE5uSjdNM05YQ0lT' \
  -d '{
    "amount": 1000,
    "currency": "EUR",
    "refno": "NIJ3OSelzyqp",
    "paymentMethods": ["ECA"],
    "card": {
        "alias": "AAABcHxr-sDssdexyrAAAfyXWIgaAF40", 
        "expiryMonth": "06",
        "expiryYear": "25",
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
  -H 'Authorization: Basic MTEwMDAxNzY3NTpTejdodE5uSjdNM05YQ0lT' \
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
            "acquirer": {
            		"acquirerMerchantId": "1234567",
            		"acquirerBin": "9876543"
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

{% hint style="info" %}
To send additional 3D parameters, please check the `card.3D` object here: [https://api-reference.datatrans.ch/#operation/init](https://api-reference.datatrans.ch/#operation/init)
{% endhint %}

If the initialization failed, you will receive one of the of the following error codes.&#x20;

> "`UNKNOWN_ERROR`", "`UNAUTHORIZED`", "`INVALID_JSON_PAYLOAD`", "`UNRECOGNIZED_PROPERTY`", "`INVALID_PROPERTY`", "`CLIENT_ERROR`", "`SERVER_ERROR`", "`INVALID_TRANSACTION_STATUS`", "`TRANSACTION_NOT_FOUND`", "`EXPIRED_CARD`", "`INVALID_CARD`", "`BLOCKED_CARD`", "`UNSUPPORTED_CARD`", "`INVALID_ALIAS`", "`INVALID_CVV`", "`DUPLICATE_REFNO`", "`DECLINED`", "`SOFT_DECLINED`", "`INVALID_SIGN`", "`BLOCKED_BY_VELOCITY_CHECKER`", "`THIRD_PARTY_ERROR`", "`REFERRAL`", "`INVALID_SETUP`".

#### 3D Secure Acquirer related data

To use the Authentication only API you need to get the following information from your acquirer as they are part of the 3D Secure 2 enrolment process between your acquirer and card schemes.

| Name                 | Description                                                                                        |
| -------------------- | -------------------------------------------------------------------------------------------------- |
| `acquirerMerchantId` | <p>Acquirer Merchant ID</p><p>Acquirer-assigned Merchant identifier</p>                            |
| `acquirerBin`        | <p>Acquirer BIN</p><p>Acquiring institution identification code</p>                                |
| `mcc`                | <p>Merchant Category Code</p><p>Describes the Merchant’s type of business, product or service.</p> |
| `merchantName`       | <p>Merchant Name</p><p>Name which will be displayed on the ACS page. </p>                          |

## Step 2: Display a 3D Secure challenge

In the body of the response, you receive the `transactionID` and in the location header the `3D-redirect`URL. Redirect the cardholder to this URL to trigger the 3D Secure process. Once the cardholder completed the 3D Secure process, he will be redirected to the `successUrl` passed to the `v1/transactions` API.&#x20;

## Step 3: Obtain 3D parameters

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/transactions/{transactionId}" method="get" summary="Status API" %}
{% swagger-description %}
Obtain 3D parameters, credit card and cvv token by executing a server to server call with the `transactionId` received in step 1.&#x20;

The parameters marked with \* are mandatory.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==

\


see setup
{% endswagger-parameter %}

{% swagger-parameter in="query" name="transactionId" type="string" required="true" %}
transactionId obtained via 

`/v1/transactions`
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
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
            "authenticationResponse": "Y",
            "cardHolderInfo": "Detailed issuer notification if available",
            "threeDSTransactionId": "8558c931-277b-4240-adfc-443cbd61a2c0"
        }
    }
}
```
{% endswagger-response %}
{% endswagger %}

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
      "authenticationResponse": "Y",
      "cardHolderInfo": "Detailed issuer notification if available",
      "threeDSTransactionId": "8558c931-277b-4240-adfc-443cbd61a2c0"
    }
  }
}
```
{% endtab %}
{% endtabs %}

####

#### 3D object field name mapping &#x20;

| Datatrans                | EMVCo                                                                                                        | Description                                                     |
| ------------------------ | ------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------- |
| `eci`                    | [eci](3d-secure-terminology.md#eci-electronic-commerce-indicator)                                            | The Electronic Commerce Indicator                               |
| `xid`                    | <p><a href="3d-secure-terminology.md#dstransid-ds-transaction-id">dsTransId</a> (3Dv2)</p><p>xid (3Dv1)</p>  | The transaction ID returned by the directory server             |
| `cavvAlgorithm`          | Only required for 3D Secure 1                                                                                | The 3D algorithm                                                |
| `cavv`                   | [authenticationValue](3d-secure-terminology.md#authenticationvalue-authentication-value)                     | The Cardholder Authentication Verification Value                |
| `threeDSVersion`         | [messageVersion](3d-secure-terminology.md#messageversion-message-version-number)                             | The 3D version                                                  |
| `directoryResponse`      | <p><a href="3d-secure-terminology.md#transstatus-transaction-status">transStatus</a> </p><p>(after ARes)</p> | Transaction status after `ARes`                                 |
| `authenticationResponse` | <p><a href="3d-secure-terminology.md#transstatus-transaction-status">transStatus </a></p><p>(after RReq)</p> | Transaction status after `RReq`                                 |
| `threeDSTransactionId`   | [threeDSServerTransID](3d-secure-terminology.md#threedsservertransid-3ds-server-transaction-id)              | Universally unique transaction identifier.                      |
| `cardHolderInfo`         | [cardholderInfo](3d-secure-terminology.md#cardholderinfo-cardholder-information-text)                        | Optional message provided by the ACS/Issuer to the Cardholder   |
| `transStatusReason`      | [transStatusReason](3d-secure-terminology.md#transstatusreason-transaction-status-reason)                    | Provides additional information on the failed 3D authentication |

### Directory response & authentication response

We return the directory response for any transaction where a 3D Secure verification can take place and the authentication response for any transaction where a 3D Secure challenge flow was completed. In other words: directoryResponse tells you if a card is enrolled or needs authentication and authenticationResponse returns the challenge flow response.

#### Directory Response (Transaction status after `ARes`)

| Value | 3Dv2                   | Description                                                                                                                                                                                                                                                                                                                                                  |
| ----- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `Y`   | authenticated          | The card or account was authenticated seamlessly with 3D Secure. No challenge flow will take place.                                                                                                                                                                                                                                                          |
| `N`   | authentication failed  | Not authenticated.                                                                                                                                                                                                                                                                                                                                           |
| `U`   | not available          | The authentication or account verification could not be performed. This is usually linked to technical problems.                                                                                                                                                                                                                                             |
| `C`   | challenge needed       | Further cardholder interaction is required to complete the authentication.                                                                                                                                                                                                                                                                                   |
| `R`   | rejected               | Not authenticated because the issuer is rejecting authentication.                                                                                                                                                                                                                                                                                            |
| `A`   | authentication attempt | Not authenticated, but a proof of authentication attempt was generated. One or more 3D Secure authentication attempts were performed but no authentication or account verification was completed successfully. This serves as a proof that 3D Secure authentication was attempted and may also be returned if a cardholder skips the 3D Secure registration. |

#### Authentication Response (Transaction status after `RReq` (Challenge flow))

| Value  | 3Dv2                   | Description                                                                                                                                                                                                                                                                                                                                                  |
| ------ | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `Y`    | authenticated          | The authentication was successful.                                                                                                                                                                                                                                                                                                                           |
| `N`    | authentication failed  | The authentication or account could not be verified. This will be returned when the authentication fails.                                                                                                                                                                                                                                                    |
| `U`    | not available          | The authentication or account verification could not be performed. This is usually linked to technical problems.                                                                                                                                                                                                                                             |
| `A`    | authentication attempt | Not authenticated, but a proof of authentication attempt was generated. One or more 3D Secure authentication attempts were performed but no authentication or account verification was completed successfully. This serves as a proof that 3D Secure authentication was attempted and may also be returned if a cardholder skips the 3D Secure registration. |
| `C`    | process incomplete     | Further cardholder interaction is required to complete the authentication. The authentication process is incomplete.                                                                                                                                                                                                                                         |

## Step 4: Forward 3D Secure data

The received `"3D"` object contains parameters with the result of the 3D Secure process and can be forwarded to 3rd party payment gateways. If you decide to use Datatrans payment gateway please continue with our [Authorize](../advanced-features/payment-orchestration/authorize-settle.md) API.
