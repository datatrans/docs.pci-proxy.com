# PULL

### Process Flow

The Pull method allows you to send a request via PCI Proxy to a Receiver API endpoint. Your payload will be filtered for tokens which will be automatically detokenized and sent further to the Receiver API endpoint. Just add the specified header parameters to your request and redirect your request to our `/v1/pull` endpoint. All the other headers and your payload will be kept and routed through PCI Proxy without modification.

![](<../../../.gitbook/assets/pull receiver.svg>)

{% swagger baseUrl="https://sandbox.pci-proxy.com" path="/v1/pull" method="post" summary="PULL method - API request" %}
{% swagger-description %}
The parameters marked with * are mandatory.
{% endswagger-description %}

{% swagger-parameter in="header" name="x-cc-merchant-id" type="string" required="true" %}
Your unique merchant id at PCI Proxy (e.g. 1000011011)
{% endswagger-parameter %}

{% swagger-parameter in="header" name="pci-proxy-api-key" type="string" required="true" %}
Your API key (ynTIoCUuUnlHkbW460eZb0zr4WBL0ntg)
{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-cc-url" type="string" required="true" %}
API endpoint (https://api.receiver.com/)
{% endswagger-parameter %}

{% swagger-response status="200" description="Response will contain tokenized credit card data." %}
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
{% endswagger-response %}
{% endswagger %}

{% hint style="warning" %}
In test mode, only [test credit cards](../../../resources/test-credentials.md) are allowed.
{% endhint %}

### Example

Once a PULL Receiver is added to your project, simply redirect requests to it via the PCI Proxy:

{% tabs %}
{% tab title="Forward to Stripe" %}
```bash
curl https://sandbox.pci-proxy.com/v1/pull \
 -H 'x-cc-merchant-id: 1000011011' \
 -H 'pci-proxy-api-key: api-key' \
 -H 'x-cc-url: https://api.stripe.com/v1/tokens' \
 -u sk_test_BQokikJOvBiI2HlWgH4olfQ2: \
 -d 'card[number]=AAABcHxr-sDssdexyrAAAfyXWIgaAF40' \
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
