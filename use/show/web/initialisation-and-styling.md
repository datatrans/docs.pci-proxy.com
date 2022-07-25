---
description: Learn how to initialise and style the Secure Fields
---

# Initialisation and styling

Using Secure Fields to reveal card data leaves you in complete control over the look and feel of various elements. Each element can be styled individually.

```java
secureFields.init(
  transactionId,
  {
    cardNumber: {
      placeholderElementId: 'card-number'
    },
    cvv:  {
      placeholderElementId: 'cvv-number'
    },
    // optional copy-to-clipboard buttons:
    copyToClipboard: {
      cardNumber: {
        placeholderElementId: 'card-number-copy',
        label: 'Copy'
      },
      cvv: {
        placeholderElementId: 'cvv-number-copy',
        label: 'Copy'
      }
    }
  },
  {
    styles: {
      cardNumber: 'font-size: 100%; border-radius: 0; -webkit-appearance: none; padding: 0; background-color: transparent;',
      cvv: 'font-size: 100%; border-radius: 0; -webkit-appearance: none; padding: 0; background-color: transparent;',
      // copy-to-clipboard styling
      copyToClipboard: 'padding: 0; font-size: 0.8rem; -webkit-appearance: none; color: #333; border: 1px solid #333;'
      // 'copyToClipboard.cardNumber': 'color: red;',
      // 'copyToClipboard.cvv': 'color: green;'
    }
  }
);
```

## Dynamic styling <a href="#dynamic-styling" id="dynamic-styling"></a>

The individual fields can also be styled dynamically:

```java
// card number field
secureFields.setStyle("cardNumber", "border: 1px solid #ccc");

// copy to clipboard buttons
secureFields.setStyle("copyToClipboard", "border: 1px solid #ccc")
```

## Web fonts <a href="#web-fonts" id="web-fonts"></a>

Web fonts are supported via the standard `@font-face` CSS rule. Because of security concerns, it is not permitted to link external resources. So, in order to get custom fonts, you need to:

* Contact [support@pci-proxy.com](mailto:support@pci-proxy.com) and provide the font files (woff, woof2, ttf etc). The files will be uploaded into your merchant id hosted files space.
* Reference the font files, by name (no path) in the styles section of the `secureFields.init` call:

```java
var styles = {
    // setting the font-family to both fields
    "*": "font-family: Metamorphous;",
    "@font-face": {
        "*": {
            fontFamily: "Metamorphous",
            fontStyle: "normal",
            fontWeight: 400,
            src: "url('metamorphous.woff2') format('woff2')"
        }        
    }
}
```

