---
description: Distribute stored payment data to any PCI-compliant API endpoint.
---

# HTTPS

## 1. Add Receiver

Before you can forward stored card data to a remote server you have to add the remote server as a Receiver to your account. You can either pick from our list of [supported Receivers](../../resources/supported-receivers.md) or add new ones:

| Click to [**Add Receivers**](https://admin.sandbox.datatrans.com/showcase/pci-proxy/add-receiver.html) |
| :--- |


## 2. Select forward method

PCI Proxy supports 2 forwarding methods [`/v1/pull/`](https.md#pull-method) and [`/v1/push/`](https.md#push-method) to suit all your needs.

Forwarding card data to a remote server via HTTPS can work in two ways. In general, either you perform a pull request to forward card data to the Receiver or a Receiver starts a push request to receive card data from you in the response. PCI Proxy can populate both operations with sensitive data.

| `/v1/pull/` | `/v1/push/` |
| --- | --- | --- |
| You start the request. | The Receiver starts the request. |
| ![](../../.gitbook/assets/receiver_pull_status_quo_color%20%281%29.png) | ![](../../.gitbook/assets/receiver_push_status_quo_color.png) |

{% api-method method="post" host="https://sandbox.pci-proxy.com" path="/v1/pull" %}
{% api-method-summary %}
PULL method
{% endapi-method-summary %}

{% api-method-description %}
`/v1/pull` method allows you to send a request via PCI Proxy to a Receiver API endpoint. When the request arrives at PCI Proxy, your payload is instantly filtered for tokens, all tokens will be detokenized and your payload is populated with sensitive card data before it arrives at the Receiver. Just add the following header params to your request and redirect your request to the `/v1/pull` endpoint. All other headers and your payload will be kept and routed through PCI Proxy without modification.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="X-CC-MERCHANT-ID" type="string" required=true %}
Your unique account id at PCI Proxy \(e.g. 1000011011\)
{% endapi-method-parameter %}

{% api-method-parameter name="X-CC-SIGN" type="string" required=true %}
Your security sign \(e.g. 30916165706580013\)
{% endapi-method-parameter %}

{% api-method-parameter name="X-CC-URL" type="string" required=true %}
API endpoint \(https://api.channel.com/\)
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="warning" %}
In test mode, only [test credit cards](https://docs.pci-proxy.com/setup/sandbox-account#test-card-numbers) are allowed.
{% endhint %}

### Process Flow

![Process Flow with PCI Proxy](../../.gitbook/assets/receiver_pull_pciproxy_color%20%281%29.png)

### Examples

Once a PULL Receiver is added to your merchantId, simply redirect requests to it via the PCI Proxy:

{% code-tabs %}
{% code-tabs-item title="Forward to Stripe" %}
```bash
curl https://sandbox.pci-proxy.com/v1/pull \
 -H 'X-CC-MERCHANT-ID: 1000011011' \
 -H 'X-CC-SIGN: 30916165706580013' \
 -H 'X-CC-URL: https://api.stripe.com/v1/tokens' \
 -u sk_test_BQokikJOvBiI2HlWgH4olfQ2: \
 -d 'card[number]=424242SKMPRI4242' \
 -d 'card[exp_month]=12' \
 -d 'card[exp_year]=2018'
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response" %}
```javascript
{
  "id": "tok_1CHoPL2eZvKYlo2Ck6KE483n",
  "object": "token",
  "card": {
    "id": "card_1CHoPL2eZvKYlo2CrbEHZ0G1",
    "object": "card",
    "address_city": null,
    "address_country": null,
    "address_line1": null,
    "address_line1_check": null,
    "address_line2": null,
    "address_state": null,
    "address_zip": null,
    "address_zip_check": null,
    "brand": "Visa",
    "country": "US",
    "cvc_check": null,
    "dynamic_last4": null,
    "exp_month": 12,
    "exp_year": 2018,
    "fingerprint": "Xt5EWLLDS7FJjR1c",
    "funding": "credit",
    "last4": "4242",
    "metadata": {},
    "name": null,
    "tokenization_method": null
  },
  "client_ip": "91.223.186.160",
  "created": 1523950759,
  "livemode": false,
  "type": "card",
  "used": false
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="success" %}
Your request is automatically filtered for tokens. Located tokens are detokenized and your payload is populated with full card data before it arrives at the Receiver endpoint. Thereby, the Receiver API endpoint obtains full credit card data.
{% endhint %}

{% api-method method="post" host="https://sandbox.pci-proxy.com" path="/v1/push:uniquePushKey" %}
{% api-method-summary %}
PUSH method
{% endapi-method-summary %}

{% api-method-description %}
`/v1/push` method allows you to receive a request via PCI Proxy on a `uniquePushKey` endpoint. Your partners can push requests to this unique PCI Proxy endpoint to ask for credit card data in the response. Hence, it is routed via PCI Proxy, your response payload is instantly filtered for tokens, all tokens will be detokenized and your response payload is populated with sensitive card data before it arrives at the Receiver. All other headers and payload will be kept and routed through PCI Proxy without modification.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="uniquePushKey" type="string" required=false %}
Your partner can simply push its request to the `uniquePushKey` endpoint.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="warning" %}
In test mode, only [test credit cards](https://docs.pci-proxy.com/setup/sandbox-account#test-card-numbers) are allowed.
{% endhint %}

### Process Flow



![Process Flow with PCI Proxy](../../.gitbook/assets/receiver_push_pciproxy_color.png)

### Examples

When you [add a PUSH Receiver](https.md#1.-add-receiver) to your account, you receive a `{uniquePushKey}` for each Receiver that is set up. Together with our PCI Proxy PUSH service URL, it results in a `PCI Proxy PUSH Endpoint` that is specific to that Receiver:

Redirect requests coming from a Receiver with a single step:

1. **Change API endpoint at Receiver from `Your API Endpoint` to `unique PCI Proxy Endpoint`.**

{% hint style="info" %}
If needed, whitelist [IP addresses](../../setup/ip-whitelisting.md) of PCI Proxy at Receiver.
{% endhint %}

{% hint style="success" %}
As the request is routed via PCI Proxy, the response payload is automatically filtered for tokens. Located tokens are detokenized and your response payload is populated with full card data before it arrives at the Receiver endpoint. Thereby, the Receiver API endpoint obtains full credit card data.
{% endhint %}

