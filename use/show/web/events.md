---
description: Make use of Secure Fields callback events
---

# Events

Use the `secureFields.on(...)` callback function to subscribe to events.

{% tabs %}
{% tab title="on ready" %}
The ready event will be emitted once the iframes are loaded.

```javascript
secureFields.on("ready", function() { 
  // fields have been rendered
});
```
{% endtab %}

{% tab title="on error" %}
```javascript
secureFields.on("error", function(data) {
  // something bad happened
});
```
{% endtab %}

{% tab title="on copyToClipboard" %}
The copyToClipboard event will be emitted if a value has been successfully copied to clipboard. This could be used to show a hint to the user.

```javascript
secureFields.on("copyToClipboard", function(data) {
  if (data.result === 'error') {
    console.error('Error copying ' + data.field + ' to clipboard!. Reason: ' + data.error);
    return;
  }
  
  console.log(data.field + ' copied to clipboard!'); // field is either "cardNumber" or "cvv"
});
```


{% endtab %}
{% endtabs %}

