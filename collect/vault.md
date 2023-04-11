---
description: >-
  Server-to-Server API to create tokens or Network Tokens for PAN, CVV codes and
  custom values.
---

# Vault

The Vault API allows you to interact with the PCI Proxy tokenisation vault. Simply pass your data directly from your server to the Vault endpoint to replace them with tokens. The API supports single as well as bulk tokenisation for credit card numbers, cvv codes and custom values. The Vault API can also be used to create [Network Tokens](../advanced-features/network-tokenization/) directly from your server.&#x20;

Please consider the following constraints when using the Vault API:&#x20;

* For bulk tokenisation the maximum number of requests per batch is 100
* For custom values we do not apply any form of validation
* Please also consider the PCI DSS requirements below

{% hint style="warning" %}
Only PCI DSS compliant merchants are allowed to use the Vault API as it consumes plain text card data. Exemptions can be granted for a limited period of time if there is a valid business reason such as for instance initial card-to-token migrations or collection of non-sensitive data. \
\
For any sensitive data collected through client based apps, please use the [Secure Fields](secure-fields-js/) or the [Mobile SDKs](mobile-sdks.md) integration.&#x20;
{% endhint %}

## Implementation&#x20;

Learn below how to build the request. You can find as well an example request and response.&#x20;

#### Endpoints

{% tabs %}
{% tab title="Sandbox" %}
[https://api.sandbox.datatrans.com](https://api.sandbox.datatrans.com)
{% endtab %}

{% tab title="Production" %}
[https://api.datatrans.com](https://api.sandbox.datatrans.com)
{% endtab %}
{% endtabs %}

### 1. Request access

Due to increased security risk, the Vault API needs to be activated for your merchantId. Please get in touch with our team to activate it for you.&#x20;

### 2. Tokenisation Request

{% swagger method="post" path="/v1/aliases/tokenize" baseUrl="https://api.sandbox.datatrans.com" summary="Vault API" %}
{% swagger-description %}
Submit card number, cvv code or any custom data values to receive tokens in return.  
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="true" %}
Basic MTEwMDAwNzAwNjpLNnFYMXUkIQ==


{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" required="false" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="requests" type="Array" required="true" %}
Array of objects. List of tokenisation requests.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" required="true" %}
`CARD`, `CVV` or `CUSTOM`

**At least one parameter is required**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pan" %}
`[ 13 .. 19 ]`

 characters

\


Plain text card number
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiryMonth" %}
`= 2` characters&#x20;

The expiry month of the card
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiryYear" %}
`= 2` characters

The expiry year of the card.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cvv" %}
`[ 3 .. 4 ]` characters&#x20;

Plain text cvv code
{% endswagger-parameter %}

{% swagger-parameter in="body" name="custom" %}
`<= 100`

 characters 

\


Custom value of your choice
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Tokenization successful" %}
```json
{
    "overview": {
        "total": 3,
        "successful": 3,
        "failed": 0
    },
    "responses": [
        {
            "type": "CARD",
            "alias": "AGhFLt-mj0BfI3XN",
            "maskedCC": "424242xxxxxx4242",
            "fingerprint": "F-dV5V8dE0SZLoTurWbq2HZp"
        },
        {
            "type": "CVV",
            "alias": "Il2ob3L2QgqoxvkqCi0UcJw5",
            "expiryDate": "2024-06-02T09:52:08Z"
        },
        {
            "type": "CUSTOM",
            "alias": "3_FtAG15RdCcRb-gC8tBwg=="
        }
    ]
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid Request: Returns error object with an error code and an error message" %}
```javascript
{
  "error": {
    "code": Enum: "INVALID_PLAIN_VALUE" "INVALID_EXPIRATION" "CLIENT_ERROR" "INVALID_JSON_PAYLOAD" "ALIAS_NOT_FOUND" "INVALID_CVV" "UNKNOWN_ERROR" "UNRECOGNIZED_PROPERTY" "INVALID_ALIAS" "SERVER_ERROR" "ILLEGAL_ARGUMENT" "UNAUTHORIZED" "INVALID_PROPERTY" "MAX_REQUESTS_PER_CALL_EXCEEDED" "VELOCITY_ERROR",
    "message": "A human readable message indicating what went wrong."
  }
}
```
{% endswagger-response %}
{% endswagger %}

#### Example

{% tabs %}
{% tab title="Request" %}
```json
curl -L -X POST 'https://api.sandbox.datatrans.com/v1/aliases/tokenize' \
-H 'Authorization: Basic MTEwMDAxNzc4OTpNQUd6UUVEbkVxd001d0Vr' \
-H 'Content-Type: application/json' \
--data-raw '{
    "requests": [
        {
            "type": "CARD",
            "pan": "4242424242424242",
            "expiryMonth": "05",
            "expiryYear": "21"
        },
        {
            "type": "CVV",
            "cvv": "123"
        },
        {
            "type": "CUSTOM",
            "custom": "John Doe"
        }
    ]
}'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "overview": {
        "total": 3,
        "successful": 3,
        "failed": 0
    },
    "responses": [
        {
            "type": "CARD",
            "alias": "AGhFLt-mj0BfI3XN",
            "maskedCC": "424242xxxxxx4242",
            "fingerprint": "F-dV5V8dE0SZLoTurWbq2HZp"
        },
        {
            "type": "CVV",
            "alias": "Il2ob3L2QgqoxvkqCi0UcJw5",
            "expiryDate": "2024-06-02T09:52:08Z"
        },
        {
            "type": "CUSTOM",
            "alias": "3_FtAG15RdCcRb-gC8tBwg=="
        }
    ]
}
```
{% endtab %}
{% endtabs %}

This service requires HTTP basic authentication. The required credentials can be found in our dashboard. Please refer to [API authentication data](../resources/pci-proxy-dashboard/api-authentication-data.md#basic-authentication) for more information.

### **Network Tokens**

In case your merchantID is activated for Network Tokenisation, use the credit card alias returned by the Vault API and make an Alias status call to create a new Network Token. The Network Token will be mapped to the PCI Proxy alias.

**Alias Status API**

{% swagger method="get" path="/v1/aliases/{alias}" baseUrl="https://api.sandbox.datatrans.com" summary="Create a Network Token" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="true" %}
Basic MTEwMDAwNzAwNjpLNnFYMXUkIQ==


{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="Content-Type" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="path" name="alias" required="true" %}
PCI Proxy alias
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Status successfully returned" %}
```json
{
    "alias": "7LHXscqwAAEAAAGEFDW3rEmNoLVdAAZE",
    "fingerprint": "F-fgxnFwN-gsIw7y80T-kpBB",
    "type": "CARD",
    "masked": "489537xxxxxx6287",
    "dateCreated": "2022-10-26T12:13:00Z",
    "card": {
        "expiryMonth": "02",
        "expiryYear": "23",
        "cardInfo": {
            "brand": "VISA",
            "type": "debit",
            "usage": "consumer",
            "country": "US",
            "issuer": "U.S. REGION"
        },
        "tokenInfo": {
            "expiryMonth": "02",
            "expiryYear": "23"
        }
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid request" %}
```json
{
  "error": {
    "code": "ALIAS_NOT_FOUND"
  }
```
{% endswagger-response %}
{% endswagger %}

{% hint style="info" %}
Check the response and look if the `tokenInfo` object is available in the response. It tells you whether we have been able to create a Network Token or not.&#x20;
{% endhint %}

### Detokenisation

Please refer to the [reverse Vault API](../use/vault.md) if you need to convert sensitive data back to clear text values.&#x20;
