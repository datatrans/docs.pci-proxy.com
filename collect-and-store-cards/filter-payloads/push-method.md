# PUSH Method

### Process flow

The push method allows you to receive already tokenized card data on a uniquePushKey endpoint. Your partners can push requests to this unique PCI Proxy endpoint containing credit card data in its payload. Hence, it is routed via PCI Proxy, the payload is filtered for credit card data and automatically tokenized. All the other headers, the payload and the HTTP method will be kept and routed through PCI Proxy without modification.

![Process Flow with PCI Proxy](<../../.gitbook/assets/channel\_push\_pciproxy\_color (4).png>)

{% swagger baseUrl="https://sandbox.pci-proxy.com" path="/v1/push/uniquePushKey" method="post" summary="PUSH method - API request" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="uniquePushKey" type="string" required="true" %}
Your 

`uniquePushKey `

can be accessed by clicking on the Settings of the Integration you added in the dashboard.
{% endswagger-parameter %}

{% swagger-response status="200" description="Request with tokenized card number and cvv code" %}
```javascript
```
{% endswagger-response %}
{% endswagger %}

The masked card number will be returned in the response as an HTTP header

`pci-proxy-masked-aliases AAABcHxr-sDssdexyrAAAfyXWIgaAF40=424242xxxxxx4242`

{% hint style="warning" %}
In test mode, only [test credit cards](../../test-card-data.md) are allowed.
{% endhint %}

### Example

When you [**add a PUSH Integration**](../../guides/pci-proxy-dashboard/add-integrations.md)** **to your account, you receive a `{uniquePushKey}` for each integration that is set up. Together with our PCI Proxy PUSH service URL, it results in a **unique PCI Proxy endpoint** that is specific to that integration. Redirect the requests coming from a Channel with a single step:

1. Change the endpoint at Channel from your API endpoint to the unique PCI Proxy endpoint

{% hint style="info" %}
If needed, whitelist the [IP addresses](../../resources/ip-whitelisting.md) of PCI Proxy at Channel.
{% endhint %}

{% hint style="success" %}
If the Channel sends a request to its **unique PCI Proxy endpoint**, PCI Proxy recognizes the Channel and connects it to your account. The request from Channel will now automatically be filtered for credit card data. Located card data will be instantly stored in our vaults while we insert the tokenized card data in the request and forward it to **your API endpoint**.
{% endhint %}
