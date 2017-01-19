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
| Whenever _you start the request_ and _receive card data in the response_ \(channel provides API\), we talk about a PULL channel type. | Whenever the _channel starts the request_ and _sends card data in the request _\(you provide API\), we talk about a PUSH channel type. |

Please see a list of supported channels and their respective channel type: [Supported Channels](/supported_channels.md).

### Process flow: PULL channel

1. Simply redirect your channel request to PCI Proxy PULL endpoint and add 3 HTTP headers. 
2. PCI Proxy forwards your request directly to the URL in the HTTP header you just added. 
3. Channel sends response message to PCI Proxy. 
4. PCI Proxy scans response message for sensitive card data and tokenizes located card data. 
5. PCI Proxy forwards response message with tokenized credit card data to you.

### Process flow: PUSH channel

1. Channel sends request to your specific PCI Proxy PUSH endpoint.
2. PCI Proxy recognizes channel by endpoint, scans request message for sensitive data, and tokenizes located card data. 
3. PCI Proxy forward request message with tokenized credit card data to you. 
4. Response message from you will just be passed through PCI Proxy back to channel.

---

## 1. Add channel to your account

Please send us a quick email with all [supported channels](/supported_channels.md) you would like to add to your account to [setup@pci-proxy.com](/mailto:setup@pci-proxy.com). In case, you would like to add a channel that is currently not supported, please send the following information to [setup@pci-proxy.com](mailto:):

| Information | Description |
| --- | --- |
| Merchant ID | Your merchant ID |
| Channel Type | Define if it is a push or pull channel. |
| API endpoint | The URL where we should forward the request to. |
| Sample Request & Response | Please include API name, required headers, auth fields, and request method. |

You receive a confirmation once the channel is successfully added. For push channels, you also receive `{YOUR-SPECIFIC-KEY}`.

---

## 2a. PULL: Redirect your request through PCI Proxy

Now that you have added a PULL channel to your account, you can redirect requests to that channel via the PCI Proxy. For your convenience we have prepared a little comparison of two curl samples

**Example **_**without**_** PCI Proxy**

This is just a basic example of how your request could look like and should reflect a standard XML request that you directly send to a channel API endpoint without PCI Proxy:

```java
$ curl "https://api.channel.com/"                   // HOST: Channel API Endpoint
        -X POST                                     // Request Method POST
        -H "Content-Type: text/xml"                 // Content-Type - We support almost all types
        -d 'yourRequest.xml'                        // XML Body message that is expected by Channel
```

### **Example **_**with**_** PCI Proxy**

In order to have PCI Proxy clean up and tokenize credit card data that the channel might send as a response, redirect your XML request \(`yourRequest.xml`\) through PCI Proxy by using the following curl sample:

```java
$ curl "https://sandbox.pci-proxy.com/v1/pull"       // HOST: PCI Proxy Endpoint
        -X POST                                      // Request Method POST

        -H "X-CC-MERCHANT-ID: 1100005433"            // New HEADER : Merchant ID you received during Signup
        -H "X-CC-URL: https://api.channel.com/"      // New HEADER parameter: Channel API Endpoint
        -H "X-CC-SIGN: 160203112421662698"           // New HEADER parameter: Security Sign you created in Step 1 

        -H "Content-Type: text/xml"                  // Content-Type - We support almost all types
        -d 'yourRequest.xml'                         // XML Body message that is expected by Channel
```

Universally spoken, you only need to change your current request as follows:

1. ##### Change `HOST` from Channel API Endpoint to PCI Proxy endpoint 
2. ##### Add required `HTTP header` to your request

> Good Job! The response from the channel will now automatically filtered for credit card data. Located card data will be instantly stored in our vaults in Switzerland while we put the tokenized card data in

#### PCI Proxy PULL Endpoint

| **PCI Proxy PULL Endpoint:** |
| --- |
| [https://sandbox.pci-proxy.com/v1/pull](https://sandbox.pci-proxy.com/v1/pull) |

#### **Required HTTP header**

| HTTP header | Description | Example value |
| --- | --- | --- |
| `X-CC-URL` | API Endpoint - Specifies the target \(channel\) URL that will be called | [https://api.channel.com/](https://api.channel.com/) |
| `X-CC-MERCHANT-ID` | Your merchant ID | 1000011011 |
| `X-CC-SIGN` | Configured Security Sign \(see Step1\) | 130709090849785405 |

> Note: In test mode, only test credit cards are allowed. For testing purposes, you will need our [test credit cards](live_mode-test.html). Learn more about [live mode and testing](live_mode-test.html).

---

## 2b. PUSH: Receive a request from a channel

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

