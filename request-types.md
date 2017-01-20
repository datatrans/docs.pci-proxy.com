# **Understand Channel types**

The integration of PCI Proxy for Web Service depends on the channel type. In general, you either perform a pull request to receive data or a channel pushes data to your server. PCI Proxy can extract sensitive data from both.

| PULL Channel | PUSH Channel |
| :--- | :--- |
| ![](/assets/channel_pull_status_quo_color.png) | ![](/assets/channel_push_status_quo_color.png) |
| Whenever _you start the request_ and _receive card data in the response_ \(channel provides API\), we talk about a PULL channel type. | Whenever the _channel starts the request_ and _sends card data in the request _\(you provide API\), we talk about a PUSH channel type. |

Please see a list of supported channels and their respective channel type: [Supported Channels](/supported_channels.md).

---

# **Understand Receiver types**

Forwarding card data to a Receiver via web service can work in two ways. In general, you either perform a pull request to forward card data to a Receiver or a Receiver starts the request to ask for card data. PCI Proxy can populate sensitive data in both.

| PULL Channel | PUSH Channel |
| :--- | :--- |
| ![](/assets/channel_pull_status_quo_color.png) | ![](/assets/channel_push_status_quo_color.png) |
| Whenever _you start the request_ and _send card data in the request_ \(Receiver provides API\), we talk about a PULL Receiver type. | Whenever the_ Receiver starts a request_ and _you forward card data in the response _\(you provide API\), we talk about a PUSH channel type. |

Please see a list of supported channels and their respective channel type:[ Supported Receivers \(Gateways\)](/supported_receivers.md).

