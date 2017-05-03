# Styling

With the inline mode you have the complete control about the styling of your payment form. The card number and cvv fields can be styled individually.

```
var styles = {
    // set style to all elements, JSON accepted too
    "*": "border: 2px solid black; background-color: blue; padding: .65em .5em",

    // the same with JSON
    '*': {
        border: '2px solid black',
        padding: '.65em .5em'       
        backgroundColor: 'blue',
        backgroundImage: 'none',
        boxSizing: 'border-box',
        WebkitBoxShadow: 'none',
        WebkitAppearance: 'none'
    }

    // ::hover on all elements
    "*::hover": "-webkit-box-shadow: none; -ms-box-shadow: none; -moz-appearance: none; ",

    // set style to one of the elements
    cardNumber: "font-weight: bold;",
    cvv: "color: green;",

    // setting style based on states
    "cardNumber.valid:hover": "background-color: green;",
    "cardNumber.invalid:hover": "background-color: red;",    

    // pseudoselectors
    '*:focus': 'border: 1px solid #66AFE9',
    '*:hover': 'border: 1px solid #66AFE9',
    '*::placeholder': 'color: #999999',
    '*:-ms-input-placeholder': 'color: #999999' // thanks MS :(  
        
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
};
```

## Dynamic styling

The individual fields can also be styled dynamically based on some events.

```
// the card number field
Inline.setStyle("cardNumber", "border: 1px solid #ccc");

// the cvv field
Inline.setStyle("cvv", "border: 1px solid #ccc")
```

## Toggled classes

The inline mode automatically toggles the following CSS classes on the input fields based on various user input:

| Class name | Description |
| :--- | :--- |
| `valid` | When the field contains valid input. |
| `invalid` | When the field contains invalid input. For example a wrong card number or CVV Code. |
| `empty` | When the field is empty. |
| `identified` | When a supported brand \(for example Visa or Mastercard\) was detected when typing in the card number field. |

## Advanced initialisation


