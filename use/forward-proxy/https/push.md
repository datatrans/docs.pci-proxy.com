# PUSH

### Process flow

The Push method allows you to receive a request via PCI Proxy on a `uniquePushKey` endpoint. Your partners can push requests to this unique PCI Proxy endpoint to ask for credit card data in the response. Hence, it is routed via PCI Proxy, your response payload is instantly filtered for tokens, all tokens will be detokenized and your response payload is populated with sensitive card data before it arrives at the Receiver. All the other headers and the payload will be kept and routed through PCI Proxy without modification.

![](<../../../.gitbook/assets/push receiver.svg>)

{% hint style="danger" %}
This service requires IP whitelisting of the requesting 3rd party. Please contact the PCI Proxy team to add the IPs to your account.&#x20;
{% endhint %}

{% swagger baseUrl="https://sandbox.pci-proxy.com" path="/v1/push/uniquePushKey" method="post" summary="PUSH method - API request" %}
{% swagger-description %}
The parameters marked with * are mandatory.
{% endswagger-description %}

{% swagger-parameter in="path" name="uniquePushKey" type="string" required="true" %}
Your 

`uniquePushKey`

 can be accessed by checking the settings of the integration you added in the dashboard. 
{% endswagger-parameter %}

{% swagger-response status="200" description="Response depends on your API. " %}
```javascript
<!-- your response - tokens will be detokenized and card data forwarded -->
```
{% endswagger-response %}
{% endswagger %}

{% hint style="warning" %}
In test mode, only [test credit cards](broken-reference) are allowed.
{% endhint %}

### Example

When you [add a PUSH Receiver](../../../resources/pci-proxy-dashboard/add-integrations.md) to your account, you receive a `{uniquePushKey}` for each Receiver that is set up. Together with our PCI Proxy PUSH service URL, it results in a `unique PCI Proxy Endpoint` that is specific to that Receiver. Now, redirect the requests coming from a Receiver with a single step:

1. **Change the endpoint at your partner from `Your API Endpoint` to the `unique PCI Proxy Endpoint`**

{% hint style="success" %}
As the request is routed via PCI Proxy, the response payload is automatically filtered for tokens. Located tokens are detokenized and your response payload is populated with full card data before it arrives at the Receiver endpoint. Thereby, the Receiver API endpoint obtains full credit card data.
{% endhint %}
