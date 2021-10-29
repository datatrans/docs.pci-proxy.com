# Initialization and Styling

Using Secure Fields leaves you complete control over the styling of your payment form. The card number and CVV fields can be styled individually.

```java
var styles = {
    // set style to all elements, JSON accepted too
    "*": "border: 2px solid black; background-color: blue; padding: .65em .5em",

    // or with JSON
    //'*': {
    //    border: '2px solid black',
    //    padding: '.65em .5em'       
    //    backgroundColor: 'blue',  // background-color
    //    backgroundImage: 'none',  // background-image
    //    boxSizing: 'border-box',  // box-sizing
    //    WebkitBoxShadow: 'none',  // -webkit-box-shadow
    //    WebkitAppearance: 'none'  // -webkit-appearance
    //}

    // ::hover on all elements
    "*::hover": "-webkit-box-shadow: none; -ms-box-shadow: none; -moz-appearance: none; ",

    // set style to one of the elements
    cardNumber: "font-weight: bold;",
    cvv: "color: green;",

    // setting style based on CSS classes (see 'Toggled classes')
    "cardNumber.valid:hover": "background-color: green;",
    "cardNumber.invalid:hover": "background-color: red;",    

    // pseudoselectors
    '*:focus': 'border: 1px solid #66AFE9',
    '*:hover': 'border: 1px solid #66AFE9',
    '*::placeholder': 'color: #999999',
    '*:-ms-input-placeholder': 'color: #999999' // thanks MS :( 
};

secureFields.init(
     "your-merchant-id",
     {
         cardNumber: "cardNumberPlaceholder",
         cvv: "cvvPlaceholder",
     },{            
         styles: styles,
         focus: "cardNumber" // or secureFields.focus("cardNumber");
     }
 );
```

## Dynamic styling <a href="dynamic-styling" id="dynamic-styling"></a>

The individual fields can also be styled dynamically:

```java
// the card number field
secureFields.setStyle("cardNumber", "border: 1px solid #ccc");

// the CVV field
secureFields.setStyle("cvv", "border: 1px solid #ccc")
```

## Toggled classes <a href="toggled-classes" id="toggled-classes"></a>

Secure Fields automatically toggle CSS classes on the input fields based on various user input. Use `"cardNumber.valid:hover": "background-color: green;"` for example to apply different style based classes.

| **Class name** | **Description**                                                                                            |
| -------------- | ---------------------------------------------------------------------------------------------------------- |
| `valid`        | When the field contains valid input.                                                                       |
| `invalid`      | When the field contains invalid input. For example a wrong card number or CVV Code.                        |
| `empty`        | When the field is empty.                                                                                   |
| `identified`   | When a supported brand (for example Visa or Mastercard) was detected when typing in the card number field. |

## Advanced initialization <a href="advanced-initialization" id="advanced-initialization"></a>

The `secureFields.init` function allows to set the input type, placeholder value and which field to be focused right from the beginning. In addition it is possible to set an `aria-label`. The (random) example from below ensures the following:

* The CVV field gets initial focus
* The CVV field's input type gets set to `tel`
* The placeholder value will be `enter your cvv`
* The CVV field input will have `aria-label="cvv aria label"`

```java
secureFields.init(
    merchantId,
    {
        cardNumber: "cardNumberPlaceholder",
        cvv:  {
            placeholderElementId: "cvvPlaceholder",
            inputType: "tel",
            placeholder: "enter your cvv",
            ariaLabel: "cvv aria label"
        }
    },{        
        styles: styles,
        focus: "cvv"
    }
);       
```

## Setting up payment methods <a href="setting-up-payment-methods" id="setting-up-payment-methods"></a>

By default all credit cards available in your merchant setup will be accepted. Use the `paymentMethods` option if there's a need to accept only a subset of card `types`.

```java
secureFields.init(
    merchantId,
    {
        cardNumber: "cardNumberPlaceholder",
        cvv:  "cvvPlaceholder"
    },{        
        styles: styles,
        paymentMethods: ["ECA", "VIS"]  // allowing Mastercard and Visa only
    }
);
```

Parameter values for “paymentmethod”:

| **Card type**  | **paymentMethod** |
| -------------- | ----------------- |
| Visa           | `VIS`             |
| MasterCard     | `ECA`             |
| AMEX           | `AMX`             |
| Diners         | `DIN`             |
| Discover       | `DIS`             |
| JCB            | `JCB`             |
| ELO            | `ELO`             |
| China UnionPay | `CUP`             |

## Web fonts <a href="web-fonts" id="web-fonts"></a>

Web fonts are supported via the standard `@font-face` CSS rule. Because of security concerns it is not permitted to link external resources. So, in order to get custom fonts, you need to:

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

[\
](https://docs.pci-proxy.com/collect-and-store-cards/capture-iframes)
