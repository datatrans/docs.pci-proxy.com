# PUSH method

{% api-method method="post" host="https://sandbox.pci-proxy.com" path="/v1/push/uniquePushKey" %}
{% api-method-summary %}
PUSH method
{% endapi-method-summary %}

{% api-method-description %}
`/v1/push` method allows you to receive already tokenized card data on a `uniquePushKey` endpoint. Your partners can push requests to this unique PCI Proxy endpoint containing credit card data in its payload. Hence, it is routed via PCI Proxy, the payload is filtered for credit card data and automatically tokenized. All other headers and payload will be kept and routed through PCI Proxy without modification.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="uniquePushKey" type="string" required=false %}
Your `uniquePushKey` can be accessed by clicking on the Settings of the Integration you added in the dashboard.  
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="warning" %}
In test mode, only [test credit cards](../../test-card-data.md) are allowed.
{% endhint %}

### Process Flow

![Process Flow with PCI Proxy](../../.gitbook/assets/channel_push_pciproxy_color%20%283%29.png)

### Examples

When you [**add a PUSH Integration**](../../pci-proxy-dashboard/add-integrations.md) ****to your account, you receive a `{uniquePushKey}` for each Channel that is set up. Together with our PCI Proxy PUSH service URL, it results in a `unique PCI Proxy Endpoint` that is specific to that Channel. Now, redirect requests coming from a Channel with a single step:

1. **Change endpoint at Channel from `Your API Endpoint` to `unique PCI Proxy Endpoint`**

{% hint style="info" %}
If needed, whitelist [IP addresses](../../resources/ip-whitelisting.md) of PCI Proxy at Channel.
{% endhint %}

{% hint style="success" %}
If Channel sends a request to its `unique PCI Proxy Endpoint`, PCI Proxy recognizes the Channel and connects it to your account. The request from Channel will now automatically be filtered for credit card data. Located card data will be instantly stored in our vaults while we insert the tokenized card data in the request and forward it to `Your API Endpoint`.
{% endhint %}

