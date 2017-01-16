# Quickstart: Collect card data within Web Service requests

Securely extract sensitive card data out of your web service communication.

Simply `redirect requests containing sensitive card data through PCI Proxy` to avoid sensitive data hitting your servers. PCI Proxy automatically scans requests for sensitive card data. Located card data is instantly collected, tokenized and stored in our secure vaults in Switzerland. A reference number \(token\) is issued that substitutes the sensitive data in the request or response. The message structure of the channel API always remains the same.

**All happens before sensitive card data ever touches your servers to reduce your PCI scope.**

---

## Understand channel types

The integration of PCI Proxy for Web Service depends on the channel type. In general, you either perform a pull request to receive data or a channel pushes data to your server. PCI Proxy can extract sensitive data from both.

| PULL Channel | PUSH Channel |
| :--- | :--- |
| ![](/assets/pull_status_quo.png) | ![](/assets/channel_push_status_quo.png) |
| Whenever _you start the request_ and _receive card data in the response_ \(channel provides API\), we talk about a PULL channel type.  | Whenever the _channel starts the request_ and _sends card data in the request _\(you provide API\), we talk about a PUSH channel type.  |

Please see a list of supported channels and their respective channel type: [Supported Channels](/supported_channels.md).

### Process flow: PULL channel

1. Simply redirect your channel request to PCI Proxy PULL endpoint and add 3 HTTP headers. 
2. PCI Proxy forwards your request directly to the URL in the HTTP header you just added. 
3. Channel sends response message to PCI Proxy. 
4. PCI Proxy scans response message for sensitive card data and tokenizes located card data. 
5. PCI Proxy forwards response message with tokenized credit card data to you.



---

## 2. Add channel to your account

Please send us a quick email with all [supported channels](/supported_channels.md) you would like to add to your account to [setup@pci-proxy.com](/mailto:setup@pci-proxy.com). In case, you would like to add a channel that is currently not supported, please send the following information to [setup@pci-proxy.com](mailto:):

| Information | Description |
| --- | --- |
| Merchant ID | Your merchant ID |
| Channel Type | Define if it is a push or pull channel. |
| API endpoint | The URL where we should forward the request to. |
| Sample Request & Response | Please include API name, required headers, auth fields, and request method. |

You receive a confirmation once the channel is successfully added. For push channels, you also receive `{YOUR-SPECIFIC-KEY}`.

---

## 3a. Make a PULL request

1. Add required HTTP header to your request
2. POST your XML/SOAP request having PCI Proxy as endpoint.

| **PCI Proxy PULL Endpoint:** |
| --- |
| [https://sandbox.pci-proxy.com/v1/pull](https://sandbox.pci-proxy.com/v1/pull) |

* **Required HTTP header:**

| HTTP header | Description | Example value |
| --- | --- | --- |
| `X-CC-URL` | API Endpoint - Specifies the target \(channel\) URL that will be called | [https://api.channel.com/](https://api.channel.com/) |
| `X-CC-MERCHANT-ID` | Your merchant ID | 1000011011 |
| `X-CC-SIGN` | Configured security sign | 130709090849785405 |

The X-CC-SIGN can be generated in the Datatrans Web Admin Tool \([http://pilot.datatrans.biz](http://pilot.datatrans.biz)\) under “UPP Administration” -&gt; “Security” -&gt; “Transaction Security”.

* **Example POST:**

```java
$ curl "https://pilot.datatrans.biz/upp/proxy/pull" 
        -X POST 
        -H "Content-Type: text/xml" 
        -H "X-CC-MERCHANT-ID: 1100005433" 
        -H "X-CC-URL: https://api.channel.com/" 
        -H "X-CC-SIGN: 160203112421662698" 
        -d 'yourRequest.xml'
```

> Note: In test mode, only test credit cards are allowed. For testing purposes, you will need our [test credit cards](live_mode-test.html). Learn more about [live mode and testing](live_mode-test.html).

## Receive a request from a channel \(PUSH\)

**Understanding the process flow:**

You will use the _Collect Webservice PUSH Proxy_ when the channel \(your partner\) starts the request and pushes the payment data directly to you.

![](Channel PUSH.png)

**Consider a business that needs this ability:**

_You are a travel technology company receiving new reservations from booking portals on an API endpoint at your server. As reservations may contain sensitive payment data, your servers are in PCI scope._

_With the use of PCI Proxy, payment data never touch your server and, hence, you reduce your PCI scope._

### Quick Start Guide

To switch PCI Proxy between you and a channel that pushes data, you just add a new channel. The channel can use it and invoke requests having PCI Proxy as endpoint.

1. Add a push channel to receive `{YOUR-SPECIFIC-KEY}`.
2. Exchange API endpoint with PCI Proxy PUSH endpoint at your partner.

| **Test PCI Proxy PUSH Endpoint:** |
| --- |
| [https://sandbox.pci-proxy.com/v1/push/](https://sandbox.pci-proxy.com/v1/push/) `{YOUR-SPECIFIC-KEY}` |

> Note: In test mode, only test credit cards are allowed. For testing purposes, you will need our [test credit cards](https://www.datatrans.ch/showcase/test-cc-numbers). Learn more about [live mode and testing](live_mode-test.html).

#### VPN and Leased Lines

In case the channel transmits your data over VPN or Leased Line, we can add secure connections to adapt to your needs. Please [get in touch](https://www.pci-proxy.com/#/signup) for more info.

