# Quickstart: Collect card data from a website

The inline mode allows you to securely collect card data by injecting iframes to your DOM. A separate iframe for the card number and CVV code is used. Like this, sensitive data never reaches your server.

Below you can find a preview of a sample form to collect the card number and CVV code.

<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
<style>
    label { display: block }    
    .paymentForm { border: 0px; background-color: #F7F8F9; padding: 10px }
</style>

<form>
<div class="paymentForm">
<div>
<label for="cardNumberPlaceholder">Card Number</label>
<div id="cardNumberPlaceholder" style="display: inline-block; width: 300px; height: 55px;">
</div>
</div>
<div>
<label for="cvvPlaceholder">Cvv</label>
<div id="cvvPlaceholder" style="display: inline-block; width: 120px; height: 55px;"></div>
</div>

<button type="button" class="btn btn-primary" id="go">Get Token!</button>

</form>

<div id="result" class="alert alert-success" role="alert" style="display: none;"></div>
<br/>
<br/>

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
trxId.textContent = "Your payment token is: " + data.transactionId;
trxId.style.display = 'block';
}
});

</script>




