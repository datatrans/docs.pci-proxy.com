# PUSH Method

### Process flow

Push method allows you to receive already tokenized card data on a uniquePushKey endpoint. Your partners can push requests to this unique PCI Proxy endpoint containing credit card data in its payload. Hence, it is routed via PCI Proxy, the payload is filtered for credit card data and automatically tokenized. All other headers and payload will be kept and routed through PCI Proxy without modification.



![Process Flow with PCI Proxy](<../../.gitbook/assets/channel_push_pciproxy_color (4).png>)

{% swagger baseUrl="https://sandbox.pci-proxy.com" path="/v1/push/uniquePushKey" method="post" summary="PUSH method - API request" %}
{% swagger-description %}
``
{% endswagger-description %}

{% swagger-parameter in="path" name="uniquePushKey" type="string" %}
Your 

`uniquePushKey`

 can be accessed by clicking on the Settings of the Integration you added in the dashboard.  
{% endswagger-parameter %}

{% swagger-response status="200" description="Request with tokenized card number and cvv code" %}
```javascript
```
{% endswagger-response %}
{% endswagger %}

{% hint style="info" %}
Masked cardnumber will be returned in the response as HTTP header`pci-proxy-masked-aliases AAABcHxr-sDssdexyrAAAfyXWIgaAF40=424242xxxxxx4242`
{% endhint %}

{% hint style="warning" %}
In test mode, only [test credit cards](../../test-card-data.md) are allowed.
{% endhint %}

### Example

When you [**add a PUSH Integration**](../../guides/pci-proxy-dashboard/add-integrations.md)** **to your account, you receive a `{uniquePushKey}` for each Channel that is set up. Together with our PCI Proxy PUSH service URL, it results in a `unique PCI Proxy Endpoint` that is specific to that Channel. Now, redirect requests coming from a Channel with a single step:

1. **Change endpoint at Channel from `Your API Endpoint` to `unique PCI Proxy Endpoint`**

{% hint style="info" %}
If needed, whitelist [IP addresses](../../resources/ip-whitelisting.md) of PCI Proxy at Channel.
{% endhint %}

{% hint style="success" %}
If Channel sends a request to its `unique PCI Proxy Endpoint`, PCI Proxy recognizes the Channel and connects it to your account. The request from Channel will now automatically be filtered for credit card data. Located card data will be instantly stored in our vaults while we insert the tokenized card data in the request and forward it to `Your API Endpoint`.
{% endhint %}
