# Token-Format

PCI Proxy Credit Card Tokens are available in different formats to adapt perfectly with your existing infrastructure. 

1. Full Substitution `1234567890123456789`

2. Masked Credit Card Alias `123456ABCDEF1234`

| Full Substitution | Masked Credit Card Alias |
| -- | -- |
| 19 digits substitute for full tokenization of credit card number | Consisting of the first 6 digits of the credit card number (BIN Range), followed by the actual token in form of 6 upper-case letters.  |

| Example: `1234567890123456789` | Example: `123456ABCDEF1234` |