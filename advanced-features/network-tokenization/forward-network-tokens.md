---
description: Forward Network Tokens to third party receivers
---

# Forward Network Tokens

As normal FPANs Network Tokens can be used to authorize a payment transaction at a payment service provider. Use the [Filter Proxy](../../use/forward-proxy/) to forward Network Tokens incl. cryptograms to the receiver of your choice. Thereby our solution is fully flexible and can convert the PCI Proxy token to either a Network Token or a FPAN. Depending on what your payment provider is able to consume (NT or FPAN) and how the format of the payload looks like you are sending to us, we can determine to which value we need to convert and forward the request to the target accordingly.&#x20;

In case a PCI Proxy token is converted to a Network Token we also make sure to request a new cryptogram at the schemes on the fly. Additionally we also create other required values and populate them directly into your request before forwarding to the receiver. Those values are for instance the expiry date, the ECI value of a Network Token or the token type.&#x20;

For Customer Initiated transaction it is required to create a cryptogram at the point the transaction is authorized. This and also their limited lifespan requires us to create the cryptogram each time at the time of the transaction to the payment provider.&#x20;

To sum up, simply submit us your request with the PCI Proxy token in the payload and we take care of the rest. To see the entire process in detail, we have added an example Network Token forward integration with the Datatrans Payment Gateway as receiver below.&#x20;

### Example flow with the forward proxy

1. Navigate to the Integrations menu in the dashboard and make sure the receiver you want to forward payment data is installed on your project.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2022-10-26 at 13.32.24.png" alt=""><figcaption></figcaption></figure>

2\. Additionally check if the installed integration is ready to accept both, Network Tokens and PANs.\
Open the setting of the integrations to review the payloads mentioned.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2022-10-28 at 10.20.15.png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
If there's no Network Token payload visible on the integration, please Request a new Integration with the button in the top right corner. Or alternatively reach out directly to our team and submit the required information.&#x20;
{% endhint %}

3\. In the next step, prepare your request according what the target is expecting and send it to the [Filter Proxy](../../use/forward-proxy/). Below is one curl example which converts from a PCI Proxy token to a Network Token and one which converts to PANs.

{% tabs %}
{% tab title="Converts to Network Token" %}
```json
curl -L -X POST 'https://sandbox.pci-proxy.com/v1/pull' \
-H 'X-CC-MERCHANT-ID: {PCI Proxy merchantId}' \
-H 'X-CC-URL: https://api.sandbox.datatrans.com/v1/transactions/authorize' \
-H 'pci-proxy-api-key: {PCI Proxy API Key}' \
-H 'Authorization: Basic {Datatrans merchantId}:{Datatrans password}' \
-H 'Content-Type: application/json' \
--data-raw '{
  "currency": "EUR",
  "amount": 1000,
  "refno": "test_nt",
  "card": {
    "type": "NETWORK_TOKEN",
    "token": "7LHXscqwAAEAAAGECbvb7UQKOtZpAL2C",
    "expiryMonth": "",
    "expiryYear": "",
    "tokenType": "",
    "cryptogram": "",
    "3D": {
        "eci": ""
        }
  }
}'
```
{% endtab %}

{% tab title="Converts to PAN" %}
```json
curl -L -X POST 'https://sandbox.pci-proxy.com/v1/pull' \
-H 'X-CC-MERCHANT-ID: {PCI Proxy merchantId}' \
-H 'X-CC-URL: https://api.sandbox.datatrans.com/v1/transactions/authorize' \
-H 'pci-proxy-api-key: {PCI Proxy API Key}' \
-H 'Authorization: Basic {Datatrans merchantId}:{Datatrans password}' \
-H 'Content-Type: application/json' \
--data-raw '{
  "currency": "EUR",
  "amount": 1000,
  "refno": "test_PAN",
  "card": {
    "number": "7LHXscqwAAEAAAGECbvb7UQKOtZpAL2C",
    "expiryMonth": "02",
    "expiryYear": "23"
    }
}'
```
{% endtab %}
{% endtabs %}

As you can see the payload structure is different depending if the target (Datatrans authorize endpoint in this case) consumes Network Tokens or PANs. For the Network Token example you only need to send us the PCI Proxy token and leave the other NT relevant fields empty in the payload, as we will take care of them. When `cryptogram` and `eci` values are requested, we write them plus the rest of the missing values such as `expiryMonth`, `expiryYear` and `tokenType` to the empty fields before forwarding it to the target url configured on the receiver.&#x20;

{% hint style="info" %}
While testing in sandbox we highly recommend to use the [Traffic Inspector](../../resources/pci-proxy-dashboard/traffic-inspector.md) feature to see what the PCI Proxy engine is converting to and what's being forwarded to the target endpoint. &#x20;
{% endhint %}



