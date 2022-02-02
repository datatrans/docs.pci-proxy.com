# PUSH

### Process Flow

Push method allows you to receive already tokenized card data on a uniquePushKey endpoint. Channels can push requests to this unique PCI Proxy endpoint containing credit card data in its payload. Hence, it is routed via PCI Proxy, the payload is filtered for credit card data and automatically tokenized. All other headers and payloads will be kept and routed through PCI Proxy without modification.

![Push channel flow with PCI Proxy](<../../../.gitbook/assets/push channel.svg>)

{% swagger baseUrl="https://sandbox.pci-proxy.com" path="/v1/push/uniquePushKey" method="post" summary="PUSH method - API request" %}
{% swagger-description %}
The parameters marked with * are mandatory.
{% endswagger-description %}

{% swagger-parameter in="path" name="uniquePushKey" type="string" required="true" %}
Your 

`uniquePushKey`

 can be accessed on the Settings screen of the Integration you added in the dashboard.  
{% endswagger-parameter %}

{% swagger-response status="200" description="Request with tokenized card number and cvv code" %}

{% endswagger-response %}
{% endswagger %}



{% hint style="info" %}
The masked card number will be returned in the response as an HTTP header`pci-proxy-masked-aliases AAABcHxr-sDssdexyrAAAfyXWIgaAF40=424242xxxxxx4242`
{% endhint %}

{% hint style="warning" %}
In test mode, only [test credit cards](../../../resources/test-credentials.md) are allowed.
{% endhint %}

### Example

When you [**add a PUSH Integration** ](../../../resources/pci-proxy-dashboard/add-integrations.md)to your account, you receive an `{uniquePushKey}` for each integration that is set up. Together with our PCI Proxy PUSH service URL, it results in a `unique PCI Proxy Endpoint` that is specific to that integration. Now, redirect requests coming from a Channel with a single step:

1. **Change the endpoint at your partner from `Your API Endpoint` to the  `unique PCI Proxy Endpoint`**

{% hint style="info" %}
If needed, whitelist the [IP addresses](../../../resources/ip-whitelisting.md) of PCI Proxy at your partner.
{% endhint %}

{% hint style="success" %}
If a Channel sends a request to its `unique PCI Proxy Endpoint`, PCI Proxy recognizes this partner and connects it to your account. The request from the Channel will now automatically be filtered for sensitive data. Located sensitive data will be instantly stored in our vaults while we insert the tokenized data in the request and forward it to `Your API Endpoint`.
{% endhint %}
