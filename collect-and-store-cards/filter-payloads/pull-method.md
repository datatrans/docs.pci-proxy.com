# PULL Method

### Process flow

Pull method allows you to send a request via PCI Proxy to a Channel API endpoint to receive a response where the payload is filtered for credit card data and automatically tokenized. Just add the specified header parameters to your request and redirect your request to the `/v1/pull` endpoint. All other headers and your payload will be kept and routed through PCI Proxy without modification.

![Process Flow with PCI Proxy](../../.gitbook/assets/channel_pull_pciproxy_color%20%285%29.png)

{% api-method method="post" host="https://sandbox.pci-proxy.com" path="/v1/pull" %}
{% api-method-summary %}
PULL method - API request
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-cc-merchant-id" type="string" required=true %}
Your unique merchant id at PCI Proxy \(e.g. 1000011011\)
{% endapi-method-parameter %}

{% api-method-parameter name="pci-proxy-api-key" type="string" required=true %}
Your API Key \(ynTIoCUuUnlHkbW460eZb0zr4WBL0ntg\)
{% endapi-method-parameter %}

{% api-method-parameter name="x-cc-url" type="string" required=true %}
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
            <cc_number>AAABcHxr-sDssdexyrAAAfyXWIgaAF40</cc_number>
            <cc_type>Visa</cc_type>
        </customer>
        <truncated>...for better visibility</truncated>
    </reservation>   
</reservations>
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
Masked card number will be returned in the response as HTTP header`pci-proxy-masked-aliases AAABcHxr-sDssdexyrAAAfyXWIgaAF40=424242xxxxxx4242`
{% endhint %}

{% hint style="warning" %}
In test mode, only [test credit cards](../../test-card-data.md) are allowed.
{% endhint %}

### Example

Once a PULL Channel is added to your merchantId, simply redirect requests to it via the PCI Proxy:

{% tabs %}
{% tab title="Pull reservations from Booking.com" %}
```bash
curl https://sandbox.pci-proxy.com/v1/pull \
  -H 'x-cc-merchant-id: merchantId' \
  -H 'pci-proxy-api-key: MfJag98oHh0rCiSXc8g3mCsqP8wrSer7' \
  -H 'x-cc-url: https://secure-supply-xml.booking.com/hotels/xml/reservations' \
  -d '<?xml version="1.0" encoding="UTF-8"?>
        <request>
          <username>providermachinelogin</username>
          <password>********</password>
        </request>'
```
{% endtab %}

{% tab title="Response" %}
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
    <cc_number>AAABcHxr-sDssdexyrAAAfyXWIgaAF40</cc_number>
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
{% endtab %}
{% endtabs %}

{% hint style="success" %}
The response from Booking.com is automatically filtered for credit card data. Located card data is now stored in our vaults in Switzerland while card tokens have been inserted into the payload.
{% endhint %}

