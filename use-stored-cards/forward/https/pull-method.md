# PULL Method

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
Your unique account id at PCI Proxy \(e.g. 1000011011\)
{% endapi-method-parameter %}

{% api-method-parameter name="pci-proxy-api-key" type="string" required=true %}
Your api key \(ynTIoCUuUnlHkbW460eZb0zr4WBL0ntg\)
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
In test mode, only [test credit cards](../../../test-card-data.md) are allowed.
{% endhint %}

### Process Flow

![Process Flow with PCI Proxy](../../../.gitbook/assets/channel_pull_pciproxy_color%20%281%29.png)

### Examples

Once a PULL Receiver is added to your merchantId, simply redirect requests to it via the PCI Proxy:

{% tabs %}
{% tab title="Forward to Stripe" %}
```bash
curl https://sandbox.pci-proxy.com/v1/pull \
 -H 'X-CC-MERCHANT-ID: 1000011011' \
 -H 'X-CC-SIGN: 30916165706580013' \
 -H 'X-CC-URL: https://api.stripe.com/v1/tokens' \
 -u sk_test_BQokikJOvBiI2HlWgH4olfQ2: \
 -d 'card[number]=424242SKMPRI4242' \
 -d 'card[exp_month]=12' \
 -d 'card[exp_year]=2018'
```
{% endtab %}

{% tab title="Response" %}
```markup
{
  "id": "tok_1CHoPL2eZvKYlo2Ck6KE483n",
  "object": "token",
  "card": {
    "id": "card_1CHoPL2eZvKYlo2CrbEHZ0G1",
    "object": "card",
    "address_city": null,
    "address_country": null,
    "address_line1": null,
    "address_line1_check": null,
    "address_line2": null,
    "address_state": null,
    "address_zip": null,
    "address_zip_check": null,
    "brand": "Visa",
    "country": "US",
    "cvc_check": null,
    "dynamic_last4": null,
    "exp_month": 12,
    "exp_year": 2018,
    "fingerprint": "Xt5EWLLDS7FJjR1c",
    "funding": "credit",
    "last4": "4242",
    "metadata": {},
    "name": null,
    "tokenization_method": null
  },
  "client_ip": "91.223.186.160",
  "created": 1523950759,
  "livemode": false,
  "type": "card",
  "used": false
}
```
{% endtab %}
{% endtabs %}

{% hint style="success" %}
Your request is automatically filtered for tokens. Located tokens are detokenized and your payload is populated with full card data before it arrives at the Receiver endpoint. Thereby, the Receiver API endpoint obtains full credit card data.
{% endhint %}

