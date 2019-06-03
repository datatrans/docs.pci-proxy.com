---
description: Authorize transactions which area alrady authenticated.
---

# Authorize

If you processed authentication only through either [Secure Fields](securefields-1/) or [3D API](api-beta.md), this API can be used to trigger authorization with only one parameter. 

{% hint style="info" %}
* This service requires basic authentication. The password can be found in the [Web Admin Tool](https://admin.sandbox.datatrans.com/) under _UPP Administration &gt; Security &gt; Server-to-Server services security_.
* Make sure to use our 3D Secure enabled test credit cards [here](../testing-3d-secure.md).
{% endhint %}

{% api-method method="post" host="https://api.sandbox.datatrans.com" path="/v1/transactions/{transactionId}/authorize" %}
{% api-method-summary %}
Authorize
{% endapi-method-summary %}

{% api-method-description %}
Authorize transactions which are alrady authenticated.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="transactionId" type="integer" required=true %}
The `transactionId` received after authentication was done
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

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
{% api-method-parameter name="amount" type="integer" required=false %}
Transaction amoun in the currency's smallest unit. For example use 1000 for EUR 10.00
{% endapi-method-parameter %}

{% api-method-parameter name="refno" type="integer" required=false %}
\[1..20\] characters  
The merchants reference number. It should be unique for each transaction.  
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Transaction successfully authorized
{% endapi-method-response-example-description %}

```javascript

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Examples

{% code-tabs %}
{% code-tabs-item title="Request" %}
```javascript
curl -X POST \
  https://api.sandbox.datatrans.com/v1/transactions/190603132621129101/authorize \
  -H 'Authorization: Basic MTEwMDAxNzY3NTpTejdodE5uSjdNM05YQ0lT' \
  -H 'Content-Type: application/json; charset=UTF-8' \
  -d '{
    "amount": 1000,
    "refno": "QzWbpYK5M"
}'
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response" %}
```javascript
{
    "acquirerAuthorizationCode": "132653"
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

