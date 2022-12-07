---
description: >-
  Use the Tokenisation Link API to collect card details through a pre built
  Tokenisation page
---

# Tokenisation Link

Create a Tokenisation Link to securely collect sensitive card data using a pre built tokenisation page hosted by PCI Proxy. Simply send one API request and we take care of the rest.&#x20;

The link can be shared through various channels such as email, live chat, text messages, social media or even displayed as a QR code in your system. It allows you to customise the tokenisation page and comes with in built 3D Secure 2 logic to apply strong customer authentication when required. &#x20;

#### How it works

1. [Create a Tokenisation Link](./#1.-create-a-tokenisation-link)
2. [Share the Tokenisation Link and redirect the user](./#2.-redirect-card-holder)
3. [Check the status of a Tokenisation Link](./#3.-check-the-status-of-a-tokenisation-link)
4. [Delete a Tokenisation Link](./#4.-delete-a-tokenisation-link)
5. [Customise a Tokenisation Link](styling.md)

#### Endpoints

{% tabs %}
{% tab title="Sandbox" %}
[https://api.sandbox.link.pci-proxy.com](https://api.link.sandbox.pci-proxy.com)
{% endtab %}

{% tab title="Production" %}
[https://api.link.pci-proxy.com](https://api.link.sandbox.pci-proxy.com)
{% endtab %}
{% endtabs %}

## 1. Create a Tokenisation Link

Create a new Tokenisation Link by calling the following endpoint from your server.&#x20;

{% hint style="warning" %}
To process 3D authentications, submitting `amount`, `currency` and at least one of the card brand object (`VIS`, `ECA`, `AMX`) is required.&#x20;

Please also ensure your account is activated and configured for 3D authentications.
{% endhint %}

{% swagger method="post" path="/v1/links" baseUrl="https://api.link.sandbox.pci-proxy.com" summary="Create tokenisation link" %}
{% swagger-description %}
Create a new tokenisation link and optionally submit 3D acquiring data. 
{% endswagger-description %}

{% swagger-parameter in="header" name="pci-proxy-api-key" required="true" %}
Your PCI Proxy 

[API Key](../../resources/pci-proxy-dashboard/api-authentication-data.md)


{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="reference" required="true" %}
Unique reference number to identify your request. [ 1 .. 100 ] characters
{% endswagger-parameter %}

{% swagger-parameter in="body" name="successUrl" %}
URL where the user will be redirected if the tokenisation was successful. If omitted a pre built success page is displayed. 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="webhookEndpoint" %}
Webhook URL which will be called if the tokenisation was successful. 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="context" type="object" %}
Use this object to submit up to 6 additional parameters. They will be displayed on the Tokenisation page. 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="integer" %}
Transaction amount in the currency's smallest unit. For example use 1000 for EUR 10.00
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" %}
3 letter ISO-4217 character. For example 

`EUR`

 or 

`USD`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="VIS" type="object" %}
Object to submit Visa 3D acquiring data
{% endswagger-parameter %}

{% swagger-parameter in="body" name="ECA" type="object" %}
Object to submit Mastercard 3D acquiring data
{% endswagger-parameter %}

{% swagger-parameter in="body" name="AMX" type="object" %}
Object to submit Amex 3D acquiring data
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="A new Tokenisation Link has been created " %}
```javascript
{
    "id": "5383CA1B-9542-4584-A989-2002AB212510",
    "link": "https://link.sandbox.pci-proxy.com/77AC96tGxyKz3YjxUNypHF"
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Something went wrong" %}
```javascript
{
    "status": 400,
    "errors": [
        // check errors array for error description
    ]
}
```
{% endswagger-response %}
{% endswagger %}

#### Example

{% tabs %}
{% tab title="Request" %}
```javascript
curl --location --request POST 'https://api.link.sandbox.pci-proxy.com/v1/links'
--header 'pci-proxy-api-key: {API Key}' \
--header 'content-type: application/json' \
--data-raw '{
    "reference": "234923490",
    "successUrl": "https://example.org/success",
    "webhookEndpoint": "https://example.org/webhook",
    "context": {
        "Test Card": "true",
        "First Name": "Jon",
        "Last Name": "Doe"
    }
}'
```
{% endtab %}

{% tab title="Response" %}
```javascript
{
    "id": "C7A177DF-E9BA-482B-9CC1-047A2DFC9F19",
    "link": "https://link.sandbox.pci-proxy.com/C7A177DF-E9BA-482B-9CC1-047A2DFC9F19"
}
```
{% endtab %}

{% tab title="Request w/3D" %}
```javascript
curl --location --request POST 'https://api.link.sandbox.pci-proxy.com/v1/links'
--header 'Content-Type: application/json' \
--header 'pci-proxy-api-key: {API Key}' \
--data-raw '{
    "reference": "234923490",
    "successUrl": "https://example.org/success",
    "webhookEndpoint": "https://example.com/webhook",
    "context": {
        "Test Card": "true",
        "First Name": "Jon",
        "Last Name": "Doe"
    },
    "amount": 1000,
    "currency": "EUR",
    "VIS": {
        "3D": {
            "acquirer": {
                "acquirerBin": "33333333",
                "acquirerMerchantId": "33333333"
            },
            "merchant": {
                "mcc": "4722",
                "merchantName": "Example Travel Ltd."
            }
        }
    },
    "ECA": {
        "3D": {
            "acquirer": {
                "acquirerBin": "22222222",
                "acquirerMerchantId": "22222222"
            },
            "merchant": {
                "mcc": "4722",
                "merchantName": "Example Travel Ltd."
            }
        }
    },
    "AMX": {
        "3D": {
            "acquirer": {
                "acquirerBin": "1111111",
                "acquirerMerchantId": "1111111"
            },
            "merchant": {
                "mcc": "4722",
                "merchantName": "Example Travel Ltd."
            }
        }
    }
}'
```
{% endtab %}

{% tab title="Response w/3D" %}
```javascript
{
    "id": "2BA76D13-20C1-4CDB-9753-21C084C96C2F",
    "link": "https://link.sandbox.pci-proxy.com/2BA76D13-20C1-4CDB-9753-21C084C96C2F"
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
A Tokenisation Link can only be consumed once. However, it doesn't expire when not used.&#x20;
{% endhint %}

## 2. Redirect user

Share the `link` URL received in the response from `/v1/links` with your user. It redirects to a Tokenisation page hosted by PCI Proxy where the card details can be entered.&#x20;

{% hint style="info" %}
The styling of the hosted Tokenisation page can be adjusted to your look and feel. See the [styling guides](styling.md) for more details.&#x20;
{% endhint %}

If your merchantId is enabled for processing 3D-Secure and acquiring data were submitted in the initial request, 3D Secure gets automatically triggered in the background. In case a challenge is required by the issuing bank, the user will be redirected to the ACS URL of the issuing bank to complete the challenge.&#x20;

After completing the credit card fields and submitting the request, a pre built confirmation page hosted by PCI Proxy will be displayed to the user with a hint that the process is finished and the window can be closed. In case a `successUrl` has been submitted in the initial request, the user will be redirected to it automatically with a 5 second delay.&#x20;

As a next step, call the [Status API](./#3.-check-the-status-of-a-tokenisation-link) to retrieve tokenised card data, 3D authentication information and other card meta data.&#x20;

{% hint style="info" %}
If a `webhookEndpoint` URL has been submitted in the initial call, a notification will be sent to it after a successful tokenisation took place.&#x20;
{% endhint %}

## 3. Check the Status of a Tokenisation Link

To obtain tokenised card data, 3D authentication values or to simply keep track and check the latest state of a Tokenisation Link call the status API anytime.&#x20;

A Tokenisation Link can have the following status:&#x20;

| Status    | Description                                                                                                                                 |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `PENDING` | A Tokenisation Link has been created but not yet completed by a user.                                                                       |
| `SUCCESS` | Credit card data successfully received and tokenised. Card, CVV tokens, 3D authentication data and additional card meta data are returned.  |
| `ERROR`   | Something unexpected happened.                                                                                                              |

{% swagger method="get" path="/v1/links/{id}" baseUrl="https://api.link.sandbox.pci-proxy.com" summary="Status endpoint" %}
{% swagger-description %}
Check the status of a Link tokenization
{% endswagger-description %}

{% swagger-parameter in="header" required="true" name="pci-proxy-api-key" %}
Your PCI Proxy 

[API Key](../../resources/pci-proxy-dashboard/api-authentication-data.md)


{% endswagger-parameter %}

{% swagger-parameter in="path" required="true" name="id" %}
Tokenisation Link 

`id`

 returned in the response of 

`/v1/links`

   
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Status successfully returned" %}
```javascript
{
    "status": "SUCCESS",
    "reference": "1362a010-3aa7-4aff-b556-de217705991c",
    "link": "'https://link.sandbox.pci-proxy.com/77AC96tGxyKz3YjxUNypHF'",
    "paymentMethod": "VIS",
    "card": {
        "alias": "7LHXscqwAAEAAAGE4x0wQt24fppOAJeH",
        "fingerprint": "F-dV5V8dE0SZLoTurWbq2HZp",
        "masked": "424242xxxxxx4242",
        "aliasCVV": "v1QMX4gXQAWzvvw3tWyU4D4f",
        "expiryMonth": "06",
        "expiryYear": "25",
        "info": {
            "brand": "VISA CREDIT",
            "type": "credit",
            "usage": "consumer",
            "country": "GB",
            "issuer": "DATATRANS"
        }
    },
    "history": []
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Something went wrong" %}
```java
{
    "status": 400,
    "errors": [
        // check errors array for error description
    ]
}
```
{% endswagger-response %}
{% endswagger %}

#### Example (success case)

{% tabs %}
{% tab title="Request" %}
```javascript
curl --location --request GET 'https://api.link.sandbox.pci-proxy.com/v1/links/{id}'
--header 'Content-Type: application/json'
--header 'pci-proxy-api-key: {API Key}'
```
{% endtab %}

{% tab title="Response" %}
```javascript
{
    "status": "SUCCESS",
    "reference": "1362a010-3aa7-4aff-b556-de217705991c",
    "link": "https://link.sandbox.pci-proxy.com/77AC96tGxyKz3YjxUNypHF",
    "paymentMethod": "VIS",
    "card": {
        "alias": "7LHXscqwAAEAAAGE4x0wQt24fppOAJeH",
        "fingerprint": "F-dV5V8dE0SZLoTurWbq2HZp",
        "masked": "424242xxxxxx4242",
        "aliasCVV": "v1QMX4gXQAWzvvw3tWyU4D4f",
        "expiryMonth": "06",
        "expiryYear": "25",
        "info": {
            "brand": "VISA CREDIT",
            "type": "credit",
            "usage": "consumer",
            "country": "GB",
            "issuer": "DATATRANS"
        }
    },
    "history": []
}
```
{% endtab %}

{% tab title="Response w/3D" %}
{% code overflow="wrap" %}
```javascript
{
  "status": "SUCCESS",
  "reference": "234923490",
  "paymentMethod": "VIS",
  "card": {
    "alias": "7LHXscqwAAEAAAGC-UIBqxCY1SodANWt",
    "fingerprint": "F-fj8CDwhx2OS2MEL8WK_W7e",
    "masked": "400000xxxxxx0026",
    "aliasCVV": "7VJu5IQjROiW8MSmwYTFzYxU",
    "expiryMonth": "12",
    "expiryYear": "26",
    "info": {
      "brand": "VISA",
      "type": "credit",
      "usage": "consumer",
      "country": "US",
      "issuer": "DATATRANS"
    },
    "3D": {
      "eci": "05",
      "xid": "0e0b4423-c8ec-4851-b239-f7858222a177",
      "threeDSTransactionId": "a9e4b589-ad94-41f0-a339-9de18da9aedd",
      "cavv": "MAAAAAAAAAAAAAAAAAAAAAAAAAA=",
      "threeDSVersion": "2.2.0",
      "directoryResponse": "C",
      "authenticationResponse": "Y",
      "transStatusReason": "15"
    }
  },
  "history": [
    {
      "action": "authenticate",
      "amount": 1000,
      "source": "secure_fields",
      "date": "2022-09-01T13:33:55Z",
      "success": true,
      "ip": "21.101.125.184"
    }
  ],
  "currency": "EUR",
  "detail": {
    "authorize": {
      "amount": 1000
    }
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## 4. Delete a Tokenisation Link

Delete a Tokenisation Link. It can not be reactivated anymore.&#x20;

{% swagger method="delete" path="/v1/links/{id}" baseUrl="https://api.link.sandbox.pci-proxy.com" summary="Delete endpoint" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" required="true" name="id" %}
Tokenisation Link 

`id`

 returned in the response of 

`/v1/links`
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="pci-proxy-api-key" %}
Your PCI Proxy 

[API Key](../../resources/pci-proxy-dashboard/api-authentication-data.md)


{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Tokenisation Link successfully deleted" %}
```javascript
{
    "state": "DELETED"
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Tokenisation Link already deleted" %}
```javascript
{
    "status": 404,
    "message": "Not found"
}
```
{% endswagger-response %}
{% endswagger %}

#### Example

{% tabs %}
{% tab title="Request" %}
```javascript
curl --location --request DELETE 'https://api.link.sandbox.pci-proxy.com/v1/links/C7A177DF-E9BA-482B-9CC1-047A2DFC9F19' \
--header 'pci-proxy-api-key: {API Key}' \
--header 'Content-Type: application/json'
```
{% endtab %}

{% tab title="Response" %}
```javascript
{
    "state": "DELETED"
}
```
{% endtab %}
{% endtabs %}

### Postman collection

Download our Postman collection to play around with the Link APIs here: &#x20;

[https://www.getpostman.com/collections/451552a774f1fc4cb884](https://www.getpostman.com/collections/451552a774f1fc4cb884)
