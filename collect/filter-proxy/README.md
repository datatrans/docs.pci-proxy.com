# Filter Proxy

Simply redirect requests containing sensitive card data through PCI Proxy to avoid sensitive data hitting your servers. PCI Proxy automatically scans the requests for sensitive card data. Located card data is instantly collected, tokenized and stored in our secure vaults. A reference string (token) is issued that substitutes the sensitive data in the request or response. All the other headers and the payload always remain the same.

{% hint style="success" %}
All happens before sensitive card data ever touches your servers to reduce your PCI scope.
{% endhint %}

## 1. Add integrations to your account

Before we can filter payloads from a remote server you have to add the remote server as an integration to your account on the [PCI Proxy dashboard](https://dashboard.pci-proxy.com).

1. Navigate to the **Integrations** menu in the Project section and type in the name of the integration
2. Check the endpoint of the integration and press **Install**
3. Check if the payload and the endpoints fit your use case and press **Activate** finish the installation of the integration.

Continue here if you miss an integration, if the payload or an endpoint doesn't match your requirements.

1. Navigate to the **Integrations** menu in the Project section and type in the name of the integration
2. Press the **Request new Integration** button and complete the form
3. You get notified once the requested integration is ready for you.

{% hint style="warning" %}
Please note the allowed TCP ports for endpoints:

**Sandbox** Port`80`and`443`

**Production** Port`443`
{% endhint %}

## 2. Select the filter method

PCI Proxy supports two different filter methods [`/v1/pull`](broken-reference) and [`/v1/push`](broken-reference) to suit all your needs.&#x20;

Collecting card data from a partner via APIs can work in two ways. In general, either you perform a pull request to receive card data from your partner or a partner starts a push request to send you card data. PCI Proxy can extract sensitive data in both operations.

* [**/v1/pull**](broken-reference) - You start the request.

![](<../../.gitbook/assets/pull request.svg>)

* [**/v1/push**](broken-reference) - Your partner starts the request.

![](<../../.gitbook/assets/push request.svg>)

### 3. Network Tokenisation (optional)

In case you want to create Network Tokens via the Filter API, please make sure that your payload contains the expiry date of the credit card number (month and year) and that we have configured the integration on our side accordingly (check the payload mentioned on the integration which installed on your project in the dashboard).&#x20;

**Example Payload**

```javascript
    {
      "source": {
            "card": {
                "cardNumber": "4242424242424242",
                "expiry_month_number": "05",
                "expiry_year_number": "23"
                }
            }
    }
```

#### 3.1 Alias Status&#x20;

Once the request received your target url, use the alias and call the [Alias Status](../../store/manage/status.md) API to check whether a Network Token has been created. Look for the `tokenInfo` object in the response. When available, a Network Token is mapped to the PCI Proxy token.&#x20;
