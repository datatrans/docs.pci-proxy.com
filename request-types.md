# Process Understanding

# **Channel types**

The integration of PCI Proxy for Web Service depends on the channel type. In general, you either perform a pull request to receive data or a channel pushes data to your server. PCI Proxy can extract sensitive data from both.

| PULL Channel | PUSH Channel |
| :--- | :--- |
| ![](/assets/channel_pull_status_quo_color.png) | ![](/assets/channel_push_status_quo_color.png) |
| Whenever _you start the request_ and _receive card data in the response_ \(channel provides API\), we talk about a PULL channel type. | Whenever the _channel starts the request_ and _sends card data in the request _\(you provide API\), we talk about a PUSH channel type. |

Please see a list of supported channels and their respective channel type: [Supported Channels](/supported_channels.md).

**Add channel**

Please send us a quick email with all [supported channels](/supported_channels.md) you would like to add to your account to [setup@pci-proxy.com](/mailto:setup@pci-proxy.com). In case, you would like to add a channel that is currently not supported, please send the following information to [setup@pci-proxy.com](mailto:):

| Information | Description |
| --- | --- |
| Merchant ID | Your merchant ID |
| Channel Type | Define if it is a push or pull channel. |
| API endpoint | The URL where we should forward the request to. |
| Sample Request & Response | Please include API name, required headers, auth fields, and request method. |

You receive a confirmation once the channel is successfully added. For push channels, you also receive `{UNIQUE-CHANNEL-KEY}`.

#### 

| PULL Process Flow with PCI Proxy |
| :--- |
| ![](/assets/channel_pull_pciproxy_color.png) |
| 1. Simply redirect your channel request to PCI Proxy PULL endpoint and add 3 HTTP headers. |
| 2. PCI Proxy forwards your request directly to the URL in the HTTP header you just added. |
| 3. Channel sends response message to PCI Proxy. |
| 4. PCI Proxy scans response message for sensitive card data and tokenizes located card data. |
| 5. PCI Proxy forwards response message with tokenized credit card data to you. |

ghhfgfhg

---

# **Understand Receiver types**

Forwarding card data to a Receiver via web service can work in two ways. In general, you either perform a pull request to forward card data to a Receiver or a Receiver starts the request to ask for card data. PCI Proxy can populate sensitive data in both.

| PULL Channel | PUSH Channel |
| :--- | :--- |
| ![](/assets/channel_pull_status_quo_color.png) | ![](/assets/channel_push_status_quo_color.png) |
| Whenever _you start the request_ and _send card data in the request_ \(Receiver provides API\), we talk about a PULL Receiver type. | Whenever the_ Receiver starts a request_ and _you forward card data in the response _\(you provide API\), we talk about a PUSH channel type. |

Please see a list of supported channels and their respective channel type:[ Supported Receivers \(Gateways\)](/supported_receivers.md).

