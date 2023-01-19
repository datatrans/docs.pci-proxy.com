# Events

Use the `secureFields.on(...)` callback function to subscribe to one or more of the `ready`, `change`, `cardInfo`, `error` or `validate` events.

{% tabs %}
{% tab title="on ready" %}
The ready event will be emitted once the iframes are loaded.

```javascript
secureFields.on("ready", function() { 
 // setting a placeholder for the cardNumber field
 secureFields.setPlaceholder("cardNumber", "Card number");

 // setting a placeholder for the CVV field
 secureFields.setPlaceholder("cvv", "CVV");
});
```
{% endtab %}

{% tab title="on validate" %}
The validate event will be emitted once the form was submitted with `secureFields.submit();`

```javascript
secureFields.on("validate", function(event) {
  // put a red border around the fields if they are not valid
  secureFields.setStyle("cardNumber.invalid","border: 1px solid #f00");
  secureFields.setStyle("cvv.invalid","border: 1px solid #f00");
});
```



Where the `event` callback object has the following structure:

```javascript
{
  "fields": {
    "cardNumber": {
      "length": 0,
      "valid": false
    },
    "cvv": {
      "length": 3,
      "valid": true
    }
  },
  "hasErrors": true // indicates if one of the fields has valid=false
}
```
{% endtab %}

{% tab title="on change" %}
The `change` event will be emitted whenever one of the following events are getting triggered:&#x20;

* `focus`
* `blur`
* `keyUp`
* `keyDown`
* `touchstart`
* `touchmovetouchend`
* `touchcancel`
* `touchforcechange`
* `autocomplete`

```
secureFields.on("change", function(event) {
  // some fancy stuff
});
```



Where the `event` callback object has the following structure:

```json
{
  "fields": {
    "cardNumber": {
      "length": 0,
      "valid": false
    },
    "cvv": {
      "length": 0,
      "valid": false
    }
  },
  "hasErrors": true,
  "event": {
    "field": "cardNumber",  // the affected input field
    "type": "blur"          // the original event
  }
}
```

****

#### **Browser autofill**

Events of type `autocomplete` are triggered if a user makes use of their browser's integrated credit card autofill feature which typically provides expiry month and year alongside credit card number and cvv. While you should never come in touch with the latter, expiry data can be captured and filled into form fields located on merchant side in order to lower friction for the user during the payment process.

Callback object:

```json
// expiry month provided via browser autofill
{
  // ...
  "event": {
    "type": "autocomplete",
    "field": "expiryMonth",
    "value": "12"    
  }
}

// expiry year provided via browser autofill
{
  // ...
  "event": {
    "type": "autocomplete",
    "field": "expiryYear",
    "value": "2021"    
  }
}
```



Sample code

```javascript
var expiryMonth, expiryYear;

secureFields.on("change", function(data) {
  var event = data.event;
  
  if (event.type === "autocomplete") {
    if (event.field === "expiryMonth") {
      expiryMonth = event.value; // "12"
      return;
    }
    
    if (event.field === "expiryYear") {
      expiryYear = event.value.slice(-2); // "2021" (note: take the last two digits for MM/YY)
      return;
    }
  }
});
```
{% endtab %}

{% tab title="on cardInfo" %}
The `cardInfo` event will be emitted when`secureFields.getCardInfo()`is called.



```javascript
secureFields.on("cardInfo", function(event) {
  // call backend, decide stuff ;)
});
```

```javascript
{
	"event": "cardInfo",
	"data": {
		"cardInfo": {
			"brand": "VISA CREDIT",
			"type": "credit",
			"usage": "consumer",
			"country": "GB",
			"issuer": "DATATRANS"
		},
		"maskedCard": "424242xxxxxx4242",
		"paymentMethod": "VIS"
	}
}
```

Calling `secureFields.getCardInfo(callback)` is the alternative way to obtain the information about the entered card by having the given callback function receive it rather than waiting for an event.
{% endtab %}

{% tab title="on success" %}
The success event will be emitted if the tokenization was successful.

```javascript
secureFields.on("success", function(data) {
  if(data.transactionId) {
    // send data.transactionId and the
    // rest of the form to your server
  }
});
```

Where the `event` callback object has the following structure:

```javascript
{
  "result": "success",
  "transactionId": "180403204621339015",
  "cardInfo":
  {
    "brand": "VISA DEBIT",
    "issuer": "Some Bank",
    "type": "debit", // debit or credit
    "usage": "unknown", // consumer, corporate or unknown
    "country": "US" // 2 letter ISO 3166-1 alpha-2 country code
  }
}
```
{% endtab %}

{% tab title="on error" %}
Possible scenarios are:

* Wrong merchantId configured in `secureFields.initTokenize(...);`
* Wrong name of card number, CVV fields
* Wrong merchantId configuration on Datatrans side



```javascript
secureFields.on("error", function(data) {
  // something bad happened
});
```
{% endtab %}
{% endtabs %}

