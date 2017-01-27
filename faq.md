# Frequently Asked Questions

**How does PCI Proxy reduce my PCI DSS scope?**

> The key for merchants and service providers wishing to reduce their PCI DSS scope is to not store, process, or transmit any sensitive cardholder data. By using PCI Proxy, we take care of that challenge by shielding your servers from sensitive card data. As a result, your servers never get in touch with sensitive card data again and you can rely on our full PCI DSS Level 1 certification.

**What credit card types does PCI Proxy support?**

> PCI Proxy automatically collects, stores, and tokenizes all PCI DSS relevant card data. Currently, we support all major brands and additional virtual cards such as Visa, Mastercard, American Express, Diners, Discover, JCB, Maestro, Expedia Virtual Cards, Booking.com Virtual Cards, AirPlus, etc. Do you need additional brands to be tokenized? Contact us.

**What token formats does PCI Proxy support?**

> PCI Proxy Credit Card Tokens are available in different formats to adapt perfectly with your existing infrastructure.
>
> | Standard: Masked Credit Card Alias | Full Substitution Token |
> | --- | --- |
> | The format consists of the first 6 digits of the real credit card number, the actual BIN Range \(Bank Identification Number\), followed by the token in form of 6 upper-case letters. The Masked Credit Card Alias ends with the last 4 digits of the actual credit card number. | 19 digits substitute for full tokenization of credit card number. |
> | Example: _**1234 56AB CDEF 3456**_ | Example:_** 1198182968382186732**_ |

**Why do I have to provide the PCI DSS Attestation of Compliance \(AoC\) if I want to pass stored card data on to a 3rd party?**

> In order to forward plain credit card data to a 3rd party, that 3rd party needs to be PCI compliant. The PCI DSS Attestation of Compliance \(AoC\) is an obligation for each party involved in the credit card acceptance or transmission. Therefore, it is your responsibility to make sure you are collaborating with the right partners. Knowing your partners' compliance status provides assurance and awareness about how they deal with cardholder data of your customers.

**Do you accept other compliance certificates next to the AoC?**

> No. The Attestations of Compliance \(AoC\) is the only official document recognized for PCI DSS validation. Any other forms of certification issued for the purposes of illustrating compliance towards PCI DSS are not acceptable for proving compliance.

**How are the cost of using PCI Proxy?**

> Our pricing model is based on actual performance we deliver to you. Unlike others, we don't charge you for storing credit cards as we understand that you often have no influence on the duration of storage. Instead, our flexible plans are grouped in volume tiers to keep you from surprise fees. You only pay for exactly what you need. All plans include free setup and use of channels and APIs and fast and reliable tokenization of credit card data off the shelf.

**Where do I find additional information about PCI DSS?**

> Global Registry of PCI compliant service providers:
>
> * [http://www.visa.com/splisting/searchGrsp.do](http://www.visa.com/splisting/searchGrsp.do)
> * [https://www.visaeurope.com/receiving-payments/security/downloads-and-resources](https://www.visaeurope.com/receiving-payments/security/downloads-and-resources)
> * [https://www.mastercard.us/en-us/merchants/safety-security/security-recommendations/merchants-need-to-know.html](https://www.mastercard.us/en-us/merchants/safety-security/security-recommendations/merchants-need-to-know.html)
> * [https://de.pcisecuritystandards.org/document\_library](https://de.pcisecuritystandards.org/document_library)
> * [https://www.pcisecuritystandards.org/faqs](https://www.pcisecuritystandards.org/faqs)



