# Quickstart: Forward card data to a Receiver via web service

PCI Proxy allows you to retain your existing data communication with PCI-compliant Receiver. This can be online travel agencies, payment gateways, hotels, airlines, car rentals, etc.

> **Forwarding card data to a Receiver works the same way as **[**collecting card data via web service**](/webservice.md)**.**

Simply `redirect requests containing tokens through PCI Proxy` to avoid sensitive data hitting your servers. PCI Proxy automatically scans requests for tokens and replaces located tokens with sensitive card data and forwards the populated request to the PCI-compliant Receiver. The message structure of your request always remains the same. Any responses from the Receiver are passed back to you and sensitive card data is tokenized if needed.

**Your requests are populated with sensitive card data after they left your systems to keep you out of PCI scope.**

---

## 1. Add Receiver to your account

**Add Receiver**

Please send us a quick email with all [Supported Receivers \(Gateways\)](/supported_receivers.md) you would like to add to your account to [setup@pci-proxy.com](/mailto:setup@pci-proxy.com). In case, you would like to add a Receiver that is currently not supported, please send the following information to [setup@pci-proxy.com](mailto:):

| Information | Description |
| --- | --- |
| Merchant ID | Your merchant ID |
| Channel Type | Define if it is a push or pull channel. |
| API endpoint | The URL where we should forward the request to. |
| Sample Request & Response | Please include API name, required headers, auth fields, and request method. |

You receive a confirmation once the Receiver is successfully added. For PUSH Receiver, you also receive `{UNIQUE-CHANNEL-KEY}`.

---

## 2a. PULL: Redirect your request through PCI Proxy

Now that you have added a PULL Receiver to your account, you can easily redirect requests to that Receiver via the PCI Proxy. For your convenience we have prepared a little comparison of two curl samples _with_ and _without_ PCI Proxy:

**Example **_**without**_** PCI Proxy**

This is just a basic example of how your request could look like and should reflect a standard XML request that you directly send to a channel API endpoint without PCI Proxy:

```java
$ curl "https://api.receiver.com/"                   // HOST: Receiver API Endpoint
        -X POST                                     // Request Method POST
        -H "Content-Type: text/xml"                 // Content-Type - We support almost all types
        -d 'yourRequest.xml'                        // XML Body message that is expected by Channel
```

#### **Example **_**with**_** PCI Proxy**

Universally spoken, you only need to change your request above as follows:

1. ##### Change `HOST` from`Receiver API Endpoint` to `PCI Proxy Endpoint`
2. ##### Add required `HTTP header` to your request
3. ##### Done!

Redirect your XML request \(`yourRequest.xml`\) through PCI Proxy by using the following simple call:

```java
$ curl "https://sandbox.pci-proxy.com/v1/pull"       // HOST: PCI Proxy Endpoint
        -X POST                                      // Request Method POST

        -H "X-CC-MERCHANT-ID: 1100005433"            // New HEADER : Merchant ID you received during Signup
        -H "X-CC-URL: https://api.receiver.com/"     // New HEADER parameter: Receiver API Endpoint
        -H "X-CC-SIGN: 160203112421662698"           // New HEADER parameter: Security Sign you created in Step 1 

        -H "Content-Type: text/xml"                  // Content-Type - We support almost all types
        -d 'yourRequest.xml'                         // XML Body message that is expected by Channel
```

_Note: In test mode, only test credit cards are allowed!_

> ### **Congrats, Level 3 completed: You have forwarded card data to a Receiver! **
>
> You have securely forwarded sensitive card data without ever touching your servers. The request will automatically from the Receiver will now automatically be filtered for credit card data. Located card data will be instantly stored in our vaults in Switzerland while we insert the tokenized card data in the response and forward it to you. **Your systems never record, transmit or store real credit card data, only the token.** **Thus, you are out of PCI scope.** Move on and learn how you can use stored card data. Please continue to [**Step 4**](/step-4-go-live.md).

#### Reference

| PULL Process Flow with PCI Proxy |
| :--- |
| ![](/assets/channel_pull_pciproxy_color.png) |
| 1. Simply redirect your channel request to PCI Proxy PULL endpoint and add 3 HTTP headers. |
| 2. PCI Proxy forwards your request directly to the URL in the HTTP header you just added. |
| 3. Channel sends response message to PCI Proxy. |
| 4. PCI Proxy scans response message for sensitive card data and tokenizes located card data. |
| 5. PCI Proxy forwards response message with tokenized credit card data to you. |

---

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

> ### **Congrats, Level 2 completed: You are out of PCI scope! **
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



