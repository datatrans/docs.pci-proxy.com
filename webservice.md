# Quickstart: Collect card data from a Channel \(Web Service\)

Securely extract sensitive card data out of your web service communication.

Simply `redirect requests containing sensitive card data through PCI Proxy` to avoid sensitive data hitting your servers. PCI Proxy automatically scans requests for sensitive card data. Located card data is instantly collected, tokenized and stored in our secure vaults in Switzerland. A reference number \(token\) is issued that substitutes the sensitive data in the request or response. The message structure of the channel API always remains the same.

**All happens before sensitive card data ever touches your servers to reduce your PCI scope.**

---

## 1. Add Channel to your account

Adding Channels is easy. You can either pick from our list of [supported Channels](/supported_channels.md) or add new ones:

| Click to [**Add Channels**](https://admin.sandbox.datatrans.com/showcase/pci-proxy/add-channel.html) |
| :--- |
| _Learn more about _[_**Request Types**_](/request-types.md)_._ |

---

## 2a. Redirect a PULL Channel through PCI Proxy

If you have added a PULL Channel to your account, you can easily redirect requests to that Channel via the PCI Proxy.

1. ##### Use[`PCI Proxy Endpoint`](#reference)  as `HOST`
2. ##### Add required [`X-CC HTTP header`](#reference) to your request
3. ##### Keep all other parameters of your request as always

Redirect your XML request \(`yourRequest.xml`\) through PCI Proxy by using the following simple call:

```java
$ curl "https://sandbox.pci-proxy.com/v1/pull"       // HOST: PCI Proxy Endpoint
        -X POST                                      // Request Method POST

        -H "X-CC-MERCHANT-ID: 1000011011"            // New HEADER parameter: Merchant ID you received during Signup
        -H "X-CC-URL: https://api.channel.com/"      // New HEADER parameter: Channel API Endpoint
        -H "X-CC-SIGN: 30916165706580013"            // New HEADER parameter: Security Sign you created in Step 1 

        -H "Content-Type: text/xml"                  // Content-Type - We support almost all types
        -d @yourRequest.xml                          // XML Body message that is expected by Channel
```

For instance, if you want to pull reservations from Channel Booking.com, see the following sample:

```bash
curl "https://sandbox.pci-proxy.com/v1/pull" -X POST -H "Content-Type: text/xml" -H "X-CC-SIGN: 30916165706580013" -H "X-CC-MERCHANT-ID: 1000011011" -H "X-CC-URL: https://secure-supply-xml.booking.com/hotels/xml/reservations" -d '
<request>
  <username>your-user</username>
  <password>your-pass</password>
</request>'
```

You have securely captured sensitive card data. The response from the channel will now automatically be filtered for credit card data. Located card data will be instantly stored in our vaults in Switzerland while we insert the tokenized card data in the response and forward it to you.

##### Required HTTP Header:

| Header | Description | Example value |
| :--- | :--- | :--- |
| `X-CC-URL` | API Endpoint - Specifies the Channel URL that will be called | [https://api.channel.com/](https://www.gitbook.com/book/dtrx/pci-proxy/edit#) |
| `X-CC-MERCHANT-ID` | Your Merchant ID | 1000011011 |
| `X-CC-SIGN` | Configured Security Sign \(see [**Step1**](/step-1-signup-and-setup.md)\) | 30916165706580013 |

_Note: In test mode, only test credit cards are allowed!_

---

## 2b. Redirect a PUSH Channel through PCI Proxy

Contrary to the PULL integration, you usually don't have much influence on how the request is started or don't want to force the Channel to change the integration. Therefore, we use a different approach for PUSH Channels.

When you [**add a PUSH Channel**](#1-add-channel-to-your-account) to your account, you receive a `{UNIQUE-CHANNEL-KEY}` for each Channel that is set up. Together with our PCI Proxy PUSH service URL, it results in a `PCI Proxy PUSH Endpoint` that is specific to that Channel:

Redirect requests coming from a Channel with a single step:

1. ##### Change API endpoint at Channel from `Your API Endpoint` to specific [https://sandbox.pci-proxy.com/v1/push/](https://sandbox.pci-proxy.com/v1/push/) `{UNIQUE-CHANNEL-KEY}`
2. ##### Whitelist [IP addresses](/ip_whitelisting.md) from PCI Proxy at Channel, if needed.

##### 

If Channel sends a request to Channel-specific `PCI Proxy PUSH Endpoint` , PCI Proxy recognizes the Channel and connects it to your account. The request from Channel will now automatically be filtered for credit card data. Located card data will be instantly stored in our vaults in Switzerland while we insert the tokenized card data in the request and forward it to `Your API Endpoint`.

_Note: In test mode, only test credit cards are allowed!_

---

> ### **Congrats, Level 2 completed: Your Channels are out of PCI scope!**
>
> You have securely captured sensitive card data. **Your systems never record, transmit or store real credit card data, only the token. Thus, you are out of PCI scope. **Move on and learn how you can use stored card data. Please continue to [**Step 3**](/step-3-use-stored-data.md).
>
> ##### Questions?
>
> Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.
>
> Phone: +41 44 256 81 91  
> Email: [support@pci-proxy.com](/mailto:support@pci-proxy.com)



