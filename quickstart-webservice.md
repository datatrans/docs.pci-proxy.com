# Extract credit cards from XML/SOAP/JSON calls

Let us assume you receive or request messages including payment data \(credit cards\) via API from a partner \(channel\).

`By placing PCI Proxy between you and the channel`, payment data is extracted and automatically stored in our secure vault. A reference number \(token\) is issued that substitutes the payment data in the request or response. The message structure of the channel API always remains the same.

_You are allowed to store the token in your system, as it is not PCI DSS relevant._

The token can be used later on to charge, forward or retrieve payment data.

**All happens before sensitive payment data ever touch your server to reduce your PCI scope.**

---

**Failure Security & Response Times**

_We understand the challenges of high availability and low response times. Multiple geo-redundant server layouts and blazing fast connections ensure response times are kept at a minimum. PCI Proxy is designed to add only a fractional overhead of 5 – 50 ms per conversion._

_We also have SLAs ready for you. Please _[_get in touch_](https://www.pci-proxy.com/#/signup)_ for more info._

## How to start

> [Sign up](https://www.pci-proxy.com/#/signup) for a free developer test account.

In general, you either perform a pull request to receive data or a channel pushes data to your server. PCI Proxy can extract payment data from both.

Do you pull data from a channel \(API endpoint at the channel\) = PULL

Does the partner channel push the data directly to you \(API endpoint at you\) = PUSH

## Perform a pull request against another API \(PULL\)

**Understanding the process flow:**

You will use the _Collect Webservice PULL Proxy_ when you start the request and receive the payment data in the response.

![Channel PULL](Channel PULL.png)

**Consider a business that needs this ability:**

_You are a travel technology company pulling new reservations from portals such as Booking.com. As reservations may contain payment data, Booking.com asks for your PCI DSS compliance._

_By using PCI Proxy, Booking.com removes this requirement from you, because we as a company are PCI DSS compliant and you can bank on our full Level 1 PCI DSS compliance._

### Quick Start Guide:

1. Add a channel to your account
2. Add required HTTP header to your request.
3. POST your XML/SOAP request having PCI Proxy as endpoint.

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

