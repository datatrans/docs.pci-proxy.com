# Quickstart: Collect card data from a website

The inline mode allows you to securely collect card data by injecting iframes to your DOM. A separate iframe for the card number and CVV code is used. Like this, sensitive data never reaches your server.

Below you can find a preview of a sample form to collect the card number and CVV code.

<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
<style>
label { display: block }
.paymentForm { border: 0px; background-color: #F7F8F9; padding: 10px }
</style>
<script src="https://code.jquery.com/jquery-1.12.4.min.js"          integrity="sha256-ZosEbRLbNQzLpnKIkEdrPv7lOy9C27hHQ+Xp8a4MxAQ="             crossorigin="anonymous">
</script>


<form>
<div class="paymentForm">
  <div>
    <label for="cardNumberPlaceholder">Card Number</label>
    <div id="cardNumberPlaceholder" style="display: inline-block; width: 300px; height: 55px;">
    </div>
  </div>
  <div>
    <label for="cvvPlaceholder">Cvv</label>
    <div id="cvvPlaceholder" style="display: inline-block; width: 120px; height: 55px;">
    </div>
  </div>

  <button type="button" class="btn btn-primary" id="go">Get Token!</button>
</div>
</form>

<br/>

<div id="result" class="alert alert-success" role="alert" style="display: none;"></div>

<script type="text/javascript" src="https://pilot.datatrans.biz/upp/payment/js/datatrans-inline-1.0.0.js"></script>
<script type="text/javascript">
$(document).ready(function() {
Inline.initTokenize( "1100002469", {
cardNumber: "cardNumberPlaceholder",
cvv: "cvvPlaceholder"
});
});

$(document).ajaxComplete(function() {
Inline.initTokenize( "1100002469", {
cardNumber: "cardNumberPlaceholder",
cvv: "cvvPlaceholder"
});
});

Inline.on("ready", function() {

Inline.setStyle("cardNumber","width: 80%; background-color: white; border-radius: 4px; border: 1px solid #ccc; padding: .65em .5em; font-size: 91%;");

Inline.setStyle("cvv","width: 80%; background-color: white; border-radius: 4px; border: 1px solid #ccc; padding: .65em .5em; font-size: 91%;");

Inline.setPlaceholder("cardNumber", "4242 4242 4242 4242");
Inline.setPlaceholder("cvv", "123");

Inline.focus("cardNumber");
});

Inline.on("validate", function(data) {
Inline.setStyle("cardNumber", data.fields.cardNumber.valid ? "border: 1px solid #ccc": "border: 1px solid #f00");
Inline.setStyle("cvv", data.fields.cvv.valid ? "border: 1px solid #ccc" : "border: 1px solid #f00");
});

$(function() {
$("#go").click( function() {
Inline.submit(); // submit the "form"
})
});

Inline.on("success", function(data) {
if(data.transactionId !== undefined) {
var trxId = document.getElementById("result");
trxId.textContent = "Your transactionId is: " + data.transactionId;
trxId.style.display = 'block';
}
});
</script>

## Step 1: Setup the Inline Mode
To get started, include the following script on your page. Please make sure to always load it directly from https://pilot.datatrans.biz (you can find the productive Endpoint in the Webadmin Tool).

```js
<script src="https://pilot.datatrans.biz/upp/payment/js/datatrans-inline-1.0.0.js"></script>
```

## Step 2: Create your form to collect card data
In order for the inline mode to insert the card number and cvv iframes at the right place, create empty DOM elements and assign them unique IDs. In the example below those are:
- `card-number-placeholder`
- `cvv-placeholder`

```html
<form>
    <div class="paymentForm">
        <div>
            <label for="card-number-placeholder">Card Number</label>
            <!-- card number container -->
            <div id="card-number-placeholder" style="width: 250px; height: 55px;"></div>
        </div>
        <div>
            <label for="cvv-placeholder">Cvv</label>
            <!-- cvv container -->
            <div id="cvv-placeholder" style="width: 90px; height: 55px;"></div>
        </div>

        <button type="button" id="go">Get Token!</button>
    </div>
</form>
```

## Step 3: Retrieving a transactionId

Initialise the inline mode with your merchantId and specify which DOM element containers should be used to inject the iframes:

```js
Inline.initTokenize( "1100002469", {
  cardNumber: "card-number-placeholder", 
  cvv: "cvv-placeholder"                
});
```

Next up is to submit the form and listening for the success event.

```js
$(function() {
  $("#go").click( function() {
    Inline.submit(); // submit the "form"
  })
});

Inline.on("success", function(data) {
  if(data.transactionId !== undefined) {
    // transmit data.transactionId and the rest
    // of the form to your server    
  }
});
```

## Step 4: Using the transactionId to obtain the tokens
Once you transmitted the transaction Id retrieved in step 3 to your server (together with the the rest of your form) you can execute a server to server request to get the tokens for your card number and cvv:

```bash
$ curl "https://pilot.datatrans.biz/upp/services/v1/inline/token?transactionId=170419151426624571" \
       -u 'merchantId:password'
```
The password can be found in the webadmin tool under _UPP Administartion > Security > Server-to-Server services security_. A sample response from the request above looks like:
```json
{
  "aliasCC" : "424242SKMPRI4242",
  "aliasCVV" : "gOnsckLxRMO67W_Wz89RYFyW"
}
```
Thats all! Proceed with [one of the ways](/step-3-use-stored-data.md) to use the tokens. Please also have a look at the Styling, Events & Error handling reference.

