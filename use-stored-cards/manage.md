---
description: Get full control and interact with your tokens (alias) stored in our vault
---

# Manage

{% hint style="danger" %}
Please note that the token management API is only working with the latest [Alias 2.0 format](https://docs.pci-proxy.com/resources/token-format).\
Reach out to your PCI Proxy contact if you are not sure which alias format you are using.
{% endhint %}

{% hint style="info" %}
The service requires HTTP basic authentication. The required credentials can be found in our dashboard. Please refer to [API authentication data](../guides/pci-proxy-dashboard/api-authentication-data.md#basic-authentication) for more information.
{% endhint %}

### Alias information

Request detailed information about an alias such as creation date or cardInfo.

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/aliases/{alias}" method="get" summary="Alias information" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="alias" type="string" required="false" %}
Alias 2.0 format received from a previous inbound channel
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" required="false" %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="false" %}
application/json; charset=UTF-8==
{% endswagger-parameter %}

{% swagger-response status="200" description="Status successfully returned" %}
```javascript
{
    "alias": "AAABeM8amw3ssdexyrAAAYwp9fXrAIkp",
    "fingerprint": "F-dV5V8dE0SZLoTurWbq2HZp",
    "type": "CARD",
    "masked": "424242xxxxxx4242",
    "dateCreated": "2021-01-14T06:38:50.637+00:00",
    "card": {
        "expiryMonth": "12",
        "expiryYear": "21",
        "cardInfo": {
            "brand": "VISA CREDIT",
            "type": "credit",
            "usage": "consumer",
            "country": "GB",
            "issuer": "DATATRANS"
        }
    }
}
```
{% endswagger-response %}

{% swagger-response status="400" description="Invalid request" %}
```javascript
{
  "error": {
    "code": "ALIAS_NOT_FOUND"
  }
}
```
{% endswagger-response %}
{% endswagger %}

#### Examples

{% tabs %}
{% tab title="Request" %}
```javascript
curl -L -X GET 'https://api.sandbox.datatrans.com/v1/aliases/AAABeM8amw3ssdexyrAAAYwp9fXrAIkp' \
-H 'Authorization: Basic MTEwMDAxNzc4OTpNQUd6UUVEbkVxd001d0Vr'
```
{% endtab %}

{% tab title="Response" %}
```javascript
{
    "alias": "AAABeM8amw3ssdexyrAAAYwp9fXrAIkp",
    "fingerprint": "F-dV5V8dE0SZLoTurWbq2HZp",
    "type": "CARD",
    "masked": "424242xxxxxx4242",
    "dateCreated": "2021-01-14T06:38:50.637+00:00",
    "card": {
        "expiryMonth": "12",
        "expiryYear": "21",
        "cardInfo": {
            "brand": "VISA CREDIT",
            "type": "credit",
            "usage": "consumer",
            "country": "GB",
            "issuer": "DATATRANS"
        }
    }
}
```
{% endtab %}
{% endtabs %}

### Convert

Convert a legacy (numeric or masked format) token to the most recent token format.

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/aliases" method="post" summary="Convert" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" required="false" %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="false" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="legacyAlias" type="string" required="false" %}
Legacy token format (numeric or masked)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiryMonth" type="string" required="false" %}
The expiry month of the credit card behind alias d{2}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiryYear" type="string" required="false" %}
The expiry year of the credit card behind the alias d{2}
{% endswagger-parameter %}

{% swagger-response status="200" description="Returns converted alias v2" %}
```javascript
{
  "alias": "AAABdJdXVGPssdexyrAAAbuFU885AFAk"
}
```
{% endswagger-response %}

{% swagger-response status="400" description="Invalid request" %}
```javascript
{
  "error": {
    "code": "INVALID_ALIAS"
  }
}
```
{% endswagger-response %}
{% endswagger %}

#### Examples

{% tabs %}
{% tab title="Request" %}
```javascript
curl -i -X POST https://api.sandbox.datatrans.com/v1/aliases \
	--user {merchantId}:{password} \
	-H 'Content-Type: application/json; charset=UTF-8' \
	-d '{
    "legacyAlias": "424242SKMPRI4242"
}'
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "alias": "AAABdJdXVGPssdexyrAAAbuFU885AFAk"
}
```
{% endtab %}
{% endtabs %}

### Delete

Delete a token with immediate effect. The token will no longer be recognized if used later with any API call.

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/aliases/{alias}" method="delete" summary="Delete" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="alias" type="string" required="false" %}
Alias which should be deleted
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" required="false" %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="false" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-response status="204" description="Alias successful deleted" %}
```
```
{% endswagger-response %}

{% swagger-response status="400" description="Invalid request" %}
```javascript
{
  "error": {
    "code": "ALIAS_NOT_FOUND"
  }
}
```
{% endswagger-response %}
{% endswagger %}

#### Examples

{% tabs %}
{% tab title="Request" %}
```javascript
curl -i -X DELETE https://api.sandbox.datatrans.com/v1/aliases/AAABdJdXjl7ssdexyrAAAZleH7dSANH- \
	--user {merchantId}:{password} \
```
{% endtab %}

{% tab title="Response" %}
```
204: No Content
```
{% endtab %}
{% endtabs %}
