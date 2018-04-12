---
description: Securely collect and tokenize card data on your website.
---

# Capture \(iframes\)

The Inline Mode allows you to securely collect card data by injecting iframes to your DOM. A separate iframe for both, card number and CVV code is used. Thereby, sensitive data never touches your server and allows you to capture all other related card data such as cardholder name, expiry date, etc. directly by yourself.

{% hint style="success" %}
**The Inline Mode qualifies you for SAQ A.**
{% endhint %}

Browser compatibility for the Inline Mode:

* Internet Explorer &gt;= 11
* Firefox &gt;= 30
* Chrome &gt;= 32
* Safari &gt;= 7
* iOS Safari &gt;= 6
* Android &gt;= 5

## 1. Setup Inline Mode

To get started include the following script on your page. 

{% code-tabs %}
{% code-tabs-item title="Inline Mode Script" %}
```javascript
<script src="https://pay.sandbox.datatrans.com/upp/payment/js/datatrans-inline-1.0.0.js"></script>
```
{% endcode-tabs-item %}

{% code-tabs-item title="Minified Version" %}
```javascript
<script src="https://pay.sandbox.datatrans.com/upp/payment/js/datatrans-inline-1.0.0.min.js"></script>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="warning" %}
Please make sure to always load it directly from [https://pay.sandbox.datatrans.com](https://pay.sandbox.datatrans.com)
{% endhint %}

## 2. Create payment form

In order for the Inline Mode to insert the card number and CVV iframes at the right place, create empty DOM elements and assign them unique IDs. In the example below those are:

* `card-number-placeholder`
* `cvv-placeholder`

```markup
<form>
    <div>
        <div>
            <label for="card-number-placeholder">Card Number</label>
            <!-- card number container -->
            <div id="card-number-placeholder" style="width: 250px; height: 38px;"></div>
        </div>
        <div>
            <label for="cvv-placeholder">Cvv</label>
            <!-- cvv container -->
            <div id="cvv-placeholder" style="width: 90px; height: 38px;"></div>
        </div>

        <button type="button" id="go">Get Token!</button>
    </div>
</form>
```

## 3. Retrieve a transactionId

Initialize the Inline Mode with your merchantId and specify which DOM element containers should be used to inject the iframes:

```javascript
Inline.initTokenize( "1100007006", {
  cardNumber: "card-number-placeholder", 
  cvv: "cvv-placeholder"                
});
```

Afterwards you submit the form and listen for the success event:

```javascript
$(function() {
  $("#go").click( function() {
    Inline.submit(); // submit the "form"
  })
});

Inline.on("success", function(data) {
  if(data.transactionId) {
    // transmit data.transactionId and the rest
    // of the form to your server    
  }
});
```

## 4. Obtain tokens

Once you've transmitted the transactionId to your server \(together with the the rest of your form\) you can execute a server to server GET Token request to get tokens for card number and CVV code:

{% code-tabs %}
{% code-tabs-item title="Example: Request" %}
```bash
$ curl "https://api.sandbox.datatrans.com/upp/services/v1/inline/token?transactionId=170419151426624571" \ 
        -u 'merchantId:password'
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response" %}
```bash
{
  "aliasCC" : "424242SKMPRI4242",
  "aliasCVV" : "gOnsckLxRMO67W_Wz89RYFyW"
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Please also have a look at [Styling](initialization-and-styling.md), [Events](events.md) and [Token API](tokenapi.md) references.

## Examples

{% embed data="{\"url\":\"https://codepen.io/pciproxy/full/VXELBZ\",\"type\":\"rich\",\"title\":\"PCI Proxy Inline Mode Sample\",\"icon\":{\"type\":\"icon\",\"url\":\"https://codepen.io/favicons/favicon-192x192.png\",\"width\":192,\"height\":192,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://s3-us-west-2.amazonaws.com/i.cdpn.io/1889199.VXELBZ.small.46c6ddbe-9001-47b2-97c5-22c3134bc8d2.png\",\"width\":384,\"height\":225,\"aspectRatio\":0.5859375},\"embed\":{\"type\":\"app\",\"url\":\"https://codepen.io/pciproxy/embed/preview/VXELBZ?height=300&slug-hash=VXELBZ&default-tabs=html,result&host=https://codepen.io&embed-version=2\",\"html\":\"<iframe src=\\"https://codepen.io/pciproxy/embed/preview/VXELBZ?height=300&amp;slug-hash=VXELBZ&amp;default-tabs=html,result&amp;host=https://codepen.io&amp;embed-version=2\\" style=\\"border: 0; width: 100%; height: 300px;\\" allowfullscreen></iframe>\",\"height\":300,\"aspectRatio\":null},\"caption\":\"Inline Mode Payment Form Sample\"}" %}

{% hint style="success" %}
#### Questions?

Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.

Phone: +41 44 256 81 91  
Email: [setup@pci-proxy.com](mailto:setup@pci-proxy.com)
{% endhint %}

