# HTTPS

## 1. Add Receiver to your account

Adding Receivers is easy. You can either pick from our list of [supported Receivers \(Gateways\)](../../resources/supported-receivers.md) or add new ones:

| Click to [**Add Receivers**](https://admin.sandbox.datatrans.com/showcase/pci-proxy/add-receiver.html) |
| :--- |
| _Learn more about _[_**Request Types**_](../../resources/request-types.md)_._ |

## 2a. Redirect a PULL Receiver through PCI Proxy

| **PCI Proxy PULL Endpoint:** |
| :--- |
| [https://sandbox.pci-proxy.com/v1/pull](https://sandbox.pci-proxy.com/v1/pull) |

If you have added a PULL Receiver to your account, you can easily redirect requests to that Receiver via the PCI Proxy.

1. **Put `token` instead of `sensitive card data` into your request**
2. **Use **[**`PCI Proxy Endpoint`**](https.md#reference)** as `HOST`**
3. **Add required **[**`X-CC HTTP header`**](https.md#reference)** to your request**
4. **Keep all other parameters of your request as always**

Redirect your XML request \(`yourRequest.xml`\) through PCI Proxy by using the following simple call:

```java
$ curl "https://sandbox.pci-proxy.com/v1/pull"       // HOST: PCI Proxy Endpoint
        -X POST                                      // Request Method POST

        -H "X-CC-MERCHANT-ID: 1000011011"            // New HEADER : Merchant ID you received during Signup
        -H "X-CC-URL: https://api.receiver.com/"     // New HEADER parameter: Receiver API Endpoint
        -H "X-CC-SIGN: 30916165706580013"            // New HEADER parameter: Security Sign you created in Step 1 

        -H "Content-Type: text/xml"                  // Content-Type - We support almost all types
        -d @yourRequest.xml                          // XML Body message that is expected by Channel
```

You have securely forwarded sensitive card data without ever touching your servers. Your request had been populated with sensitive card data while it was routed through PCI Proxy. Thereby, your Receiver obtained full credit card data.

#### Required HTTP Header:

| Header | Description | Example value |
| :--- | :--- | :--- |
| `X-CC-URL` | API Endpoint - Specifies the Receiver URL that will be called | [https://api.receiver.com/](https://www.gitbook.com/book/dtrx/pci-proxy/edit#) |
| `X-CC-MERCHANT-ID` | Your Merchant ID | 1000011011 |
| `X-CC-SIGN` | Configured Security Sign \(see [**Step1**](../../setup/)\) | 130709090849785405 |

_Note: In test mode, only test credit cards are allowed!_

## 2b. Redirect a PUSH Receiver through PCI Proxy

| **PCI Proxy PUSH Endpoint:** |
| :--- |
| [https://sandbox.pci-proxy.com/v1/push/](https://sandbox.pci-proxy.com/v1/push/) {UNIQUE-RECEIVER-KEY} |

Contrary to the PULL integration, you usually don't have much influence on how the request is started or don't want to force the Receiver to change the integration. Therefore, we use a different approach for PUSH Receiver.

When you [add a PUSH Receiver to your account](https.md#1-add-receiver-to-your-account), you receive a `{UNIQUE-RECEIVER-KEY}` for each Receiver that is set up. Together with our PCI Proxy PUSH service URL, it results in a `PCI Proxy PUSH Endpoint` that is specific to that Receiver:

Redirect requests coming from a Receiver with a single step:

1. **Change API endpoint at Receiver from `Your API Endpoint` to specific `PCI Proxy PUSH Endpoint`**
2. **Let us know IP addresses of PUSH Receiver if not already mentioned in **[**1. Add Receiver to your account**](https.md#1-add-receiver-to-your-account)
3. **Whitelist **[**IP addresses**](../../resources/ip-whitelisting.md)** of PCI Proxy at Receiver, if needed.**

If Receiver sends a request to Receiver-specific `PCI Proxy PUSH endpoint`, PCI Proxy recognizes Receiver and connects it to your account. The request from Receiver will be passed directly on to your system. Your response will be populated with sensitive card data while it was routed through PCI Proxy and forwarded to Receiver. Thereby, your Receiver obtained full credit card data.

_Note: In test mode, only test credit cards are allowed!_

## Great job**: You have successfully integrated PCI Proxy! **

> You have securely forwarded sensitive card data without ever touching your servers. **Your systems never record, transmit or store real credit card data, only the token. Thus, you are out of PCI scope. **
>
> Enjoy PCI compliance in a risk-free environment. Keep in mind that you can use stored data as often as you need it.
>
> ### Questions?
>
> Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.
>
> Phone: +41 44 256 81 91  
> Email: [support@pci-proxy.com](mailto:support@pci-proxy.com)

