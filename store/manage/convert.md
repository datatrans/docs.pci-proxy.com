---
description: Convert a legacy token (numeric or masked format) to an Alias 2.0 format.
---

# Convert

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/aliases" method="post" summary="CONVERT" %}
{% swagger-description %}
The parameters marked with * are mandatory.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="legacyAlias" type="string" required="true" %}
Legacy token format (numeric or masked)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiryMonth" type="string" %}
The expiry month of the credit card behind alias d{2}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiryYear" type="string" %}
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
```javascript
{
  "alias": "AAABdJdXVGPssdexyrAAAbuFU885AFAk"
}
```
{% endtab %}
{% endtabs %}

{% hint style="danger" %}
Please note that the CONVERT API is only working with the latest [Alias 2.0 format.](../../resources/token-formats.md#alias-2.0) \
Reach out to your PCI Proxy contact if you are not sure which alias format you are using.
{% endhint %}
