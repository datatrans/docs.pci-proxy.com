---
description: Get full control and interact with your tokens stored in our vault
---

# Manage

{% hint style="danger" %}
Please note that the token management API is only working with the latest Alias 2.0 format.   
Reach out to your PCI Proxy contact if you are not sure which alias format you are using. 
{% endhint %}

{% hint style="info" %}
The service requires HTTP basic authentication. The required credentials can be found in our dashboard. Please refer to [API authentication data](../guides/pci-proxy-dashboard/api-authentication-data.md#basic-authentication) for more information. 
{% endhint %}

{% api-method method="post" host="https://api.sandbox.datatrans.com" path="/v1/aliases" %}
{% api-method-summary %}
CONVERT
{% endapi-method-summary %}

{% api-method-description %}
Convert a legacy \(numeric or masked format\) token to the most recent token format.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==
{% endapi-method-parameter %}

{% api-method-parameter name="Content-Type" type="string" required=true %}
application/json; charset=UTF-8
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="legacyAlias" type="string" required=true %}
Legacy token format \(numeric or masked\)
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Returns converted alias v2
{% endapi-method-response-example-description %}

```javascript
{
  "alias": "AAABdJdXVGPssdexyrAAAbuFU885AFAk"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Invalid request
{% endapi-method-response-example-description %}

```javascript
{
  "error": {
    "code": "INVALID_ALIAS"
  }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

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
```javascript
{
  "alias": "AAABdJdXVGPssdexyrAAAbuFU885AFAk"
}
```
{% endtab %}
{% endtabs %}

{% api-method method="delete" host="https://api.sandbox.datatrans.com" path="/v1/aliases/{alias}" %}
{% api-method-summary %}
DELETE
{% endapi-method-summary %}

{% api-method-description %}
Delete a token with immediate effect. The token will no longer be recognized if used later with any API call.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="alias" type="string" required=true %}
Alias which should be deleted
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==
{% endapi-method-parameter %}

{% api-method-parameter name="Content-Type" type="string" required=true %}
application/json; charset=UTF-8
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Alias successful deleted
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Invalid request
{% endapi-method-response-example-description %}

```javascript
{
  "error": {
    "code": "ALIAS_NOT_FOUND"
  }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

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

