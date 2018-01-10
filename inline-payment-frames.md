# Quickstart: Collect card data from a website (Inline Mode)

The Inline Mode allows you to securely collect card data by injecting iframes to your DOM. A separate iframe for both, card number and CVV code is used. Thereby, sensitive data never touches your server and allows you to capture all other related card data such as cardholder name, expiry date, etc. directly by yourself.

> **The Inline Mode qualifies you for SAQ A.**

Browser compatibility for the Inline Mode:
>Internet Explorer: >= 11

>Firefox: >= 30

>Chrome: >= 32

>Safari: >= 7

>iOS Safari: >= 6

>Android: >= 5

---

## Sample

Below you can find a preview of a sample form to collect the card number and CVV code.

<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
<style>
label { display: block }
.paymentForm { border: 0px; background-color: #F7F8F9; padding: 10px }
</style>
<script src="https://code.jquery.com/jquery-1.12.4.min.js"          integrity="sha256-ZosEbRLbNQzLpnKIkEdrPv7lOy9C27hHQ+Xp8a4MxAQ="             crossorigin="anonymous"></script>

<form>
<div class="paymentForm">
  <div>
    <label for="cardNumberPlaceholder">Card Number</label>
    <div id="cardNumberPlaceholder" style="display: inline-block; width: 300px; height: 38px;">
    </div>
  </div>
  <div>
    <label for="cvvPlaceholder">Cvv</label>
    <div id="cvvPlaceholder" style="display: inline-block; width: 120px; height: 38px;">
    </div>
  </div>

  <button type="button" class="btn btn-primary" id="go">Get token!</button>
</div>
</form>

<br/>

<div id="result" class="alert alert-success" role="alert" style="display: none;"></div>

<script type="text/javascript" src="https://pay.sandbox.datatrans.com/upp/payment/js/datatrans-inline-1.0.0.js"></script>
<script type="text/javascript">

$(document).ready(function() {
  console.log("### $(document).ready called!");  
  
  function setup() { 
    
    Inline.initTokenize( 
      "1100007006", {
        cardNumber: "cardNumberPlaceholder",
        cvv: "cvvPlaceholder"
      },{
        // options...          
      }    
    );
    
    Inline.on("ready", function() {
      
      Inline.setStyle("cardNumber","width: 80%; background-color: white; border-radius: 4px; border: 1px solid #ccc; padding: .65em .5em; font-size: 91%;");
      Inline.setStyle("cardNumber::placeholder","color: #D8D8D8");
      
      Inline.setStyle("cvv","width: 80%; background-color: white; border-radius: 4px; border: 1px solid #ccc; padding: .65em .5em; font-size: 91%;");
      Inline.setStyle("cvv::placeholder","color: #D8D8D8");
      
      Inline.setPlaceholder("cardNumber", "4242 4242 4242 4242");
      Inline.setPlaceholder("cvv", "123");
      
      Inline.focus("cardNumber");
    });
    
    Inline.on("validate", function(data) {
      Inline.setStyle("cardNumber", data.fields.cardNumber.valid ? "border: 1px solid #ccc": "border: 1px solid #f00");
      Inline.setStyle("cvv", data.fields.cvv.valid ? "border: 1px solid #ccc" : "border: 1px solid #f00");
    });
    
   
    $("#go").click( function() {
      Inline.submit(); // submit the "form"  
    });
    
    Inline.on("success", function(data) {
      if(data.transactionId !== undefined) {
        var trxId = document.getElementById("result");
        trxId.textContent = "Your transactionId is: " + data.transactionId;
        trxId.style.display = 'block';
      }
    });
    
  }
    
});



</script>

---

## Step 1: Setup the Inline Mode
To get started include the following script on your page. Please make sure to always load it directly from https://pay.sandbox.datatrans.com (you can find the productive endpoint in the Web Admin Tool).

```js
<script src="https://pay.sandbox.datatrans.com/upp/payment/js/datatrans-inline-1.0.0.js"></script>
```

---

## Step 2: Create your form to collect card data
In order for the Inline Mode to insert the card number and CVV iframes at the right place, create empty DOM elements and assign them unique IDs. In the example below those are:
- `card-number-placeholder`
- `cvv-placeholder`

```html
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

---

## Step 3: Retrieving a transactionId

Initialize the Inline Mode with your merchantId and specify which DOM element containers should be used to inject the iframes:

```js
Inline.initTokenize( "1100007006", {
  cardNumber: "card-number-placeholder", 
  cvv: "cvv-placeholder"                
});
```

Afterwards you submit the form and listen for the success event:

```js
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

---

## Step 4: Using the transactionId to obtain tokens
Once you've transmitted the transactionId (step 3) to your server (together with the the rest of your form) you can execute a server to server [Token API](/inline-payment-frames/token-api.md) request to get the tokens for card number and CVV code:

```bash
$ curl "https://api.sandbox.datatrans.com/upp/services/v1/inline/token?transactionId=170419151426624571" \
       -u 'merchantId:password'
```
The password can be found in the [Web Admin Tool](https://admin.sandbox.datatrans.com) under _UPP Administartion > Security > Server-to-Server services security_. A sample response from the request above looks like:
```json
{
  "aliasCC" : "424242SKMPRI4242",
  "aliasCVV" : "gOnsckLxRMO67W_Wz89RYFyW"
}
```

Please also have a look at [Styling](/inline-payment-frames/styling.md), [Events](/inline-payment-frames/events.md) and [Token API](/inline-payment-frames/token-api.md) references.

---

> ### Congrats, Level 2 completed: Your site is out of PCI scope!
>
> You have securely captured sensitive card data on your website without sensitive data touching your servers. **Your systems never record, transmit or store real credit card data, only the token.** **Thus, you are out of PCI scope.** Move on and learn how you can use stored card data. Please continue to [**Step 3**](/step-3-use-stored-data.md).
>
> ##### Questions?
>
> Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.
>
> Phone: +41 44 256 81 91  
> Email: [support@pci-proxy.com](/mailto:support@pci-proxy.com)




