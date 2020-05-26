# Secure Fields \(iframes\)

Secure Fields allow you to securely collect card data by injecting iframes to your DOM. A separate iframe for both, card number and CVV code is used. Thereby, sensitive data never touches your server and allows you to capture all other related card data such as cardholder name, expiry date, etc. directly by yourself.

{% hint style="success" %}
**Using Secure Fields qualifies you for SAQ A.**
{% endhint %}

Browser compatibility for Secure Fields:

| **Browser** | **Version** |
| :--- | :--- |
| Chrome \| Chrome Mobile | &gt;=28 \| &gt;=28 |
| Firefox \| Firefox Mobile | &gt;=31 \| &gt;=31 |
| Internet Explorer \| Internet Explorer Mobile | &gt;=9 \| &gt;= 9 |
| Safari \| Safari Mobile | &gt;=6 \| &gt;=6 |
| Opera \| Opera Mobile | &gt;=24 \| &gt;=22 |
| Blackberry Browser | &gt;=8 |
| Android Browser | &gt;=4 |

## 1. Setup Secure Fields

To get started include the following script on your page. 

{% tabs %}
{% tab title="Secure Fields Script" %}
```javascript
<script src="https://pay.sandbox.datatrans.com/upp/payment/js/secure-fields-2.0.0.js"></script>
```
{% endtab %}

{% tab title="Minified Version" %}
```javascript
<script src="https://pay.sandbox.datatrans.com/upp/payment/js/secure-fields-2.0.0.min.js"></script>
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Please make sure to always load it directly from [https://pay.sandbox.datatrans.com](https://pay.sandbox.datatrans.com)
{% endhint %}

## 2. Create payment form

In order for Secure Fields to insert card number and CVV iframes at the right place, create empty DOM elements and assign them unique IDs. In the example below those are:

* `card-number-placeholder`
* `cvv-placeholder`

```markup
<form>
    <div>
        <div>
            <label for="card-number-placeholder">Card Number</label>
            <!-- card number container -->
            <div id="card-number-placeholder" style="width: 250px;"></div>
        </div>
        <div>
            <label for="cvv-placeholder">Cvv</label>
            <!-- cvv container -->
            <div id="cvv-placeholder" style="width: 90px;"></div>
        </div>

        <button type="button" id="go">Get Token!</button>
    </div>
</form>
```

{% hint style="warning" %}
In test mode, only [test credit cards](../../test-card-data.md) are allowed.
{% endhint %}

## 3. Retrieve a Transaction ID

Start with creating a new Secure Fields instance:

```javascript
var secureFields = new SecureFields();

// Multiple instances might be created and used independently:
// e.g. var secureFields2 = new SecureFields();
```

Initialize it with your `merchantId` and specify which DOM element containers should be used to inject the iframes:

```javascript
secureFields.initTokenize( "1100007006", {
  cardNumber: "card-number-placeholder", 
  cvv: "cvv-placeholder"                
});
```

Afterwards submit the form and listen for the success event:

```javascript
$(function() {
  $("#go").click( function() {
    secureFields.submit(); // submit the "form"
  })
});

secureFields.on("success", function(data) {
  if(data.transactionId) {
    // transmit data.transactionId and the rest
    // of the form to your server    
  }
});
```

Instances can be destroyed if no longer used:

```javascript
secureFields.destroy();
```

## 4. Obtain tokens

Once you've transmitted the `transactionId` to your server \(together with the the rest of your form\) you can execute a server to server [`GET Token`](token-api.md) request to get tokens for card number and CVV code:

{% tabs %}
{% tab title="Example: Request" %}
```bash
curl https://api.sandbox.datatrans.com/upp/services/v1/inline/token?transactionId=180416140429310027 
    -u 'merchantId:password'
```
{% endtab %}

{% tab title="Response" %}
```javascript
{
  "aliasCC": "AAABcHxr-sDssdexyrAAAfyXWIgaAF40",
  "aliasCVV": "mVHJkLRrRX-vb9uUzEM40RUN",
  "maskedCard": "424242xxxxxx4242"
}
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Please refer to [Token API](token-api.md) to see how to get the password. 
{% endhint %}

## Examples

Advanced example with card detection

GitHub repository: [https://github.com/datatrans/secure-fields-sample](https://github.com/datatrans/secure-fields-sample)  
  
Demo Basic: [https://datatrans.github.io/secure-fields-sample/](https://datatrans.github.io/secure-fields-sample/index.html)  
Demo with horizontal fields: [https://datatrans.github.io/secure-fields-sample/inline-example.html](https://datatrans.github.io/secure-fields-sample/inline-example.html)

An example of how to implement this behaviour in modern web applications can be found [here](https://github.com/datatrans/secure-fields-sample/tree/master/react-example)

{% hint style="warning" %}
In test mode, only [test credit cards](../../test-card-data.md) are allowed.
{% endhint %}

Please also have a look at [Styling](initialization-and-styling.md), [Events](events.md) and [Token API](token-api.md) references.

## Next up

{% page-ref page="../../use-stored-cards/" %}



