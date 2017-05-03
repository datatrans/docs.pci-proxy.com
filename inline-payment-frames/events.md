# Events 
Use the `Inline.on(...)` callback function to subscribe to one or more of the `ready`, `change`, `error` or `validate` events.

## On `ready` event
The ready event will be emitted once the iframes are loaded.

```js
Inline.on("ready", function() { 
 // setting a placholder for the cardNumber field
 Inline.setPlaceholder("cardNumber", "Card number");
 
 // setting a placeholder for the cvv field
 Inline.setPlaceholder("cvv", "CVV");
});
```

## On `validate` event
The validate event will be emitted once the form was submitted with
`Inline.submit();`

```js
Inline.on("validate", function(event) {
  // put a red border around the fields if they are not valid
  Inline.setStyle("cardNumber.invalid","border: 1px solid #f00");
  Inline.setStyle("cvv.invalid","border: 1px solid #f00");
});
```
Where the `event` callback object has the following structure:
```js
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

## On `success` event
The success event will be emitted if the tokenization was successful.
```js
Inline.on("success", function(event) {
  if(data.transactionId) {
    // send data.transactionId and the
    // rest of the form to your server
  }
});
```
Where the `event` callback object has the following structure:
```js
{
  "transactionId": "170407160646158477",
  "result": "success"
}
```

## On `change` event
The `change` event will be emitted whenever one of the following events are getting triggered:
* `onkeyup`
* `onkeydown`
* `onblur`
* `touchstart`
* `touchmovetouchend`
* `touchcancel`
* `touchforcechange`

```js
Inline.on("change", function(event) {
  // some fancy stuff
});
```
Where the `event` callback object has the following structure:
```js
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

## On `error` event
The error event will be emitted if there was an error after calling         `Inline.initTokenize(...)`.
Possible scenarios are:
* Wrong merchantId configured in `Inline.init(...);`
* Wrong name of cardno, cvv fields
* Wrong merchantId configuration on Datarans side

Those errors should only occur during development/testing.
```js
Inline.on("error", function(data) {
  // something bad happened
});
```

