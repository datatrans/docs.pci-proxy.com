# Styling

Using Inline Mode leaves you complete control over the styling of your payment form. The card number and CVV fields can be styled individually.

```js
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

Inline.initTokenize(
     ":your-merchant-id",
     {
         cardNumber: "cardNumberPlaceholder",
         cvv: "cvvPlaceholder"
     },{            
         styles: styles,
         focus: "cardNumber" // or Inline.focus("cardNumber");
     }
 );
```

## Dynamic styling

The individual fields can also be styled dynamically:

```js
// the card number field
Inline.setStyle("cardNumber", "border: 1px solid #ccc");

// the CVV field
Inline.setStyle("cvv", "border: 1px solid #ccc")
```

## Toggled classes

The inline mode automatically toggles CSS classes on the input fields based on various user input. Use `"cardNumber.valid:hover": "background-color: green;"` for example to apply different style based classes.

| Class name | Description |
| :--- | :--- |
| `valid` | When the field contains valid input. |
| `invalid` | When the field contains invalid input. For example a wrong card number or CVV Code. |
| `empty` | When the field is empty. |
| `identified` | When a supported brand \(for example Visa or Mastercard\) was detected when typing in the card number field. |

## Advanced initialization

The `initTokenize` function allows to set the input type, placeholder value and which field to be focused right from the beginning. The \(random\) example from below ensures the following:

* The CVV field gets initial focus
* The CVV field's input type gets set to `tel`
* The placeholder value will be `enter your cvv`

```js
Inline.initTokenize(
    merchantId,
    {
        cardNumber: "cardNumberPlaceholder",
        cvv:  {
            placeholderElementId: "cvvPlaceholder",
            inputType: "tel",
            placeholder: "enter your cvv"
        }
    },{        
        styles: styles,
        focus: "cvv"
    }
);
```

## Setting up payment methods

By default all credit cards available in your merchant setup will be accepted. Use the `paymentMethods` option if there's a need to accept only a subset of card types.

```js
Inline.initTokenize(
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

## Web fonts

Web fonts are supported via the standard `@font-face` CSS rule. Because of security concerns it is not permitted to link external resources. So, in order to get custom fonts, one needs to:

* Contact support@pci-proxy.com and provide the font files \(woff, woof2, ttf etc\). The files will be uploaded into your merchant id hosted files space.
* Reference the font files, by name \(no path\) in the styles section of the `Inline.initTokenize` call:

```js
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



