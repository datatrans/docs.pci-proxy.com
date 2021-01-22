# Glossary

#### ECI

the Electronic Commerce Indicator is a Payment System-specific value provided by the ACS or DS to indicate the results of the attempt to authenticate the Cardholder.  
Possible value returned by [**Visa**](https://usa.visa.com/dam/VCOM/download/merchants/verified-by-visa-acquirer-merchant-implementation-guide.pdf), **American Express** and its interpretation:

* **ECI 05:** 3DS authentication was successful; transactions are secured by 3DS.
* **ECI 06:** authentication was attempted but was not or could not be completed; possible reasons being either the card or its Issuing Bank has yet to participate in 3DS.
* **ECI 07: 3DS authentication is either failed or could not be attempted; possible reasons being both card and Issuing Bank are not secured by 3DS, technical errors, or improper configuration.**  

Possible value returned by [**MasterCard**](https://www.mastercard.us/content/dam/mccom/en-us/documents/SMI_Manual.pdf) and its interpretation:

* **ECI 02:** 3DS authentication is successful; both card and Issuing Bank are secured by 3DS.
* **ECI 01:** 3DS authentication was attempted but was not or could not be completed; possible reasons being either the card or its Issuing Bank has yet to participate in 3DS, or cardholder ran out of time to authorize.
* **ECI 00: 3DS authentication is either failed or could not be attempted; possible reasons being both card and Issuing Bank are not secured by 3DS, technical errors, or improper configuration.**

