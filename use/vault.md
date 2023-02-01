---
description: Server to Server API to detokonize data
---

# Vault

Use the reverse Vault API to convert sensitive data from a PCI Proxy token back to the clear text value. The API supports single as well as bulk detokenization for credit card number-, cvv- and custom value aliases.&#x20;

Please consider the following constraints when using the reverse Vault API:&#x20;

* For bulk detokenizations the maximum number of requests per batch is 100
* For custom values we do not apply any form of validation
* Please also consider the PCI DSS requirements below

{% hint style="warning" %}
Only PCI DSS compliant merchants are allowed to use the reverse Vault API as it returns sensitive plain text data which extends your PCI DSS scope. \
\
Exemptions can be granted for a limited period of time if there is a valid business reason such as for instance PSP migrations or in case of non-sensitive data. \
\
For any sensitive data to be revealed in client apps, please use the [Show API](show/) integration.&#x20;
{% endhint %}

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

Due to increased security risk, the reverse Vault API needs to be activated for your merchantId and IP whitelisting is required. Please get in touch with our team to configure it for you.&#x20;

### 2. Detokenization Request

{% swagger method="post" path="/v1/aliases/detokenize" baseUrl="https://api.sandbox.datatrans.com" summary="Vault API" %}
{% swagger-description %}
Submit card number-, cvv-, or any custom data aliases to receive plain text values in return.  
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

{% swagger-parameter in="body" name="alias" required="true" %}
An 

[alias (token)](../resources/token-formats.md)

 created with a previous PCI Proxy integration. 
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Detokenization successful" %}
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
            "pan": "5186151650011006"
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
curl -L -X POST 'https://api.sandbox.datatrans.com/v1/aliases/detokenize' \
-H 'Authorization: Basic MTEwMDAxNzc4OTpNQUd6UUVEbkVxd001d0Vr' \
-H 'Content-Type: application/json' \
--data-raw '{
    "requests": [
        {
            "type": "CARD",
            "alias": "7LHXscqwAAEAAAGELW8yPYx7lOreANmg"
        },
        {
            "type": "CVV",
            "alias": "LqFr-TLBQRC6lIkfogaSDbz3"
        },
        {
            "type": "CUSTOM",
            "alias": "DHoVO57dSKKK5EDH-ysnSw=="
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
            "pan": "5186151650011006"
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
}
```
{% endtab %}
{% endtabs %}

This service requires HTTP basic authentication. The required credentials can be found in our dashboard. Please refer to [API authentication data](../resources/pci-proxy-dashboard/api-authentication-data.md#basic-authentication) for more information.

{% hint style="info" %}
CVV aliases have a limited lifespan of 30 minutes and can't be detokenized anymore when expired.&#x20;
{% endhint %}

