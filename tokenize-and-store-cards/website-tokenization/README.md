---
description: Securely collect and tokenize card data on your website.
---

# Website Tokenization

The Inline Mode allows you to securely collect card data by injecting iframes to your DOM. A separate iframe for both, card number and CVV code is used. Thereby, sensitive data never touches your server and allows you to capture all other related card data such as cardholder name, expiry date, etc. directly by yourself.

{% hint style="success" %}
**The Inline Mode qualifies you for SAQ A.**
{% endhint %}

Browser compatibility for the Inline Mode:

* Internet Explorer: &gt;= 11 
* Firefox: &gt;= 30 
* Chrome: &gt;= 32 
* Safari: &gt;= 7 
* iOS Safari: &gt;= 6 
* Android: &gt;= 5

## Sample

Below you can find a preview of a sample form to collect the card number and CVV code.

{% embed data="{\"url\":\"https://codepen.io/pciproxy/pen/GxXeZm\",\"type\":\"rich\",\"title\":\"PCI Proxy Inline Mode Sample\",\"description\":\"The Inline Mode allows you to securely collect card data by injecting iframes to your DOM. A separate iframe for both, card number and CVV code is used...\",\"icon\":{\"type\":\"icon\",\"url\":\"https://codepen.io/favicons/favicon-192x192.png\",\"width\":192,\"height\":192,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://s3-us-west-2.amazonaws.com/m.cdpn.io/screenshot-coming-soon-small.png\",\"width\":384,\"height\":225,\"aspectRatio\":0.5859375},\"embed\":{\"type\":\"app\",\"url\":\"https://codepen.io/pciproxy/embed/preview/GxXeZm?height=300&slug-hash=GxXeZm&default-tabs=html,result&host=https://codepen.io&embed-version=2\",\"html\":\"<iframe src=\\"https://codepen.io/pciproxy/embed/preview/GxXeZm?height=300&amp;slug-hash=GxXeZm&amp;default-tabs=html,result&amp;host=https://codepen.io&amp;embed-version=2\\" style=\\"border: 0; width: 100%; height: 300px;\\" allowfullscreen></iframe>\",\"height\":300,\"aspectRatio\":null},\"caption\":\"Inline Mode Sample Script\"}" %}

## Step 1: Setup the Inline Mode

To get started include the following script on your page. Please make sure to always load it directly from [https://pay.sandbox.datatrans.com](https://pay.sandbox.datatrans.com)

```javascript
<script src="https://pay.sandbox.datatrans.com/upp/payment/js/datatrans-inline-1.0.0.js"></script>
```

Minified Version

```javascript
<script src="https://pay.sandbox.datatrans.com/upp/payment/js/datatrans-inline-1.0.0.min.js"></script>
```

## Step 2: Create your form to collect card data

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

## Step 3: Retrieving a transactionId

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

## Step 4: Using the transactionId to obtain tokens

Once you've transmitted the transactionId \(step 3\) to your server \(together with the the rest of your form\) you can execute a server to server [Token API]() request to get the tokens for card number and CVV code:

```bash
$ curl "https://api.sandbox.datatrans.com/upp/services/v1/inline/token?transactionId=170419151426624571" \
       -u 'merchantId:password'
```

The password can be found in the [Web Admin Tool](https://admin.sandbox.datatrans.com) under _UPP Administartion &gt; Security &gt; Server-to-Server services security_. A sample response from the request above looks like:

```javascript
{
  "aliasCC" : "424242SKMPRI4242",
  "aliasCVV" : "gOnsckLxRMO67W_Wz89RYFyW"
}
```

Please also have a look at [Styling](initialization-and-styling.md), [Events](events.md) and [Token API]() references.

> ### Congrats, Level 2 completed: Your site is out of PCI scope!
>
> You have securely captured sensitive card data on your website without sensitive data touching your servers. **Your systems never record, transmit or store real credit card data, only the token.** **Thus, you are out of PCI scope.** Move on and learn how you can use stored card data. Please continue to [**Step 3**](../../use-stored-cards/).
>
> #### Questions?
>
> Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.
>
> Phone: +41 44 256 81 91  
> Email: [support@pci-proxy.com](mailto:support@pci-proxy.com)

