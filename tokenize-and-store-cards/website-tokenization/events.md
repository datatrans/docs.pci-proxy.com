---
description: Callback function to listen in on events for Inline Mode
---

# Events

Use the `Inline.on(...)` callback function to subscribe to one or more of the `ready`, `change`, `error` or `validate` events.

{% tabs %}
{% tab title="on ready" %}
The ready event will be emitted once the iframes are loaded.

```javascript
Inline.on("ready", function() { 
 // setting a placholder for the cardNumber field
 Inline.setPlaceholder("cardNumber", "Card number");

 // setting a placeholder for the CVV field
 Inline.setPlaceholder("cvv", "CVV");
});
```
{% endtab %}

{% tab title="on validate" %}
The validate event will be emitted once the form was submitted with `Inline.submit();`

```javascript
Inline.on("validate", function(event) {
  // put a red border around the fields if they are not valid
  Inline.setStyle("cardNumber.invalid","border: 1px solid #f00");
  Inline.setStyle("cvv.invalid","border: 1px solid #f00");
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

{% tab title="on success" %}
The success event will be emitted if the tokenization was successful.

```javascript
Inline.on("success", function(data) {
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
    "distinction":"unknown", // consumer or corporate
    "country":"US"
  }
}
```
{% endtab %}

{% tab title="on change" %}
The `change` event will be emitted whenever one of the following events are getting triggered:

* `onkeyup`
* `onkeydown`
* `onblur`
* `touchstart`
* `touchmovetouchend`
* `touchcancel`
* `touchforcechange`

```javascript
Inline.on("change", function(event) {
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

{% tab title="on error" %}
The error event will be emitted if there was an error after calling `Inline.initTokenize(...)`.  
Possible scenarios are:

* Wrong merchantId configured in `Inline.init(...);`
* Wrong name of card number, CVV fields
* Wrong merchantId configuration on Datatrans side

Those errors should only occur during development/testing.

```javascript
Inline.on("error", function(data) {
  // something bad happened
});
```
{% endtab %}
{% endtabs %}



