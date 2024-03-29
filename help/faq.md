# FAQ

## How does PCI Proxy reduce my PCI DSS scope? <a href="#how-does-pci-proxy-reduce-my-pci-dss-scope" id="how-does-pci-proxy-reduce-my-pci-dss-scope"></a>

The key for merchants and service providers wishing to reduce their PCI DSS scope is to not store, process, or transmit any sensitive cardholder data. By using PCI Proxy, we take care of that challenge by shielding your servers from sensitive card data. As a result, your servers never get in touch with sensitive card data again and you can rely on our full PCI DSS Level 1 certification.

## What credit card types does PCI Proxy support? <a href="#what-credit-card-types-does-pci-proxy-support" id="what-credit-card-types-does-pci-proxy-support"></a>

PCI Proxy automatically collects, stores, and tokenizes all PCI DSS relevant card data. Currently, we support all major brands and additional virtual cards such as Visa, Mastercard, American Express, Diners, Discover, JCB, ELO, Maestro, Expedia Virtual Cards, Booking.com Virtual Cards, AirPlus, etc. Do you need additional brands to be tokenized? [Contact us](https://www.pci-proxy.com/pci-proxy/contact/).

## What are the costs of using PCI Proxy? <a href="#what-are-the-costs-of-using-pci-proxy" id="what-are-the-costs-of-using-pci-proxy"></a>

Our pricing model is based on actual performance we deliver to you. Unlike others, we don't charge you for storing credit cards as we understand that you often have no influence on the duration of storage. Instead, you only pay for exactly what you need. All plans include free setup and use of channels and APIs and fast and reliable tokenization of credit card data off the shelf.

## What token formats does PCI Proxy support? <a href="#what-token-formats-does-pci-proxy-support" id="what-token-formats-does-pci-proxy-support"></a>

**Alias 2.0** - Example: \_AAABcH0Bq92s3kgAESIAAbGj5NIsAHWCThis format consists of 32 digits, letters, dash and underline, for full tokenization of the credit card number**Masked Credit Card Token** - Example: _1234 56AB CDEF 3456_This format consists of the first 6 digits of the real credit card number, the actual BIN Range (Bank Identification Number), followed by the token in form of 6 upper-case letters. The Masked Credit Card Token ends with the last 4 digits of the actual credit card number..

## Why do I have to provide the PCI DSS Attestation of Compliance (AoC) if I want to pass stored card data on to a 3rd party? <a href="#why-do-i-have-to-provide-the-pci-dss-attestation-of-compliance-aoc-if-i-want-to-pass-stored-card-dat" id="why-do-i-have-to-provide-the-pci-dss-attestation-of-compliance-aoc-if-i-want-to-pass-stored-card-dat"></a>

In order to forward plain credit card data to a 3rd party, that 3rd party needs to be PCI compliant. The PCI DSS Attestation of Compliance (AoC) is an obligation for each party involved in the credit card acceptance or transmission. Therefore, it is your responsibility to make sure you are collaborating with the right partners. Knowing your partners' compliance status provides assurance and awareness about how they deal with cardholder data of your customers.

## Do you accept other compliance certificates next to the AoC? <a href="#do-you-accept-other-compliance-certificates-next-to-the-aoc" id="do-you-accept-other-compliance-certificates-next-to-the-aoc"></a>

No. The Attestations of Compliance (AoC) is the only official document recognized for PCI DSS validation. Any other forms of certification issued for the purposes of illustrating compliance towards PCI DSS are not acceptable for proving compliance.

## I'm PCI-certified - Can I still use your storage vault? <a href="#im-pci-certified-can-i-still-use-your-storage-vault" id="im-pci-certified-can-i-still-use-your-storage-vault"></a>

Yes, if you are PCI certified and just want to store your sensitive card data in our secure vaults in Switzerland, you can connect via our XML Alias Gateway API to tokenize on-the-fly.

## Can I act as a payment facilitator? <a href="#can-i-act-as-a-payment-facilitator" id="can-i-act-as-a-payment-facilitator"></a>

Working with PCI Proxy allows you to store your customers' credit card data in our vault without ever touching your servers. PCI Proxy takes care of passing that sensitive card data directly to the gateway or API endpoint, who settles the funds into the respective merchant account.If you're looking to operate as a platform like Etsy or eBay, you'll be able to onboard thousands of different merchants and route payments to their own merchant account on their behalf - all without ever touching the money or sensitive card data yourself.

## Can you help me to receive a PCI Level 1 certification? <a href="#can-you-help-me-to-receive-a-pci-level-1-certification" id="can-you-help-me-to-receive-a-pci-level-1-certification"></a>

Yes, PCI Proxy works closely with PCI-accredited Qualified Security Assessors (QSA). They know our platform and can help you achieve the highest PCI Level 1 compliance. Depending on your environment, our QSAs allow you to achieve Level 1 compliance within less than 14 days including info packages, documentation templates, onsite audit, Report on Compliance (ROC) and the finalized Attestation of Compliance (AOC). [Contact us ](contact.md)for more details.

## Where do I find additional information about PCI DSS? <a href="#where-do-i-find-additional-information-about-pci-dss" id="where-do-i-find-additional-information-about-pci-dss"></a>

{% embed url="https://www.pcisecuritystandards.org/faqs" %}
PCI Council - FAQs
{% endembed %}

{% embed url="https://www.pcisecuritystandards.org/document_library" %}
PCI Council - Document Library (find SAQs & PCI DSS specs)
{% endembed %}

