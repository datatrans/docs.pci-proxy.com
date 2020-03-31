# PUSH Method

{% hint style="danger" %}
This service requires IP whitelisting of the requesting 3rd party. Please contact the PCI Proxy team to add the IPs to your account. 
{% endhint %}

{% api-method method="post" host="https://sandbox.pci-proxy.com" path="/v1/push/uniquePushKey" %}
{% api-method-summary %}
PUSH method
{% endapi-method-summary %}

{% api-method-description %}
`/v1/push` method allows you to receive a request via PCI Proxy on a `uniquePushKey` endpoint. Your partners can push requests to this unique PCI Proxy endpoint to ask for credit card data in the response. Hence, it is routed via PCI Proxy, your response payload is instantly filtered for tokens, all tokens will be detokenized and your response payload is populated with sensitive card data before it arrives at the Receiver. All other headers and payload will be kept and routed through PCI Proxy without modification.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="uniquePushKey" type="string" required=true %}
Your `uniquePushKey` can be accessed by clicking in the Settings of the Integration you added in the dashboard. 
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Response depends on your API. 
{% endapi-method-response-example-description %}

```javascript
<!-- your response - tokens will be detokenized and card data forwarded -->
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="warning" %}
In test mode, only [test credit cards](../../../test-card-data.md) are allowed.
{% endhint %}

### Process Flow

![Process Flow with PCI Proxy](../../../.gitbook/assets/receiver_push_pciproxy_color.png)

### Examples

When you [add a PUSH Receiver](../../../guides/pci-proxy-dashboard/add-integrations.md) to your account, you receive a `{uniquePushKey}` for each Receiver that is set up. Together with our PCI Proxy PUSH service URL, it results in a `unique PCI Proxy Endpoint` that is specific to that Receiver. Now, redirect requests coming from a Receiver with a single step:

1. **Change endpoint at Receiver from `Your API Endpoint` to `unique PCI Proxy Endpoint`**

{% hint style="info" %}
If needed, whitelist [IP addresses](../../../resources/ip-whitelisting.md) of PCI Proxy at Receiver.
{% endhint %}

{% hint style="success" %}
As the request is routed via PCI Proxy, the response payload is automatically filtered for tokens. Located tokens are detokenized and your response payload is populated with full card data before it arrives at the Receiver endpoint. Thereby, the Receiver API endpoint obtains full credit card data.
{% endhint %}

