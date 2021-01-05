# Events

Use the `secureFields.on(...)` callback function to subscribe to one or more of the `ready`, `change`, `error` or `validate` events.

{% tabs %}
{% tab title="on ready" %}
The ready event will be emitted once the iframes are loaded.

```javascript
secureFields.on("ready", function() { 
 // setting a placholder for the cardNumber field
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
The `change` event will be emitted whenever one of the following events are getting triggered:

* `focus`
* `blur`
* `keyUp`
* `keyDown`
* `touchstart`
* `touchmovetouchend`
* `touchcancel`
* `touchforcechange`

```javascript
secureFields.on("change", function(event) {
  // some fancy stuff
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
{% endtab %}

{% tab title="on cardInfo" %}
The `cardInfo` event will be emitted when`secureFields.getCardInfo()`is called.

```javascript
secureFields.on("cardInfo", function(event) {
  // call backend, decide surcharges ;)
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
  "result":"success",
  "transactionId":"180403204621339015",
  "cardInfo":
  {
    "brand":"VISA DEBIT",
    "issuer":"Some Bank",
    "type":"debit", // debit or credit
    "usage":"unknown", // consumer or corporate
    "country":"US"
  }
}
```
{% endtab %}

{% tab title="on error" %}
The error event will be emitted if there was an error after calling `secureFields.initTokenize(...)`.

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



