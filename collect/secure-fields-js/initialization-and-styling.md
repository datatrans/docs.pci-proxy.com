# Initialization and Styling

Using Secure Fields leaves you complete control over the styling of your payment form. The card number and CVV fields or the bank account data can be styled individually.

```javascript
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

secureFields.initTokenize(
     "your-merchant-id",
     {
         cardNumber: "cardNumberPlaceholder",
         cvv: "cvvPlaceholder",
     },{            
         styles: styles,
         debug: true,
         focus: "cardNumber" // or secureFields.focus("cardNumber");
     }
 );
```

## Dynamic styling

The individual fields can also be styled dynamically:

```javascript
// the card number field
secureFields.setStyle("cardNumber", "border: 1px solid #ccc");

// the CVV field
secureFields.setStyle("cvv", "border: 1px solid #ccc")
```

## Toggled classes

Secure Fields automatically toggle CSS classes on the input fields based on various user input.&#x20;

Use, for example,

`"cardNumber.valid:hover": "background-color: green;"`&#x20;

to apply different style-based classes.

| Class name   | Description                                                                                                |
| ------------ | ---------------------------------------------------------------------------------------------------------- |
| `valid`      | When the field contains valid input.                                                                       |
| `invalid`    | When the field contains invalid input. For example a wrong card number or CVV Code                         |
| `empty`      | When the field is empty.                                                                                   |
| `identified` | When a supported brand (for example Visa or Mastercard) was detected when typing in the card number field. |

## Advanced initialization

The `initTokenize` function allows to set the input type, placeholder value and which field to be focused on right from the beginning. In addition, it is possible to set an `aria-label`. The random example from below ensures the following:

* The CVV field gets initial focus
* The CVV field's input type gets set to `tel`
* The placeholder value will be `enter your cvv`
* The CVV field input will have `aria-label="cvv aria label"`
* The credit card iframe title attribute have the value "iframe title"
* The cvv iframe title attribute will have the value "iframe title"

```javascript
secureFields.initTokenize(
    merchantId,
    {
        cardNumber: {
            placeholderElementId: "cardNumberPlaceholder",
            iframeTitle: "iframe title"
        },
        cvv:  {
            placeholderElementId: "cvvPlaceholder",
            inputType: "tel",
            placeholder: "enter your cvv",
            ariaLabel: "cvv aria label",
            iframeTitle: "iframe title"
        }
    },{        
        styles: styles,
        focus: "cvv"
    }
);
```

## Setting up payment methods

By default, all credit cards types available in your merchant setup will be accepted. Use the `paymentMethods` option if there's a need to accept only a subset of card `types`.

```javascript
secureFields.initTokenize(
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

Parameter values for "paymentMethod":

| Card Type  | paymentMethod |
| ---------- | ------------- |
| Visa       | `VIS`         |
| MasterCard | `ECA`         |
| AMEX       | `AMX`         |
| Diners     | `DIN`         |
| Discover   | `DIS`         |
| JCB        | `JCB`         |
| ELO        | `ELO`         |
| UnionPay   | `CUP`         |

## Web fonts

Web fonts are supported via the standard `@font-face` CSS rule. Because of security concerns, it is not permitted to link external resources. So, in order to get custom fonts, you need to:

* Contact [support@pci-proxy.com](mailto:support@pci-proxy.com) and provide the font files (woff, woof2, ttf etc). The files will be uploaded into your merchant id hosted files space.
* Reference the font files, by name (no path) in the styles section of the `initTokenize` call:

```javascript
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
