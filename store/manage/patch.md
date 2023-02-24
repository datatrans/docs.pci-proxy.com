---
description: Update an existing alias
---

# Patch

Use the Alias Patch endpoint to update an existing alias. It allows you to either update and map the expiry date (expiry year and month) of a card to it or remove the underlying PAN of an alias form your vault.&#x20;

Adding the expiry date is useful when the expiry date is not already submitted in the initial alias creation request. Such as for instance when using the Filter or SFTP proxy. An alias with a mapped expiry date is required when you plan to create a Network Token after the initial PCI Proxy tokenisation.&#x20;

Removing a PAN from storage is helpful if you need to comply with certain regulations which doesn't allow anyone in the payment eco system to store plain text card numbers anymore.&#x20;

{% hint style="info" %}
Please consider, that removing a PAN only works when your account is enabled for [Network Tokenisation](../../advanced-features/network-tokenization/) and we have been able to provision a Network Token for a given card number. A removed PAN can not be restored.&#x20;
{% endhint %}

{% hint style="danger" %}
The Alias Patch API is only working with the two latest [Alias 2.0 format](../../resources/token-formats.md#alias-2.0).&#x20;
{% endhint %}

#### Endpoints

{% tabs %}
{% tab title="Sandbox" %}
[https://api.sandbox.datatrans.com](https://api.sandbox.datatrans.com)
{% endtab %}

{% tab title="Production" %}
[https://api.datatrans.com](https://api.sandbox.datatrans.com)
{% endtab %}
{% endtabs %}

### Alias Patch request

{% swagger method="patch" path="/v1/aliases/{alias}" baseUrl="https://api.sandbox.datatrans.com" summary="PATCH alias" %}
{% swagger-description %}
Update an existing alias with the expiry year and month of the card or remove the raw underlying PAN. 
{% endswagger-description %}

{% swagger-parameter in="header" required="true" name="authorization" type="string" %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" required="true" type="string" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="path" name="alias" required="true" type="string" %}
Alias 2.0 format received from a previous inbound channel
{% endswagger-parameter %}

{% swagger-parameter in="body" type="string" name="expiryMonth" required="false" %}
`= 2`

 characters 

\


The expiry month of the card
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiryYear" required="false" type="string" %}
`= 2`

 characters 

\


The expiry year of the card
{% endswagger-parameter %}

{% swagger-parameter in="body" name="removePlain" type="string" %}
Remove the raw PAN from storage
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Update successful" %}

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

#### Examples

{% tabs %}
{% tab title="Request (expiry date)" %}
```javascript
curl -L -X PATCH 'https://api.sandbox.datatrans.com/v1/aliases/7LHXscqwAAEAAAGFDIr3SD05RBVAAK5n' \
-H 'Content-Type: application/json; charset=UTF-8' \
-H 'Authorization: {merchantId}:{password}' \
--data-raw '{   
    "expiryMonth": "02",    
    "expiryYear": "23"   
}'
```
{% endtab %}

{% tab title="Response" %}
```javascript
{
    "alias": "7LHXscqwAAEAAAGFDIr3SD05RBVAAK5n",
    "fingerprint": "F-dYOqJEhLBUD5Qs6i-_uJOr",
    "type": "CARD",
    "masked": "420034xxxxxx0015",
    "dateCreated": "2022-12-13T17:31:52Z",
    "card": {
        "expiryMonth": "02",
        "expiryYear": "23",
        "cardInfo": {
            "brand": "VISA",
            "type": "credit",
            "usage": "consumer",
            "country": "DE",
            "issuer": "VISA U.S.A. INC."
        },
        "tokenInfo": {
            "expiryMonth": "12",
            "expiryYear": "22"
        }
    }
}
```
{% endtab %}

{% tab title="Request (remove PAN)" %}
```javascript
curl -L -X PATCH 'https://api.sandbox.datatrans.com/v1/aliases/7LHXscqwAAEAAAGFDDm7on4gPrwPAMrW' \
-H 'Content-Type: application/json; charset=UTF-8' \
-H 'Authorization: {merchantId}:{password}' \
--data-raw '{
    "removePlain": true
}'
```
{% endtab %}

{% tab title="Response" %}
```java
{
    "alias": "7LHXscqwAAEAAAGFgnDhB3yHmsrQACZy",
    "fingerprint": "F-dYOqJEhLBUD5Qs6i-_uJOr",
    "type": "CARD",
    "masked": "420034xxxxxx0015",
    "dateCreated": "2022-12-13T17:31:52Z",
    "card": {
        "panRemoved": true,
        "expiryMonth": "02",
        "expiryYear": "23",
        "cardInfo": {
            "brand": "VISA",
            "type": "credit",
            "usage": "consumer",
            "country": "DE",
            "issuer": "VISA U.S.A. INC."
        },
        "tokenInfo": {
            "expiryMonth": "12",
            "expiryYear": "22"
        }
    }
}
```
{% endtab %}
{% endtabs %}

#### PATCH expiry date

{% hint style="info" %}
The response object `tokenInfo` indicates if a Network Token has been created. A missing `tokenInfo` object means the Network Token creation failed.&#x20;
{% endhint %}

#### PATCH removePlain&#x20;

{% hint style="info" %}
The response parameter `panRemoved` indicates if the PAN has been removed from storage for a given alias. \
\
You can also call the [Alias status API](status.md) if you are not sure whether the PAN is still existing or not.&#x20;
{% endhint %}
