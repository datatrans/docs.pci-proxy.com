# Quickstart: Collect card data within Web Service requests

Securely extract sensitive card data out of your web service communication.

Simply `redirect requests containing sensitive card data through PCI Proxy` to avoid sensitive data hitting your servers. PCI Proxy automatically scans requests for sensitive card data. Located card data is instantly collected, tokenized and stored in our secure vaults in Switzerland. A reference number \(token\) is issued that substitutes the sensitive data in the request or response. The message structure of the channel API always remains the same.

**All happens before sensitive card data ever touches your servers to reduce your PCI scope.**

---

## 1. Add Channel to your account

Adding a Channel is easy. You can either pick from our list of [supported Channels](/supported_channels.md) or add new ones. Just use our form:

| Click to [Add a Channel](/www.pci-proxy.com) |
| :--- |


---

## 2a. PULL: Redirect your request through PCI Proxy

If you have added a PULL Channel to your account, you can easily redirect requests to that Channel via the PCI Proxy. For your convenience we have prepared a little comparison of two curl samples _with_ and _without_ PCI Proxy:

**Example **_**without**_** PCI Proxy**

This is just a basic example of how your request could look like and should reflect a standard XML request that you directly send to a channel API endpoint without PCI Proxy:

```java
$ curl "https://api.channel.com/"                   // HOST: Channel API Endpoint
        -X POST                                     // Request Method POST
        -H "Content-Type: text/xml"                 // Content-Type - We support almost all types
        -d 'yourRequest.xml'                        // XML Body message that is expected by Channel
```

#### **Example **_**with**_** PCI Proxy**

Universally spoken, you only need to change your request above as follows:

1. ##### Change `HOST` from `Channel API Endpoint` to `PCI Proxy Endpoint`
2. ##### Add required `HTTP header` to your request
3. ##### Done!

Redirect your XML request \(`yourRequest.xml`\) through PCI Proxy by using the following simple call:

```java
$ curl "https://sandbox.pci-proxy.com/v1/pull"       // HOST: PCI Proxy Endpoint
        -X POST                                      // Request Method POST

        -H "X-CC-MERCHANT-ID: 1100005433"            // New HEADER : Merchant ID you received during Signup
        -H "X-CC-URL: https://api.channel.com/"      // New HEADER parameter: Channel API Endpoint
        -H "X-CC-SIGN: 160203112421662698"           // New HEADER parameter: Security Sign you created in Step 1 

        -H "Content-Type: text/xml"                  // Content-Type - We support almost all types
        -d 'yourRequest.xml'                         // XML Body message that is expected by Channel
```

_Note: In test mode, only test credit cards are allowed!_

> ### **Congrats, Level 2 completed: Your Channel is out of PCI scope! **
>
> You have securely captured sensitive card data. The response from the channel will now automatically be filtered for credit card data. Located card data will be instantly stored in our vaults in Switzerland while we insert the tokenized card data in the response and forward it to you. **Your systems never record, transmit or store real credit card data, only the token.** **Thus, you are out of PCI scope.** Move on and learn how you can use stored card data. Please continue to [**Step 3**](/step-3-use-stored-data.md).

#### Reference

| **PCI Proxy PULL Endpoint:** |
| :--- |
| [https://sandbox.pci-proxy.com/v1/pull](https://sandbox.pci-proxy.com/v1/pull) |

---

| Required HTTP header | Description | Example value |
| :--- | :--- | :--- |
| `X-CC-URL` | API Endpoint - Specifies the target \(channel\) URL that will be called | [https://api.channel.com/](https://www.gitbook.com/book/dtrx/pci-proxy/edit#) |
| `X-CC-MERCHANT-ID` | Your merchant ID | 1000011011 |
| `X-CC-SIGN` | Configured Security Sign \(see Step1\) | 130709090849785405 |

---

## 2b. PUSH: Receive a request from a channel

Contrary to the PULL integration, you usually don't have much influence on how the request is started or don't want to force the channel to change the integration. Therefore, we use a different approach for PUSH channels.

When you [add a PUSH Channel to your account](#1-add-channel-to-your-account), you receive a `{UNIQUE-CHANNEL-KEY}` for each channel that is set up. Together with our PCI Proxy PUSH service URL, it results in a PCI Proxy PUSH Endpoint that is specific to that channel:

| **PCI Proxy PUSH Endpoint:** |
| :--- |
| [https://sandbox.pci-proxy.com/v1/push/](https://sandbox.pci-proxy.com/v1/push/) `{UNIQUE-CHANNEL-KEY}` |

Redirect requests coming from a channel with a single step:

1. ##### Change API endpoint at the channel from `Your API Endpoint` to channel-specific `PCI Proxy PUSH Endpoint`
2. ##### Done!

_Note: In test mode, only test credit cards are allowed!_

> ### **Congrats, Level 2 completed: Your channel is out of PCI scope! **
>
> If the channel now sends a request to the channel-specific PCI Proxy PUSH endpoint, PCI Proxy recognizes the channel and connects it to your account. The request coming from the channel will now automatically be filtered for credit card data. Located card data will be instantly stored in our vaults in Switzerland while we insert the tokenized card data in the request and forward it to you.
>
> Thereby, you have securely captured sensitive card data. **Your systems never record, transmit or store real credit card data, only the token.** **Thus, you are out of PCI scope.** Move on and learn how you can use stored card data. Please continue to [**Step 3**](/step-3-use-stored-data.md).

#### Reference

| PUSH Process Flow with PCI Proxy |
| :--- |
| ![](/assets/channel_push_pciproxy_color.png) |
| 1. Channel sends request to channel-specific PCI Proxy PUSH endpoint. |
| 2. PCI Proxy recognizes channel by endpoint, scans request message for sensitive data, and tokenizes located card data. |
| 3. PCI Proxy forward request message with tokenized credit card data to you. |
| 4. Response message from you will just be passed through PCI Proxy back to channel. |

---

> ##### Questions?
>
> Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.
>
> Phone: +41 44 256 81 91  
> Email: [support@pci-proxy.com](/mailto:support@pci-proxy.com)



