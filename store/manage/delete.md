---
description: Delete a token with immediate effect. The token will no longer be available.
---

# Delete

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/aliases/{alias}" method="delete" summary="DELETE" %}
{% swagger-description %}
The parameters marked with * are mandatory.
{% endswagger-description %}

{% swagger-parameter in="path" name="alias" type="string" required="true" %}
Alias which should be deleted
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
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

{% hint style="danger" %}
Please note that the DELETE API is only working with the latest [Alias 2.0 format](../../resources/token-formats.md#alias-2.0). \
Reach out to your PCI Proxy contact if you are not sure which alias format you are using.&#x20;
{% endhint %}
