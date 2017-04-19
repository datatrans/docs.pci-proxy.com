# Quickstart: Collect card data from a website

The inline mode allows you to securely collect card data by injecting iframes to your DOM. A separate iframe for the card number and CVV code is used. Like this, sensitive data never reaches your server.

Below you can find a preview of a sample payment form.

<style>
    label { display: block }
    button { font-size: 90% }
</style>

<form>
<fieldset>
<div>
<label for="cardNumberPlaceholder">Card Number</label>
<div id="cardNumberPlaceholder" style="display: inline-block; width: 500px; height: 55px;">
</div>
</div>
<div>
<label for="cvvPlaceholder">Cvv</label>
<div id="cvvPlaceholder" style="display: inline-block; width: 250px; height: 55px;"></div>
</div>

<button type="button" id="go">GO</button>
</fieldset>
</form>

<script type="text/javascript" src="https://pilot.datatrans.biz/upp/payment/js/datatrans-inline-1.0.0.js"></script>
<script type="text/javascript">
Inline.initTokenize( "1100002469", {
cardNumber: "cardNumberPlaceholder", 
cvv: "cvvPlaceholder"           
});


Inline.on("ready", function() {

Inline.setStyle("cardNumber","width: 80%; border-radius: 1px; border: 1px solid #ccc; padding: .65em .5em; font-size: 91%;");

Inline.setStyle("cvv","width: 80%; border-radius: 3px; border: 1px solid #ccc; " padding: .65em .5em; font-size: 91%;");

Inline.setPlaceholder("cardNumber", "card goes here");

Inline.setPlaceholder("cvv", "cvv here");

Inline.focus("cardNumber");
});

</script>




