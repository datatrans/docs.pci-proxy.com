---
description: Securely filter (extract and tokenize) card data on incoming payloads.
---

# Filter Proxy

Simply redirect requests containing sensitive card data through PCI Proxy to avoid sensitive data hitting your servers. PCI Proxy automatically scans requests for sensitive card data. Located card data is instantly collected, tokenized and stored in our secure vaults in Switzerland. A reference number \(token\) is issued that substitutes the sensitive data in the request or response. All other headers and payload always remains the same.

{% hint style="success" %}
All happens before sensitive card data ever touches your servers to reduce your PCI scope.
{% endhint %}

## 1. Add Channels

Adding Channels is easy. Before you can start to filter payloads you have to You can either pick from our list of [supported Channels](../resources/supported-channels.md) or add new ones:

| Click to [**Add Channels**](https://admin.sandbox.datatrans.com/showcase/pci-proxy/add-channel.html) |
| :--- |
| _Learn more about _[_**Request Types**_](../resources/request-types.md)_._ |

## 2. Select filter method

PCI Proxy supports two different filter methods `/v1/pull` and `/v1/push` to suit all your needs. 

Collecting card data from a Channel via web service can work in two ways. In general, either you perform a pull request to receive card data from the Channel or a Channel starts a push request to send you card data. PCI Proxy can extract sensitive data in both operations.

| `/v1/pull` method | `/v1/push` method |
| --- | --- | --- |
| You start the request. | The Channel starts the request. |
| ![](../.gitbook/assets/channel_pull_pciproxy_color%20%281%29.png) | ![](../.gitbook/assets/channel_push_pciproxy_color.png) |

{% api-method method="post" host="https://sandbox.pci-proxy.com" path="/v1/pull" %}
{% api-method-summary %}
PULL method
{% endapi-method-summary %}

{% api-method-description %}
`/v1/pull` method allows you to send a request via PCI Proxy to a Channel API endpoint to receive a response where the payload is filtered for credit card data and automatically tokenized. Just add the following header params to your request and redirect your request to the `/v1/pull` endpoint. All other headers and your payload will be kept and routed through PCI Proxy without modification.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="X-CC-MERCHANT-ID" type="string" required=true %}
Your merchant id \(e.g. 1000011011\)
{% endapi-method-parameter %}

{% api-method-parameter name="X-CC-SIGN" type="string" required=true %}
Your security sign \(e.g. 30916165706580013\)
{% endapi-method-parameter %}

{% api-method-parameter name="X-CC-URL" type="string" required=true %}
API endpoint \(https://api.channel.com/\)
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Response will contain tokenized credit card data.
{% endapi-method-response-example-description %}

```markup
<?xml version="1.0" encoding="UTF-8"?>
<reservations>
    <reservation>
        <customer>
            <cc_cvc>xC80dmLNReahfVnMNeW6DHt_</cc_cvc>
            <cc_expiration_date>07/2018</cc_expiration_date>
            <cc_name>John Doe</cc_name>
            <cc_number>424242SKMPRI4242</cc_number>
            <cc_type>Visa</cc_type>
        </customer>
        <truncated>...for better visability</truncated>
    </reservation>   
</reservations>
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="warning" %}
In test mode, only [test credit cards](../resources/sandbox-account.md) are allowed.
{% endhint %}

### Examples

Once a PULL Channel is added to your merchantId, simply redirect requests to it via the PCI Proxy:

{% code-tabs %}
{% code-tabs-item title="Pull reservations from Booking.com" %}
```bash
curl -X POST \
  https://sandbox.pci-proxy.com/v1/pull \
  -H 'Content-Type: application/xml' \
  -H 'X-CC-MERCHANT-ID: merchantId' \
  -H 'X-CC-SIGN: securitysign' \
  -H 'X-CC-URL: https://secure-supply-xml.booking.com/hotels/xml/reservations' \
  -d '<?xml version="1.0" encoding="UTF-8"?>
        <request>
          <username>providermachinelogin</username>
          <password>********</password>
        </request>'
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response" %}
```markup
<?xml version="1.0" encoding="UTF-8"?>
<reservations>
<reservation>
  <booked_at>2016-06-01T11:57:22+00:00</booked_at>
  <commissionamount>21.09</commissionamount>
  <currencycode>EUR</currencycode>
  <customer>
    <address>Vista 2, 3º izq</address>
    <cc_cvc>xC80dmLNReahfVnMNeW6DHt_</cc_cvc>
    <cc_expiration_date>07/2018</cc_expiration_date>
    <cc_name>John Doe</cc_name>
    <cc_number>424242SKMPRI4242</cc_number>
    <cc_type>Visa</cc_type>
    <city>Madrid</city>
    <company />
    <countrycode>es</countrycode>
    <dc_issue_number />
    <dc_start_date />
    <email>guest01@guest.booking.com</email>
    <first_name>Juan</first_name>
    <last_name>Valdez</last_name>
    <remarks>Booker is travelling for business...</remarks>
    <telephone>666 428 664</telephone>
    <zip>28004</zip>
  </customer>
  <!-- remaining response has been truncated for better visability -->
</reservation>
</reservations>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="success" %}
The response from Booking.com was automatically filtered for credit card data. Located card data is now stored in our vaults in Switzerland while card tokens have been inserted into the payload.
{% endhint %}

{% api-method method="post" host="https://sandbox.pci-proxy.com" path="/v1/push:uniquePushKey" %}
{% api-method-summary %}
PUSH method
{% endapi-method-summary %}

{% api-method-description %}
`/v1/push` method allows you to receive already tokenized card data on a `uniquePushKey` endpoint. Your partners can push requests to this unique PCI Proxy endpoint containing credit card data in its payload. Hence, it is routed via PCI Proxy, the payload is filtered for credit card data and automatically tokenized. All other headers and payload will be kept and routed through PCI Proxy without modification.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
Your partner can simply push its request to the `uniquePushKey` endpoint. 
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="warning" %}
In test mode, only [test credit cards](../resources/sandbox-account.md) are allowed.
{% endhint %}

### Examples

When you [**add a PUSH Channel**](filter-payloads.md#1-add-channel-to-your-account) to your account, you receive a `{uniquePushKey}` for each Channel that is set up. Together with our PCI Proxy PUSH service URL, it results in a `PCI Proxy PUSH Endpoint` that is specific to that Channel:

Redirect requests coming from a Channel with a single step:

1. **Change API endpoint at Channel from `Your API Endpoint` to specific `PCI Proxy PUSH Endpoint`**
2. **Whitelist **[**IP addresses**](../resources/ip-whitelisting.md)** from PCI Proxy at Channel, if needed.**

{% hint style="success" %}
If Channel sends a request to Channel-specific `PCI Proxy PUSH Endpoint` , PCI Proxy recognizes the Channel and connects it to your account. The request from Channel will now automatically be filtered for credit card data. Located card data will be instantly stored in our vaults in Switzerland while we insert the tokenized card data in the request and forward it to `Your API Endpoint`.
{% endhint %}

{% page-ref page="../use-stored-cards/" %}

{% hint style="info" %}
#### Questions?

Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.

Phone: +41 44 256 81 91  
Email: [setup@pci-proxy.com](mailto:support@pci-proxy.com)
{% endhint %}

